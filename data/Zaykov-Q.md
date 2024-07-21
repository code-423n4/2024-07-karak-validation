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