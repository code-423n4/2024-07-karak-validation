 QA Report for Karak

## Table of Contents

| Issue ID                                                                                                              | Description                                                                                           |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [QA-01](#qa-01-fix-typos-_2-instances_)                                                                               | Fix typos: _2 instances_                                                                              |
| [QA-02](<#qa-02-wrong-error-messages-for-sister-_(_pause/_unpause)_-functions>)                                       | Wrong error messages for sister _`(_pause/_unpause)`_ functions                                       |
| [QA-03](#qa-03-reserved-addresses-for-both-default_node_implementation_flag-&-default_vault_implementation_flag)      | Reserved addresses for both `DEFAULT_NODE_IMPLEMENTATION_FLAG` & `DEFAULT_VAULT_IMPLEMENTATION_FLAG`  |
| [QA-04](#qa-04-operators-manager-can-break-the-protocol)                                                              | Operator's manager can break the protocol                                                             |
| [QA-05](#qa-05-vault.sol-redeem-process-is-not-compliant-with-4626)                                                   | Vault.sol redeem process is not compliant with 4626                                                   |
| [QA-06](#qa-06-the-same-function-selector-should-use-the-same-pause-checker)                                          | The same function selector should use the same pause checker                                          |
| [QA-07](#qa-07-setters-dont-have-equality-checkers)                                                                   | Setters don't have equality checkers                                                                  |
| [QA-08](#qa-08-low-level-calls-to-the-dss-could-still-be-passed-on-when-not-enough-gas-is-passed-leading-to-failures) | Low Level calls to the DSS could still be passed on when not enough gas is passed leading to failures |
| [QA-09](#qa-09-dont-cast-timestamp-to-uint48)                                                                         | Don't cast timestamp to uint48                                                                        |
| [QA-10](#qa-10-import-declarations-should-import-specific-identifiers-rather-than-the-whole-file)                     | Import declarations should import specific identifiers, rather than the whole file                    |

## QA-01 Fix typos: _2 instances_

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/Vault.sol#L124-L149

```solidity
    /// @return withdrawalKey The ID of the withdrawl. This is variable is shared across everyone's withdrawal request in the vault
    function startRedeem(uint256 shares, address beneficiary)
        external
        whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
        nonReentrant
        returns (bytes32 withdrawalKey)
    {
        if (shares == 0) revert ZeroShares();
        if (beneficiary == address(0)) revert ZeroAddress();

        (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
        address staker = msg.sender;

        uint256 assets = convertToAssets(shares);

        withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);

        state.withdrawalMap[withdrawalKey].staker = staker;
        state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
        state.withdrawalMap[withdrawalKey].shares = shares;
        state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;

        this.transferFrom(msg.sender, address(this), shares);

        emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
    }
```

### Impact

QA, confusing code.

### Recommended Mitigation Steps

https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/Vault.sol#L124-L149

```diff
-    /// @return withdrawalKey The ID of the withdrawl. This is variable is shared across everyone's withdrawal request in the vault
+    /// @return withdrawalKey The ID of the withdrawal. This is variable is shared across everyone's withdrawal request in the vault
    function startRedeem(uint256 shares, address beneficiary)
        external
        whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
        nonReentrant
        returns (bytes32 withdrawalKey)
    {
        if (shares == 0) revert ZeroShares();
        if (beneficiary == address(0)) revert ZeroAddress();

        (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
        address staker = msg.sender;

        uint256 assets = convertToAssets(shares);

        withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);

        state.withdrawalMap[withdrawalKey].staker = staker;
        state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
        state.withdrawalMap[withdrawalKey].shares = shares;
        state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;

        this.transferFrom(msg.sender, address(this), shares);

        emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
    }
```

Also https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/NativeVault.sol#L164-L167

```diff
-    /// @notice Validates that a validator's withdrawal credentials are pointed to the an owner's NativeNode.
+    /// @notice Validates that a validator's withdrawal credentials are pointed to the owner's NativeNode.
    /// @param nodeOwner: address of the owner whose NativeNode the proof is submitted for
    /// @param beaconStateRootProof: proof of a beacon state root against the beacon block root
    /// @param validatorFieldsProofs: validator fields proofs validated against the beacon state root
```

## QA-02 Wrong error messages for sister _`(_pause/_unpause)`_ functions

### Proof of Concept

First see https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/Pauser.sol#L32-L34

```solidity
    error AttemptedUnpauseWhilePausing();

    error AttemptedPauseWhileUnpausing();
```

These are the error messages available for wrong instances of pausing & unpausing

Now take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/Pauser.sol#L67-L79

```solidity
    function _pause(uint256 map) internal virtual {
        PauserStorage storage self = _getPauserStorage();
        if ((self._paused & map) != self._paused) revert AttemptedUnpauseWhilePausing();
        self._paused = map;
        emit Paused(_msgSender(), map);
    }

    function _unpause(uint256 map) internal virtual {
        PauserStorage storage self = _getPauserStorage();
        if (self._paused & map != map) revert AttemptedPauseWhileUnpausing();
        self._paused = map;
        emit Unpaused(_msgSender(), map);
    }
```

Evidently the error messages have been swapped using the `_pause` function as an example if the condition `(self._paused & map) != self._paused` is true, it reverts with `AttemptedUnpauseWhilePausing`. However, this error message doesn't accurately describe the situation, which is attempting to pause functions that are already unpaused, and should instead be `AttemptedPauseWhileUnpausing`, a similar case is applicable to the `_unpause` function too.

### Impact

QA

### Recommended Mitigation Steps

Consider applying these changes:

```diff
    function _pause(uint256 map) internal virtual {
        PauserStorage storage self = _getPauserStorage();
        if ((self._paused & map) != self._paused) revert AttemptedUnpauseWhilePausing();
        self._paused = map;
        emit Paused(_msgSender(), map);
    }

    function _unpause(uint256 map) internal virtual {
        PauserStorage storage self = _getPauserStorage();
        if (self._paused & map != map) revert AttemptedPauseWhileUnpausing();
        self._paused = map;
        emit Unpaused(_msgSender(), map);
    }
```

## QA-03 Reserved addresses for both `DEFAULT_NODE_IMPLEMENTATION_FLAG` & `DEFAULT_VAULT_IMPLEMENTATION_FLAG`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/interfaces/Constants.sol#L4-L7

```solidity
library Constants {
    address public constant DEFAULT_NODE_IMPLEMENTATION_FLAG = address(1);
    address public constant DEFAULT_VAULT_IMPLEMENTATION_FLAG = address(1);

```

These are both the reserved addresses for the `DEFAULT_NODE_IMPLEMENTATION_FLAG` & `DEFAULT_VAULT_IMPLEMENTATION_FLAG` , and as can be seen from the below we can see that attach a new vault implemenetation to these addresses https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/Core.sol#L173-L179

```solidity
    function changeStandardImplementation(address newVaultImpl) external onlyOwner {
        if (newVaultImpl == address(0)) revert ZeroAddress();
        if (newVaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();
        _self().vaultImpl = newVaultImpl;
        emit UpgradedAllVaults(newVaultImpl);
    }

```

Issue however is that the same address is reserved for 2 different parties which showcases the logic is broken.

### Impact

QA

### Recommended Mitigation Steps

Consider applying these changes:
https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/interfaces/Constants.sol#L4-L7

```diff
library Constants {
    address public constant DEFAULT_NODE_IMPLEMENTATION_FLAG = address(1);
-    address public constant DEFAULT_VAULT_IMPLEMENTATION_FLAG = address(1);
+    address public constant DEFAULT_VAULT_IMPLEMENTATION_FLAG = address(2);

```

## QA-04 Operator's manager can break the protocol

### Proof of Concept

When NativeVault is created, its manager is granted a role that allows him to pause different actions.

For e.g see https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/NativeVault.sol#L299-L318

```solidity
    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
        external
        onlyOwner
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_SLASHER)
        returns (uint256 transferAmount)
    {
        NativeVaultLib.Storage storage self = _state();

        if (slashingHandler != self.slashStore) revert NotSlashStore();

        // avoid negative totalAssets if slashing amount is greater than totalAssets
        if (totalAssetsToSlash > self.totalAssets) {
            totalAssetsToSlash = self.totalAssets;
        }

        self.totalAssets -= totalAssetsToSlash;
        emit Slashed(totalAssetsToSlash);
        return totalAssetsToSlash;
    }
```

Now with such power, the manager can break some functionality of the protocol. An example of such actions is slashing as hinted above, since the
manager can pause it and then Core contract will not be able to slash funds
from the operator. Another example: the manager can forbid users to withdraw.

### Impact

QA

### Recommended Mitigation Steps

Think about attaching a timelock to core changes.

## QA-05 Vault.sol redeem process is not compliant with 4626

### Proof of Concept

https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/Vault.sol#L157-L188

```solidity
    function finishRedeem(bytes32 withdrawalKey)
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_VAULT_FINISH_REDEEM)
    {
        (VaultLib.State storage state, VaultLib.Config storage config) = _storage();

        WithdrawLib.QueuedWithdrawal memory startedWithdrawal = state.validateQueuedWithdrawal(withdrawalKey);

        uint256 shares = startedWithdrawal.shares;
        if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();
        uint256 redeemableAssets = convertToAssets(shares);

        delete state.withdrawalMap[withdrawalKey];

        _withdraw({
            by: address(this),
            to: startedWithdrawal.beneficiary,
            owner: address(this),
            assets: redeemableAssets,
            shares: shares
        });

        emit FinishedRedeem(
            startedWithdrawal.staker,
            startedWithdrawal.beneficiary,
            config.operator,
            startedWithdrawal.shares,
            redeemableAssets,
            withdrawalKey
        );
    }
```

This function is used to finish a redeem process after waiting the required delay, issue however is that the redemption check is done on the wrong address, i.e `      if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();` it should instead be on the address who is going to get the final withdrawal from the `withdrawalKey`.

### Impact

- In the case where a user's maximum redemption should be lesser than that of the vault contract then they can sidestep the ERC4626 `maxRedeem` protection and redeem more than they should have access to.
- In the rare case where a user's max redemption is higher than that of the Vault, then they would be DOS'd from redeeming all of their tokens.

### Recommended Mitigation Steps

```diff

-       if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();
+       if (shares > maxRedeem(startedWithdrawal.staker)) revert RedeemMoreThanMax();

```

## QA-06 The same function selector should use the same pause checker

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/Vault.sol#L77-L103

```solidity

    function deposit(uint256 assets, address to)
        public
        override(ERC4626, IVault)
        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
        nonReentrant
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        return super.deposit(assets, to);
    }

    /// @notice Deposits assets into the vault with a minimum amount of shares to mint
    /// @dev This is to prevent any malicious frontrunning in ERC4626
    /// @param assets The amount of assets to deposit
    /// @param to The address to mint the shares to
    /// @param minSharesOut The minimum amount of shares to mint else revert
    function deposit(uint256 assets, address to, uint256 minSharesOut)
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT_SLIPPAGE)
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        shares = super.deposit(assets, to);
        if (shares < minSharesOut) revert NotEnoughShares();
    }
```

Both functions inherently deposit where one has a slippage implementation and the other doesn't, however their pauser checkers are different which isn't efficient considering they both just deposit, since deposit with slippage just calls `deposit` have only one `deposit` querier and have this protected by the `PAUSE_VAULT_DEPOSIT` checker.

### Impact

QA, inefficiency of code.

### Recommended Mitigation Steps

Consider applying these changes:

```diff

    function deposit(uint256 assets, address to)
        public
        override(ERC4626, IVault)
        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
        nonReentrant
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        return super.deposit(assets, to);
    }

    /// @notice Deposits assets into the vault with a minimum amount of shares to mint
    /// @dev This is to prevent any malicious frontrunning in ERC4626
    /// @param assets The amount of assets to deposit
    /// @param to The address to mint the shares to
    /// @param minSharesOut The minimum amount of shares to mint else revert
    function deposit(uint256 assets, address to, uint256 minSharesOut)
        external
        nonReentrant
+        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
-        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT_SLIPPAGE)
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        shares = super.deposit(assets, to);
        if (shares < minSharesOut) revert NotEnoughShares();
    }
```

## QA-07 Setters don't have equality checkers

### Proof of Concept

https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/CoreLib.sol#L56-L66

```solidity
    function updateGasValues(
        Storage storage self,
        uint32 _hookCallGasLimit,
        uint32 _supportsInterfaceGasLimit,
        uint32 _hookGasBuffer
    ) internal {
        self.hookCallGasLimit = _hookCallGasLimit;
        self.hookGasBuffer = _hookGasBuffer;
        self.supportsInterfaceGasLimit = _supportsInterfaceGasLimit;
    }

```

### Impact

QA, unnecesary code execution

### Recommended Mitigation Steps

Implement equality checkers for the function.

## QA-08 Low Level calls to the DSS could still be passed on when not enough gas is passed leading to failures

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/HookLib.sol#L78-L103

```solidity
function callHookIfInterfaceImplemented(
    IERC165 dss,
    bytes memory data,
    bytes4 interfaceId,
    bool ignoreFailure,
    uint32 hookCallGasLimit,
    uint32 supportsInterfaceGasLimit,
    uint32 hookGasBuffer
) internal returns (bool) {
    if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {
        revert NotEnoughGas();
    }

    (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(
        address(dss),
        abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId),
        supportsInterfaceGasLimit
    );

    if (!success || result == bytes32(0)) {
        emit InterfaceNotSupported();
        return false;
    }
    return callHook(address(dss), data, ignoreFailure, hookCallGasLimit, hookGasBuffer);
}
```

This function performs low-level calls to the DSS with given data, returns boolean incase of success or failure with a check to ensure enough gas is passed (`supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer`). However, this check isn't foolproof. When `supportsInterfaceGasLimit` is not a multiple of `63`, the calculation can suffer from precision loss, causing calls to succeed when they shouldn't.

To avoid failures, the low-level call is designed to use at most 63/64th of the available gas. However, even with this calculation, calls can fail. For instance, with `supportsInterfaceGasLimit` of `984374`, `hookGasBuffer` of `100000`, and `gasleft()` of `1099998`, the check would not revert as expected due to rounding down.

### Impact

Low-level calls to the DSS may not behave as expected, breaking considerations around gas consumption.

### Recommended Mitigation Steps

Apply the following changes to account for potential precision loss:

```diff

-        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {
+        if (gasleft() <= (supportsInterfaceGasLimit * 64 / 63 + 1 hookGasBuffer)) {
        revert NotEnoughGas();
    }

#
```

## QA-09 Don't cast timestamp to uint48

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/Operator.sol#L61-L88

```solidity
    function requestUpdateVaultStakeInDSS(
        CoreLib.Storage storage self,
        StakeUpdateRequest memory requestStakeUpdate,
        uint128 nonce,
        address operator
    ) external returns (QueuedStakeUpdate memory queuedStake) {
        State storage operatorState = self.operatorState[operator];
        validateStakeUpdateRequest(operatorState, requestStakeUpdate);
        queuedStake = QueuedStakeUpdate({
            nonce: uint48(nonce),
            startTimestamp: uint48(block.timestamp),
            operator: operator,
            updateRequest: requestStakeUpdate
        });
        operatorState.pendingStakeUpdates[requestStakeUpdate.vault] = calculateRoot(queuedStake);
        IDSS dss = requestStakeUpdate.dss;

        HookLib.callHookIfInterfaceImplemented({
            dss: dss,
            data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate),
            interfaceId: dss.requestUpdateStakeHook.selector,
            ignoreFailure: !requestStakeUpdate.toStake,
            hookCallGasLimit: self.hookCallGasLimit,
            supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
            hookGasBuffer: self.hookGasBuffer
        });
    }

```

Directly casting timestamps to uint48, reduces the lifetime of protocol.

### Impact

QA

### Recommended Mitigation Steps

Consider not casting timestamp to uint48.

## QA-10 Import declarations should import specific identifiers, rather than the whole file

### Proof of Concept

Multiple instances in scope, for example take a look at https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/SlasherLib.sol#L12-L16

```solidity
import "../interfaces/Errors.sol";
import "../interfaces/Constants.sol";
import "../interfaces/IDSS.sol";
import "../interfaces/IKarakBaseVault.sol";
import "../interfaces/Events.sol";
```

Evidently, the imports being done is not name specific, but this is not the best implementation cause this could lead to polluting the symbol namespace.

### Impact

QA, albeit this could lead to the potential pollution of the symbol namespace and a slower compilation speed.

### Recommended Mitigation Steps

Consider using import declarations of the form `import {<identifier_name>} from "some/file.sol"` which avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation (but does not save any gas), an example can be seen here https://github.com/code-423n4/2024-07-karak/blob/ab18e1f6c03e118158369527baa2487b2b4616b1/src/entities/SlasherLib.sol#L7-L10

```solidity
import {CoreLib} from "./CoreLib.sol";
import {HookLib} from "./HookLib.sol";
import {Operator} from "./Operator.sol";
import {CommonUtils} from "../utils/CommonUtils.sol";
```
