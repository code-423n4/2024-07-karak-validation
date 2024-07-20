## Length Mismatch Check in `allowlistAssets` Function


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
