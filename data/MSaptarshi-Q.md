# [QA-1] Different Timestamp casting in different areas of the codebase
## Impact
1. While initiating a 2 step redeem process, the starting timestamp is [casted to uint96](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L142)
`state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);`
2. While updating a stake in DSS by a operator, the starting  timestamp is [casted to uint48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L71)
` startTimestamp: uint48(block.timestamp),`

This makes the readability and storage cost complex due to different way of storing the time

## Recommendation
Have the casting for both the starting time same

# [QA-2] Misguided check for address(0) in nodeOwner
Any addresses deployed by [create2 will not be address(0)](https://github.com/Vectorized/solady/blob/1f43cc8005cc3b3c8361dd7dbdd2cdeaf0f99e66/src/utils/LibClone.sol#L1517)
So having this check makes the line unnecessary increasing the storage cost for the codebase
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L530
## Recommendation
The check can be remodified by just checking if the particuolar nodeAddress is present in all the nodeAddress deployed by the create2 BeaconProxy 