# QA Report - Karak Audit Contest | 17 July 2024 - 31 July 2024

---

# Executive summary

### Overview

|              |                                              |
| :----------- | :------------------------------------------- |
| Project Name | Karak Restaking                              |
| Repository   | https://github.com/code-423n4/2024-07-karak  |
| Website      | [Link](https://karak.network/)               |
| X            | [Link](https://x.com/Karak_Network)          |
| Methods      | Manual Review                                |
| Total nSLOC  | 1737 over 20 contracts                       |

---

---

# Findings Summary

| ID              | Title                                                                                              | Instances | Severity       |
| --------------- | -------------------------------------------------------------------------------------------------- | --------- | -------------- |
| [L-01](#L-01)   | Lack of zero address check for `_owner`,`_operator` parameters in `initialize` - `NativeVault.sol` | -         | _Low_          |
| [L-02](#L-02)   | Lack of Cooldown Period in operator registration/unregistration can lead to availability issues    | -         | _Low_          |
| [L-03](#L-03)   | `unregistrationHookData` parameter is passed unchecked to `unregisterOperatorFromDSS`              | -         | _Low_          |
| [NC-01](#NC-01) | Incorrect / Outdated Natspec in `NativeVault.sol`                                                  | -         | _Non Critical_ |
| [NC-02](#NC-02) | Incorrect / Outdated Natspec in `Vault.sol`                                                        | -         | _Non Critical_ |
| [NC-03](#NC-03) | Incorrect / Outdated Natspec in `SlashingHandler.sol`                                              | -         | _Non Critical_ |

---

---

# [L-01] Lack of zero address check for `_owner`,`_operator` parameters in `initialize` - `NativeVault.sol`

## GitHub Links

https://github.com/code-423n4/2023-10-brahma/blob/main/contracts/src/core/AddressProvider.sol#L77-L90
https://github.com/code-423n4/2023-10-brahma/blob/main/contracts/src/core/AddressProvider.sol#L97-L105

## Impact

- Contract may be initialized with a zero address owner or operator, leading to a loss of control over critical ownership functions or granting roles.
Similarly the operator parameter can be set to the zero address, leading to the inability to perform essential operator functions, such as managing
vault configurations or updating node implementations. 

## Vulnerability Details

The `NativeVault.initialize` function is responsible for initializing the `NativeVault` contract with critical parameters such as the contract owner and operator. However, the function lacks the neccessary input validation checks for the `_owner` and `_operator` parameters to prevent the use of invalid adresses.

```javascript
 function initialize(
        address _owner,
        address _operator,
        address _depositToken,
        string memory _name,
        string memory _symbol,
        bytes memory _extraData
    ) external initializer {
        _initializeOwner(_owner);
        __Pauser_init();

        if (_depositToken != Constants.DEAD_BEEF) revert DepositTokenNotAccepted();

        (address manager, address slashStore, address nodeImplementation) =
            abi.decode(_extraData, (address, address, address));

        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();
        _grantRoles(manager, Constants.MANAGER_ROLE);

        NativeVaultLib.Storage storage self = _state();
        VaultLib.Config storage config = _config();

        config.asset = _depositToken;
        config.name = _name;
        config.symbol = _symbol;
        config.decimals = 18;
        config.operator = _operator;
        config.extraData = _extraData;

        self.slashStore = slashStore;
        self.nodeImpl = nodeImplementation;

        emit NativeVaultInitialized(_owner, manager, _operator, slashStore);
    }
```

### Tools Used

- Manual Code Review

## Recommended Mitigation Steps

Add a validation check before `_initializeOwner` is called in the function to ensure that the parameters are not set to invalid addresses.

```jsx
if (_owner == address(0) || _operator == address(0)) revert ZeroAddress();
```

---

# [L-02] Lack of Cooldown Period in operator registration/unregistration can lead to availability issues

## Github Links

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L97-L107
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L113-L124

## Summary

```jsx
function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)
        external
        whenFunctionNotPaused(Constants.PAUSE_CORE_REGISTER_TO_DSS)
        nonReentrant
    {
        address operator = msg.sender;
        CoreLib.Storage storage self = _self();
        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();
        self.registerOperatorToDSS(dss, operator, registrationHookData);
        emit RegisteredOperatorToDSS(operator, address(dss));
    }
```

```jsx
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

Lack of cooldown period between within registration and unregistration to DSS functions:

In the current implementation, an operator can unregister from a DSS immediately after registering, without any cooldown period.

This lack of a cooldown period could potentially lead to various issues:

An operator could repeatedly register and unregister from a DSS in quick succession, potentially causing unnecessary state changes and increasing the gas consumption.

Malicious operators could exploit this to manipulate the system or disrupt the normal functioning of the protocol.

The absence of a cooldown period might not provide sufficient time for the DSS to perform necessary actions or validations related to the operator's registration.

## Recommended Mitigation Steps

Implement a cooldown period equal to the SLASHING WINDOW + SLASHING VETO WINDOW.

---

---

# [L-03] `unregistrationHookData` parameter is passed unchecked to `unregisterOperatorFromDSS`

## Github Links

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L113-L124
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/Operator.sol#L181-L203

## Summary / Impact

The `unregisterOperatorFromDSS` function in the Core contract receives the `unregistrationHookData` parameter from the external caller and passes it directly to the `unregisterOperatorFromDSS` function in the Operator library without any validation or sanitization. If the `unregistrationHookData` is not properly validated or sanitized, it could lead to potential vulnerabilities or unintended behavior in the subsequent code execution.

## Vulnerability Detail

The `unregisterOperatorFromDSS` function in the Core contract passes the `unregistrationHookData` parameter to the unregisterOperatorFromDSS function in the Operator library without any checks or validation. The Operator library then uses this data to call the unregistrationHook function on the DSS contract via the HookLib.callHookIfInterfaceImplemented function.

```jsx
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

```jsx
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

# [NC-01] Incorrect / Outdated Natspec in `NativeVault.sol`

## Github Links

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L206-L209
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L225-L227

## Summary

There are a few discrepancies in the `NativeVault.sol` natspec that are incorrect or outdated.

The `validateExpiredSnapshot` function's NatSpec comment mentions that it "Allows anyone to start a new snapshot if the last snapshot has expired." However, the function does not actually start a new snapshot; it only validates an expired snapshot and emits an event.

The `startWithdrawal` function's NatSpec comment states "Allows caller to start a withdrawal to withdraw ETH accrued on their NativeNode." It would be clearer to mention that the function also updates the `nodeOwnerToWithdrawAmount` mapping and performs some validations.

## Recommendation

Make the necessary updates to the documentation to the function operation accurately.

---

# [NC-02] Incorrect / Outdated Natspec in `Vault.sol`

## Github Links

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L190

## Summary

There is a minor discrepancy in the `slashAssets` function. NatSpec comment mentions that the function "Slash the assets in the vault by a certain amount portion to a slashing handler contract."

However, the code implementation calculates the `transferAmount` as the minimum of `totalAssets()` and `totalAssetsToSlash`, which may not always represent a "certain amount portion."

It would be more accurate to describe the behavior as slashing the assets up to the specified `totalAssetsToSlash` amount.

## Recommendation

Make the necessary updates to the documentation to reflect the function operation accurately.

---

# [NC-03] Incorrect / Outdated Natspec in `SlashingHandler.sol`

## Github Links

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/SlashingHandler.sol#L49

## Summary

There is a minor discrepancy in the natspec for the `handleSlashing` function. The NatSpec comment mentions "Pulls the assets form the vault and send them to address(0)." However, the code implementation transfers the assets to the `SlashingHandler` contract itself before sending them to address(0).

It would be more accurate to describe the behavior as transferring the assets from the caller to the `SlashingHandler` contract and then sending them to address(0).

## Recommendation

Make the necessary updates to the documentation to reflect the function operation accurately.

---
---

######

_Reference: Documentation Flow - https://docs.karak.network/protocol/v2/overview
