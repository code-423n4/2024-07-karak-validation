# [QA-1] Rebasing token/FOT may cause problematic for slashing
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

# [QA-2] Misguided check for allowed tokens
The project checks for tokens allowed for slashing in [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L288)
```
function isAssetAllowlisted(address asset) public view returns (bool) {
        return _self().assetSlashingHandlers[asset] != address(0);
    }
```
But this check is not appropriate since a token which is not allowed in the vault in [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/VaultLib.sol#L11)
```
function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {
        return _config().asset;
    }
```
So a token which is not allowed in the vault(let's say USDC) may get allowlisted in `slashingHandler`, which might result in inappropriate user experience , since  any unallowed asset would show as allowed for slashing
## Recommendation
Compare the asset in the slashing handler with the `Config` struct asset for vault implementation

# [QA-3] Admin can change the gas values suddenly
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

# [QA-4] Different Timestamp casting in different areas of the codebase
## Impact
1. While initiating a 2 step redeem process, the starting timestamp is [casted to uint96](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L142)
`state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);`
2. While updating a stake in DSS by a operator, the starting  timestamp is [casted to uint48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L71)
` startTimestamp: uint48(block.timestamp),`

This makes the readability and storage cost complex due to different way of storing the time

## Recommendation
Have the casting for both the starting time same

# [QA-5] Misguided check for address(0) in nodeOwner
Any addresses deployed by [create2 will not be address(0)](https://github.com/Vectorized/solady/blob/1f43cc8005cc3b3c8361dd7dbdd2cdeaf0f99e66/src/utils/LibClone.sol#L1517)
So having this check makes the line unnecessary increasing the storage cost for the codebase
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L530
## Recommendation
The check can be remodified by just checking if the particular nodeAddress is present in all the nodeAddress deployed by the create2 BeaconProxy 