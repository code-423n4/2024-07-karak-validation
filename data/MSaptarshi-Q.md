# [QA-1] Rebasing token/FOT may be problematic for slashing
While initiating a [slashing for a particular vault](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L202)
it burns the required amount by checking
`transferAmount = Math.min(totalAssets(), totalAssetsToSlash);` which burns the assets by the following way
```
   function handleSlashing(IERC20 token, uint256 amount) external {
        if (amount == 0) revert ZeroAmount();
        if (!_config().supportedAssets[token]) revert UnsupportedAsset();

        SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount);
        // Below is where custom logic for each asset lives
        SafeTransferLib.safeTransfer(address(token), address(0), amount);
    }
```
The problem here is if while initiating the slashing the `totalAssets` > `totalassetstoslash` so amount slashed =`totalassetstoslash` , but if rebasing occurs for a rebasing token,  which might result in the amount to slash decrease by the rebased amount. This might result in the full amount not getting slashed
## Recommendation
Query the balance before and after the transfer to address(0) for burning

# [QA-2] Slashing can be frontrunned to avoid penalty imposed on operator
`requestSlashing()` is used to take funds away from a operators when they misbehave.
```
 function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)
        external
        whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
        nonReentrant
        returns (SlasherLib.QueuedSlashing memory queuedSlashing)
    {
        IDSS dss = IDSS(msg.sender);
        CoreLib.Storage storage self = _self();
        self.checkIfOperatorIsRegInRegDSS(slashingRequest.operator, dss);
        queuedSlashing = self.requestSlashing(dss, slashingRequest, self.nonce++);
        emit RequestedSlashing(address(dss), slashingRequest);
    }
```
However, a malicious user can frontrun this operation and call `startRedeem()` to fully exit before the penalty can affect them.

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L125

Malicious users who have intentionally committed some offenses that would lead to getting slashed can listen to the mempool and frontrun the `requestSlashing()` function call by the protocol to protect all his assets before slashing can happen.

Slashing mechanism implemented can be bypassed by malicious operator.
The frontrunning can be done easily since both slashing and withdrawal is a two step process.
## Recommendation
I implore the sponsors to explore alternatives to this slashing mechanism as they can be easily bypassed, especially so by sophisticated users who presumably are the ones who will be getting slashed.

# [QA-3] Misguided check for allowed tokens
The project checks for tokens allowed for slashing in [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L288)
```
function isAssetAllowlisted(address asset) public view returns (bool) {
        return _self().assetSlashingHandlers[asset] != address(0);
    }
```
But this check is not appropriate since a token which is not allowed in the vault in [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/VaultLib.sol#L11), may get allowlisted in [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/SlashingHandler.sol#L43)
```
function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {
        return _config().asset;
    }
```
So a token which is not allowed in the vault(let's say USDC) may get allowlisted in `slashingHandler`, which might result in inappropriate user experience , since  any unallowed asset would show as allowed for slashing
## Recommendation
Compare the asset in the slashing handler with the `Config` struct asset for vault implementation

# [QA-4] Admin can change the gas values suddenly
## Impact
Changing the [gas values](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L274) suddenly, can result in failure of certain operations {[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L78), [2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L162) , [3](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L194) ,.... } while implementation of the vault
```
function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)
        external
        onlyRolesOrOwner(Constants.MANAGER_ROLE)
    {
        _self().updateGasValues(_hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
    }
```
This could simply result in DOS of the vault

# [QA-5] Different Timestamp casting in different areas of the codebase
## Impact
1. While initiating a 2 step redeem process, the starting timestamp is [casted to uint96](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L142)
`state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);`
2. While updating a stake in DSS by a operator, the starting  timestamp is [casted to uint48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L71)
` startTimestamp: uint48(block.timestamp),`

This makes the readability and storage cost complex due to different way of storing the time

## Recommendation
Have the casting for both the starting time same

# [QA-6] Misguided check for address(0) in nodeOwner
Any addresses deployed by [create2 will not be address(0)](https://github.com/Vectorized/solady/blob/1f43cc8005cc3b3c8361dd7dbdd2cdeaf0f99e66/src/utils/LibClone.sol#L1517)
So having this check makes the line unnecessary increasing the storage cost for the codebase
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L530
## Recommendation
The check can be remodified by just checking if the particular nodeAddress is present in all the nodeAddress deployed by the create2 BeaconProxy 

# [QA-7] `isSmartContract` is not a adequate check for checking contract existance
While registering the DSS the contract checks if the DSS is a smartcontract, by check the [codesize](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/utils/CommonUtils.sol#L48)
```
function registerDSS(uint256 maxSlashablePercentageWad) external {
        IDSS dss = IDSS(msg.sender);
        if (!address(dss).isSmartContract()) revert NotSmartContract();
        _self().setDSSMaxSlashablePercentageWad(dss, maxSlashablePercentageWad);
        emit DSSRegistered(msg.sender, maxSlashablePercentageWad);
    }
```
However, this check can be passed even though input is a smart contract if
Function is called in the constructor, since during construction code length is 0.Smart contract that has not been deployed yet can be used. The CREATE2 opcode can be used to deterministically calculate the address of a smart contract before it is created. This means that the user can bypass this check by calling this function before deploying the contract.
