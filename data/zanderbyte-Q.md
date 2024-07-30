# [L-1] Inefficient call to `NativeNode` for slashed ETH transfer
## Impact
A call to `NativeNode` is performed to send a slashed amount of ETH on every invocation of `_startSnapshot` or `validateExpiredSnapshot`. However, in most cases, there will not be a slashing, resulting in unnecessary higher costs for these operations due to the redundant contract call.

## Proof of Concept
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L436

## Tools Used
Manual review
## Recommended Mitigation Steps
Add a check to ensure the value is sent only if `slashedWithdrawable` is not zero. This will avoid unnecessary contract calls and reduce gas costs.
```diff
    function _transferToSlashStore(address nodeOwner) internal {
        NativeVaultLib.Storage storage self = _state();
        NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner];

        // slashed ETH = total restaked ETH (node + beacon) - share price equivalent ETH
        uint256 slashedAssets = node.totalRestakedETH - convertToAssets(balanceOf(nodeOwner));

-       // sweepable ETH = min(ETH available on node address, total slashed ETH)
-       uint256 slashedWithdrawable = Math.min(node.nodeAddress.balance, slashedAssets);

-       // withdraw sweepable ETH to slashStore
-       INativeNode(node.nodeAddress).withdraw(self.slashStore, slashedWithdrawable);

-       // update total restaked ETH available (node + beacon)
-       node.totalRestakedETH -= slashedWithdrawable;
+        if (slashedWithdrawable != 0) {
+           // withdraw sweepable ETH to slashStore
+           INativeNode(node.nodeAddress).withdraw(self.slashStore, slashedWithdrawable);

+           // update total restaked ETH available (node + beacon)
+           node.totalRestakedETH -= slashedWithdrawable;  
        }

        // update withdrawable credited ETH available on the node only when node balance
        // decreases to less than that of the credited node ETH
        if (node.nodeAddress.balance < node.withdrawableCreditedNodeETH) {
            node.withdrawableCreditedNodeETH = node.nodeAddress.balance;
        }
    }
```
# [L-2] `validateExpiredSnapshot` can be called on a node that has not yet validated its own withrawal credentials

## Impact
`validateExpiredSnapshot` function is called from anyone to start a new snapshot if the last snapshot has expired. However an insufficient check in the function allows for creating a snapshot over a node which has not yet validated his withdrawal credentials.
## Tools Used
Manual review
## Recommendation 
Ensure the function can only be called on existing snapshot:
```diff

    function validateExpiredSnapshot(address nodeOwner)
        external
        nonReentrant
        nodeExists(nodeOwner)
        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_VALIDATE_EXPIRED_SNAPSHOT)
    {
        NativeVaultLib.NativeNode storage node = _state().ownerToNode[nodeOwner];
        // Only check if the last snapshot has expired or not
-       if (node.lastSnapshotTimestamp + Constants.SNAPSHOT_EXPIRY > block.timestamp) {
-           revert SnapshotNotExpired();
-       }
+       if (node.lastSnapshotTimestamp + Constants.SNAPSHOT_EXPIRY > block.timestamp || node.lastSnapshotTimestamp == 0) {
+           revert SnapshotNotExpired();
+       }

        _startSnapshot(node, false, nodeOwner);
    }
```

# [L-3] Veto Committee can be EOA
## Impact
As mentioned in the docs and nat specs - 
```solidity
/// @param _vetoCommittee: The address of the veto committee who can cancel/veto slashing requests. Should be a multisig.
```
Allowing the vetoCommittee to be an EOA instead of a smart contract multisig poses security risks, as a single private key compromise could lead to unauthorized canceling of slashing requests.

## Proof of Concept
There is no check to verify if `_vetoCommittee` is a smart contract in the `initialize` function:
```solidity
    function initialize(
        address _vaultImpl,
        address _manager,
        address _vetoCommittee, 
        uint32 _hookCallGasLimit,
        uint32 _supportsInterfaceGasLimit,
        uint32 _hookGasBuffer
    ) external initializer {
        _initializeOwner(msg.sender);
        __Pauser_init();

        _grantRoles(_manager, Constants.MANAGER_ROLE);
@>      _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);

        _self().init(_vaultImpl, _vetoCommittee, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
    }
```

## Tools Used
Manual Review
## Recommended Mitigation Steps
Add a check to ensure `_vetoCommittee` address is a smart contract. You can use the `isContract` method from OpenZeppelin's Address library to implement this check. Here is a sample implementation:

```solidity
import "@openzeppelin/contracts/utils/Address.sol";

function initialize(
    address _vaultImpl,
    address _manager,
    address _vetoCommittee,
    uint32 _hookCallGasLimit,
    uint32 _supportsInterfaceGasLimit,
    uint32 _hookGasBuffer
) external initializer {
    require(Address.isContract(_vetoCommittee), "VetoCommittee must be a contract");

    _initializeOwner(msg.sender);
    __Pauser_init();

    _grantRoles(_manager, Constants.MANAGER_ROLE);
    _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);

    _self().init(_vaultImpl, _vetoCommittee, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
}
```
# [L-4] `maxDeposit` function in `NativeVault` always returns `type(uint256).max`
## Impact
When the `_increaseBalance` function is called, there is a check to ensure that the newly added assets do not exceed the maximum balance. However, the `maxDeposit` function is not overridden in the `NativeVault` contract and always returns `type(uint256).max`. This makes the check ineffective and redundant, as the condition `assets + self.totalAssets > maxDeposit(_of)` will never be true.

## Proof of Concept
The check is performed in `_increaseBalance` function:
```solidity
    function _increaseBalance(address _of, uint256 assets) internal {
        NativeVaultLib.Storage storage self = _state();
@>      if (assets + self.totalAssets > maxDeposit(_of)) revert DepositMoreThanMax(); 
        uint256 shares = convertToShares(assets);
        _mint(_of, shares);
        self.totalAssets += assets;
        self.ownerToNode[_of].totalRestakedETH += assets;
        emit IncreasedBalance(self.ownerToNode[_of].totalRestakedETH);
    }
```
The `maxDeposit` function in the `ERC4626` contract is implemented as follows:
```solidity
    function maxDeposit(address to) public view virtual returns (uint256 maxAssets) {
        to = to; // Silence unused variable warning.
        maxAssets = type(uint256).max;
    }
```
## Tools Used
Manual review
## Recommended Mitigation Steps
Override the `maxDeposit` function in the `NativeVault` contract to return a meaningful limit for deposits or remove the check in `_increaseBalance` if no such limit is needed. 



# [I-1] `Constants.sol` is imported two times
## Impact
The `Constants.sol` file is imported twice in the `Core.sol` contract. While this does not have a direct impact on the functionality or security of the contract, it can lead to confusion and unnecessary clutter in the codebase.

## Proof of Concept
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L18
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L24C1-L24C37

## Tools Used
Manual review
## Recommended Mitigation Steps
Remove the second import statement to avoid redundancy.