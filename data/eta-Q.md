# Repeated unregisterOperatorFromDSS() calls
## Impact

The `unregisterOperatorFromDSS()` function can be invoked multiple times by a operator, leading to redundant `UnregisteredOperatorToDSS()` events and unnecessary calls to the DSS's beforeUnregistrationHook()`. This could potentially trigger unintended consequences. 

## Recommended Mitigation Steps

To mitigate this issue, implement a check within the `unregisterOperatorFromDSS()` function to verify if the operator is already unregistered. This will prevent duplicate unregistrations and subsequent redundant actions. 

[Core::unregisterOperatorFromDSS](https://github.com/code-423n4/2024-07-karak/blob/a9658bccc884eb72538875c3940c6b507e06d4ca/src/Core.sol#L113C1-L124C6)
```solidity
    function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_CORE_UNREGISTER_FROM_DSS)
    {
        address operator = msg.sender;
require(isOperatorRegisteredToDSS(operator, dss));
        CoreLib.Storage storage self = _self();
        self.checkIfOperatorIsRegInRegDSS(operator, dss);
        self.unregisterOperatorFromDSS(dss, operator, unregistrationHookData);

        emit UnregisteredOperatorToDSS(operator, address(dss));
    }

```