## [L-01] The veto committee retains the authority to cancel a slashing request even after the expiration of the veto window.

### Links to affected code

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/SlasherLib.sol#L153-L168

### Description

A dss may be unable to finalize a slashing request even after veto window due to the late cancellation.

I added a new test case to `slashing.t.sol` for PoC purpose.

```solidity
    function test_cancel_slashing_after_veto_window(uint96 slashPercentageWad) public {
        uint256 elapsedTime = 3 days;
        vm.assume(
            slashPercentageWad > Constants.ONE_WAD && slashPercentageWad <= core.getDssMaxSlashablePercentageWad(dss)
        );
        stake_vaults_to_dss();
        uint96[] memory slashPercentagesWad = new uint96[](vaults.length);
        slashPercentagesWad[0] = slashPercentageWad;
        // Generate nonequal percentages
        uint96 slashPercentageWad1 =
            (slashPercentageWad + uint96(10 * Constants.ONE_WAD)) % uint96(core.getDssMaxSlashablePercentageWad(dss));
        // Make sure zero is not passed
        slashPercentageWad1 = slashPercentageWad1 == 0 ? slashPercentageWad1 : uint96(Constants.ONE_WAD);
        slashPercentagesWad[1] = slashPercentageWad1;

        vm.startPrank(address(dss));
        address[] memory operatorVaults = core.fetchVaultsStakedInDSS(operator, dss);

        SlasherLib.SlashRequest memory slashingReq = SlasherLib.SlashRequest({
            operator: operator,
            slashPercentagesWad: slashPercentagesWad,
            vaults: operatorVaults
        });
        SlasherLib.QueuedSlashing memory queuedSlashing = core.requestSlashing(slashingReq);
        vm.stopPrank();

        vm.warp(block.timestamp + elapsedTime);
        vm.prank(vetoCommittee);
        core.cancelSlashing(queuedSlashing);
    }
```

Here are successful test logs after running `forge test --match-test test_cancel_slashing_after_veto_window`:
```
Ran 1 test for test/core/slashing.t.sol:SlashingTests
[PASS] test_cancel_slashing_after_veto_window(uint96) (runs: 257, μ: 1599408, ~: 1599408)
Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 459.56ms (456.48ms CPU time)
```

Consider adding the following lines to `SlasherLib::cancelSlashing()` function:
```solidity
    if (queuedSlashing.timestamp + Constants.SLASHING_VETO_WINDOW <= block.timestamp) {
        revert;
    }
```