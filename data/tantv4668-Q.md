# Duplicate the logic in the Core contract's *unregisterOperatorFromDSS()* function.
## Description 
This function calls:
- *checkIfOperatorIsRegInRegDSS()* function of Operator library.
- *unregisterOperatorFromDSS()* function of Operator library.
```
    function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_CORE_UNREGISTER_FROM_DSS)
    {
        address operator = msg.sender;
        CoreLib.Storage storage self = _self();
        self.checkIfOperatorIsRegInRegDSS(operator, dss);
        self.unregisterOperatorFromDSS(dss, operator, unregistrationHookData);

        emit UnregisteredOperatorToDSS(operator, address(dss));
    }
```

The *checkIfOperatorIsRegInRegDSS()* function calls the *isOperatorRegisteredToDSS()* function.
```
    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {
        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();
        if (!isOperatorRegisteredToDSS(self, operator, dss)) {
            revert OperatorNotValidatingForDSS();
        }
    }
```

But the *unregisterOperatorFromDSS()* function of the Operator library calls *isOperatorRegisteredToDSS()* again.
```
     function unregisterOperatorFromDSS(
        CoreLib.Storage storage self,
        IDSS dss,
        address operator,
        bytes memory unregistrationHookData
    ) external {
        State storage operatorState = self.operatorState[operator];
        // Checks if all operator delegations are zero
        address[] memory vaults = getVaultsStakedToDSS(operatorState, dss);
        if (vaults.length != 0) revert AllVaultsNotUnstakedFromDSS();
        if (!isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorNotValidatingForDSS();

        self.operatorState[operator].dssMap.remove(address(dss));
        HookLib.callHookIfInterfaceImplemented({
            dss: dss,
            data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData),
            interfaceId: dss.unregistrationHook.selector,
            ignoreFailure: true, // So it can't prevent the operator from unregistering
            hookCallGasLimit: self.hookCallGasLimit,
            supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
            hookGasBuffer: self.hookGasBuffer
        });
    }
```
## Recommendation
Remove the call to *isOperatorRegisteredToDSS()* function in the *unregisterOperatorFromDSS()* function.