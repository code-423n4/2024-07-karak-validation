# G-01 Missing check for zero amount

In the `_transferToSlashStore` function in NativeVault.sol [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L430). The amount of `slashedAssets` is calculated and afterwards it calls `withdraw` on the native node. This does not consider the (common) case that the user does not have any slashed assets. By adding a check for zero (as shown below), the cost of a snapshot can be reduces substantially:

```
    function _transferToSlashStore(address nodeOwner) internal {
        NativeVaultLib.Storage storage self = _state();
        NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner];

        // slashed ETH = total restaked ETH (node + beacon) - share price equivalent ETH
        uint256 slashedAssets = node.totalRestakedETH - convertToAssets(balanceOf(nodeOwner));

        ####if (slashedAssets == 0) return;####

        // sweepable ETH = min(ETH available on node address, total slashed ETH)
        uint256 slashedWithdrawable = Math.min(node.nodeAddress.balance, slashedAssets);

        // withdraw sweepable ETH to slashStore
        INativeNode(node.nodeAddress).withdraw(self.slashStore, slashedWithdrawable);

        // update total restaked ETH available (node + beacon)
        node.totalRestakedETH -= slashedWithdrawable;

        // update withdrawable credited ETH available on the node only when node balance
        // decreases to less than that of the credited node ETH
        if (node.nodeAddress.balance < node.withdrawableCreditedNodeETH) {
            node.withdrawableCreditedNodeETH = node.nodeAddress.balance;
        }
    }
```

Using forge gas-reports it was shown, that this reduces the gas used of the `startSnapshot` function from an median of `154_754` to `104_364` (~32.5%).


# G-02 Using soldity snippets for common functions
CommonUtils.sol implements a custom sorting function for an array of addresses. It is a lot more gas efficient (and less error prone) to use a existing snipped for these common functions. Seeing that solady is already being utilized by Karak, it was compared to their LibSort.sol implementation [solady-LibSort](https://github.com/Vectorized/solady/blob/main/src/utils/LibSort.sol):
Using forge's gas report, the gas used of `hasDuplicates` in CommonUtils.sol was reduced from `452_073` to `99_278`. Also running the tests shows a similar improvement: Running `duplicateChecker.t.sol` with the custom implementation:
```
[PASS] test_dupes() (gas: 66773)
[PASS] test_empty_array() (gas: 17465)
[PASS] test_no_dupes() (gas: 51402)
[PASS] test_largeSort(bytes22) (runs: 258, μ: 392777, ~: 398616)
```

Using solady:
```
PASS] test_dupes() (gas: 48905)
[PASS] test_empty_array() (gas: 17460)
[PASS] test_no_dupes() (gas: 38968)
[PASS] test_largeSort(bytes22) (runs: 258, μ: 164442, ~: 163974)
```
Note: test_largeSort sorts an array of length 32 - the current max amount per slashing.

Therefor it was shown that by using an optimized sorting implementation, the gas usage can be optimized by up to 58.8%.


# G-03 Using a optimized EnumerableSet implementation

Seeing that solady is already utilized by Karak and EnumerableSet being used extensively in the `Operator` library, the `EnumerableSet` implementation by OpenZeppelin was replaced by the only by solady `EnumerableSetLib.sol` [source](https://github.com/Vectorized/solady/blob/main/src/utils/EnumerableSetLib.sol):
```
import {EnumerableSetLib} from "solady/src/utils/EnumerableSetLib.sol";

...

library Operator {
    using EnumerableSetLib for EnumerableSetLib.AddressSet;
    using CoreLib for CoreLib.Storage;

    struct State {
        EnumerableSetLib.AddressSet vaults;
        EnumerableSetLib.AddressSet dssMap;
        mapping(IDSS dss => EnumerableSetLib.AddressSet vaultStakeInDss) vaultStakedInDssMap;
        mapping(IDSS dss => uint256 timestamp) nextSlashableTimestamp; // When this operator can be slashed again by a DSS
        mapping(address vault => bytes32 updateHash) pendingStakeUpdates; //Supporting only 1 update per vault at a time
    }
...
```

Below shows a comparison using forge gas-report on impacted Core.sol functions:
```
| src/Core.sol:Core contract      | EnumerableSet OpenZeppelin ||  EnumerableSetLib solady | median gas saved |
|---------------------------------|--------|- -------|- -------||--------|--------|--------|------------------|
| Function Name                   | avg    |  median |  max    || avg    | median | max    |                  |
| deployVaults                    | 680733 |  680733 |  680733 || 610518 | 610518 | 610518 |  70215 |  10.31% |
| fetchVaultsStakedInDSS          | 6756   |  7181   |  7471   || 5289   | 5720   | 8633   |   1461 |  20.35% |
| finalizeUpdateVaultStakeInDSS   | 78682  |  102804 |  111354 || 57259  | 65079  | 67243  |  37725 |  36.70% |
| getLeverage                     | 20418  |  20418  |  20475  || 19297  | 19297  | 19371  |   1121 |  5.49%  |
| isOperatorRegisteredToDSS       | 3207   |  3207   |  3207   || 2614   | 2562   | 2823   |    645 |  20.11% |
| registerOperatorToDSS           | 105760 |  120945 |  120945 || 70227  | 78344  | 78344  |  42601 |  35.22% |
| requestUpdateVaultStakeInDSS    | 58743  |  77956  |  77956  || 58229  | 76666  | 78800  |   1290 |  1.65%  |
```

Seeing those substantial improvements, it should be considered to use solady's implementation.

