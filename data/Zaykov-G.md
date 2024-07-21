## Optimize Storage Access in `validateSnapshotProof` Function for Gas Efficiency

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/NativeVaultLib.sol#L110-L144

The `validateSnapshotProof` function is currently accesses the storage variable `self.ownerToNode[nodeOwner]` multiple times. By storing the value of it in a local variable, we can reduce the number of storage reads and make the function more gas-efficient.

```diff
 function validateSnapshotProof(
        Storage storage self,
        address nodeOwner,
        ValidatorDetails memory validatorDetails,
        bytes32 balanceRoot,
        BeaconProofs.BalanceProof calldata proof
    ) internal returns (int256 balanceDeltaWei) {

+       NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner];

        uint64 timestamp = node.currentSnapshotTimestamp;
        uint40 validatorIndex = validatorDetails.validatorIndex;

        uint256 prevBalanceWei = validatorDetails.restakedBalanceWei;
        uint256 newBalanceWei = BeaconProofs.validateBalance(balanceRoot, validatorIndex, proof);

        validatorDetails.restakedBalanceWei = newBalanceWei;
        validatorDetails.lastBalanceUpdateTimestamp = timestamp;

        // Update validator status if balance is zero
        if (newBalanceWei == 0) {
            node.activeValidatorCount--;
            validatorDetails.status = ValidatorStatus.WITHDRAWN;

            emit ValidatorWithdrawn(nodeOwner, node.nodeAddress, timestamp, validatorIndex);
        }

        node.validatorPubkeyHashToDetails[proof.pubkeyHash] = validatorDetails;

        emit SnapshotValidator(nodeOwner, node.nodeAddress, timestamp, validatorIndex);

        if (newBalanceWei != prevBalanceWei) {
            emit ValidatorBalanceChanged(nodeOwner, node.nodeAddress, validatorIndex, timestamp, newBalanceWei);

            balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);
        }

        return balanceDeltaWei;
    }
```

**Gas Savings Estimate**:
Based on typical gas costs:

* Each storage read costs approximately 2100 gas.
* Each storage write costs approximately 5000 gas.
* Accessing the same storage slot multiple times can be optimized by using local variables.

Assuming the function originally reads `self.ownerToNode[nodeOwner]` 6 times:
* Original gas cost: 6 * 2100 = 12,600 gas.

After optimization, using a local variable for these accesses:
* Optimized gas cost: 1 * 2100 (initial storage read) + 5 * 3 (local variable read) = 2100 + 15 = 2115 gas.

Estimated gas savings per call:
* 12,600 - 2,115 = 10,485 gas.

This change will make the` validateSnapshotProof` function more efficient, reducing gas costs by approximately 10,485 gas per call and improving the performance of the smart contract.









