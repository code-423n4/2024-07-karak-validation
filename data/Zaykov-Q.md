## [L-01] Length Mismatch Check in `allowlistAssets` Function


The `allowlistAssets` function currently does not verify that the lengths of the assets and `slashingHandlers` arrays are equal. This oversight can lead to transaction failures if the provided arrays have mismatched lengths.
If the assets and `slashingHandlers` arrays have different lengths, the function will revert, causing the transaction to fail:

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L82-L91

### Recommended Fix:
```diff
   function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)
        external
        onlyRolesOrOwner(Constants.MANAGER_ROLE)
    {
+       if(assets.length != slashingHandlers.length) revert LengthsDontMatch();
        _self().allowlistAssets(assets, slashingHandlers);
        emit AllowlistedAssets(assets);
    }
```
## [L-02] Accurate Event Logging in validateSnapshotProof Function
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/NativeVaultLib.sol#L137-L141

In the validateSnapshotProof function, the calculation of balanceDeltaWei should precede the emission of the ValidatorBalanceChanged event. This change ensures that the event logs the correct balance change and reflects the accurate state of the contract at the time of the event emission.

The ValidatorBalanceChanged event is emitted before calculating the balanceDeltaWei, which may lead to incorrect logging of the balance change.

if (newBalanceWei != prevBalanceWei) {
    emit ValidatorBalanceChanged(nodeOwner, nodeAddress, validatorIndex, timestamp, newBalanceWei);

    balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);
}


Issue:
Emitting the ValidatorBalanceChanged event before calculating balanceDeltaWei may result in the event not accurately reflecting the actual balance change that has occurred.

Optimized Implementation:
if (newBalanceWei != prevBalanceWei) {
    balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);
    emit ValidatorBalanceChanged(nodeOwner, nodeAddress, validatorIndex, timestamp, newBalanceWei);
}

## [C-01] Add name constant inside `BeaconProofsLib.sol`

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/BeaconProofsLib.sol#L65
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/BeaconProofsLib.sol#L98

The library currently uses the magic number 32 to represent the size of a hash in multiple places. This can make the code harder to read and maintain, as the significance of the number 32 is not immediately clear. By defining a named constant for the hash size, the code will be more readable, maintainable, and less prone to errors when changes are needed.

```
        if (validatorProof.length != 32 * ((VALIDATOR_HEIGHT + 1) + BEACON_STATE_HEIGHT)) {
```
```
        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();
```
### Recommended Fix:
Define a name constant for better understanding.

## [C-01] Function `allowlistVaultImpl` and `isDSSRegistered` in CoreLib.sol are not used 

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/CoreLib.sol#L153-L155

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/CoreLib.sol#L161-L163

The `allowlistVaultImpl` and `isDSSRegistered` inside CoreLib.sol are never used. If they are not supposed to be used in the contract it is better to be removed.

```
function allowlistVaultImpl(Storage storage self, address implementation) internal {
        self.allowlistedVaultImpl[implementation] = true;
    }
```
```
 function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {
        return self.dssMaxSlashablePercentageWad[dss] != 0;
    }
```