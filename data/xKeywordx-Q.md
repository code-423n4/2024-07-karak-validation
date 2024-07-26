### [L-1] `EOAs` can register as `Operators`

**Description:** Based on the official docs [v2](https://docs.karak.network/protocol/v2/operators) I wasn't able to find any explicit reference about what an `Operator` should or shouldn't be. Based on the complexity of the protocol and the fact that the `Operator` needs to fulfill tasks for a `DSS` it seems that it would be better if `Operators` are smart contracts instead of `EOAs`, but the code doesn't enforce it. I am submitting this as a `Low/Info` finding because I am unsure if this is the intended design of the protocol or not. If this is not the intended design, I think this should be a Medium severity finding.

**Impact:** I wasn't able to identify any issue in the protocol based on the current implementation if the address of an `Operator` would be an `EOA` instead of a smart contract, but we are lacking context over what a `task` coming from a `DSS` looks like. If sponsors deem that `EOAs` can manage and fulfill tasks like a smart contract would do, then there shouldn't be any problems.

**Proof of Concepts:** Input the test below in the `operatorDSS.t.sol` file.

<summary>PoC - Click the arrow below</summary>
<details>

```javascript
    function test_aliceRegister_operator_to_DSS() public {
        address alice = makeAddr("alice");
        vm.startPrank(alice);
        core.registerOperatorToDSS(dss, "");
        vm.stopPrank();
        assertTrue(core.isOperatorRegisteredToDSS(alice, dss));
    }

```

Test output

```javascript
@>  ├─ [4185] TransparentUpgradeableProxy::isOperatorRegisteredToDSS(alice: [0x328809Bc894f92807417D2dAD6b7C998c1aFdac6], MockDSS: [0x0Da75B8A871Aca5398ec218479f2B297E36D75D6]) [staticcall]
@>  │   ├─ [3207] Core::isOperatorRegisteredToDSS(alice: [0x328809Bc894f92807417D2dAD6b7C998c1aFdac6], MockDSS: [0x0Da75B8A871Aca5398ec218479f2B297E36D75D6]) [delegatecall]
    │   │   └─ ← [Return] true
    │   └─ ← [Return] true
    ├─ [0] VM::assertTrue(true) [staticcall]
    │   └─ ← [Return]
    └─ ← [Return]

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 22.55ms (2.19ms CPU time)
```

</details>

**Recommended mitigation:** If this is not the intended design, I recommend adding the `isSmartContract()` check on the `Core::registerOperatorToDSS` function.