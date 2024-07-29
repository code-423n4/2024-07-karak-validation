# supportsInterfaceGasLimit and hookGasBuffer variables do not have size limits

## Impact

https://github.com/code-423n4/2024-07-karak/blob/main/src/entities/HookLib.sol#L78

The problem occurs in the `HookLib, Core, CoreLib` contract. In the `callHookIfInterfaceImplemented` function of the HookLib contract, the supportsInterfaceGasLimit and hookGasBuffer variables are used to check whether the remaining gas is sufficient. The supportsInterfaceGasLimit and hookGasBuffer variables are mainly set by privileged roles. However, there is no size limit for the supportsInterfaceGasLimit and hookGasBuffer variables, which may cause the following effects:

1. If the supportsInterfaceGasLimit variable here is equal to zero, no matter what the value of gasleft() is, all gas sufficiency checks will fail.
2. If the supportsInterfaceGasLimit variable is extremely large and hookGasBuffer is extremely small, this will cause the defined Gas value to be extremely large, which may eventually lead to all gas being insufficient, unless gasleft() is an extremely large value, but this will waste a lot of Gas.

## Proof of Concept

Vulnerability in callHookIfInterfaceImplemented function: Multiple values ​​in callHookIfInterfaceImplemented function are not restricted.

```solidity
    function callHookIfInterfaceImplemented(
        IERC165 dss,
        bytes memory data,
        bytes4 interfaceId,
        bool ignoreFailure,
        uint32 hookCallGasLimit,
        uint32 supportsInterfaceGasLimit,
        uint32 hookGasBuffer
    ) internal returns (bool) {

        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {
            revert NotEnoughGas();
        }
        (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(
            address(dss),
            abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId),
            supportsInterfaceGasLimit 
        );

        if (!success || result == bytes32(0)) {
            // Either call failed or interface isn't implemented
            emit InterfaceNotSupported();
            return false;
        }
        return callHook(address(dss), data, ignoreFailure, hookCallGasLimit, hookGasBuffer);
    }
```

## Tools Used

Remix IDE

## Recommended Mitigation Steps

Limit the value of the GasValues ​​variable to avoid large or small values ​​that may cause the contract logic to fail to execute normally.


# Undetermined addresses are not the same

## Impact

https://github.com/code-423n4/2024-07-karak/blob/main/src/NativeVault.sol#L62

Failure to verify that the address is unique when the NativeVault contract is initialized may lead to potential confusion of permissions and security risks. For example, if the `manager` and `slashStore` addresses are the same, too many permissions and functions may be granted to a single address, increasing the risk of malicious behavior. This may lead to abuse of management permissions and even threaten the funds in the contract.

## Proof of Concept

Vulnerability in initialize function: manager, slashStore, nodeImplementation may have the same address.

```solidity
if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();
```

## Tools Used

Remix IDE

## Recommended Mitigation Steps

Add additional checks to ensure `manager`, `slashStore` and `nodeImplementation` addresses are unique.