Improper approach. Double checking non-zero addresses in the array.
```solidity
        bytes32[] memory results = core.extSloads(slots);
        uint256 count = 0;
        for (uint256 i = 0; i < results.length; i++) {
            if (results[i] != bytes32(0)) count++;
        }
        vaults = new address[](count);
        uint256 latestIndex = 0;
        for (uint256 i = 0; i < results.length; i++) {
            if (results[i] != bytes32(0)) vaults[latestIndex++] = stakedVaults[i];
        }
```

https://github.com/code-423n4/2024-07-karak/blob/main/src/Qurier.sol#L32-L41
I think it could be better to returning the count of non-zero addresses from core.extSloads function and avoid recounting. 