[QA-01] Visibility Mismatch in CommonUtils Library Functions
## Vulnerability Detail:
In the `CommonUtils` library, there is a visibility mismatch between the `hasDuplicates` function and the `sortArr` function it attempts to call. Specifically, `hasDuplicates` is declared as `external`, while `sortArr` is marked as `private`. According to Solidity's visibility rules, `private` functions cannot be called from `external` functions. This discrepancy prevents the `hasDuplicates` function from executing as intended, as it requires calling `sortArr` to sort the array before checking for duplicates.

## Impact
It prevents the `hasDuplicates` function from performing its intended task of checking an array of addresses for duplicates. Since `hasDuplicates` relies on `sortArr` to sort the array, the inability to call `sortArr` due to its private visibility means that the function cannot accurately determine if the array contains duplicate addresses. This could lead to incorrect results in any logic that relies on this information, potentially affecting decision-making processes within the contract or application.

## Recommendation:
- Adjust the Visibility of `sortArr`: Change the visibility of sortArr from private to internal. This adjustment allows hasDuplicates to call `sortArr` without violating Solidity's visibility rules, enabling the function to sort the array and correctly check for duplicates.
```
function sortArr(address[] memory arr) internal pure {
    ...
}
```
[QA-02] Unsafe call to `.decimals`
## Vulnerability Detail
The `Vault` contract relies on the `.decimals()` function to determine the number of decimal places a token uses, which is crucial for accurately calculating token amounts and managing stakes. However, not all ERC20 tokens implement this function, leading to potential compatibility issues.
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L278-L279

```solidity
        return _config().decimals;
```
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L317-L318

```solidity
        return _config().decimals;
```
## Impact
When the contract attempts to call `.decimals()` on a token that does not support it, the call will fail, resulting in a runtime error.
## Recommendation
Consider using a helper function to prevent this

[QA-03] Improper Role Assignment Due to Lack of Input Validation
## Vulnerability Detail
The `initialize` function grants roles to the `_manager` and `_vetoCommittee` addresses without performing any input validation. Specifically, it does not check if these addresses are non-zero before attempting to assign them roles via the `_grantRoles` function. 
https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L64-L66

```solidity
        _grantRoles(_manager, Constants.MANAGER_ROLE);
        _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);
```
## Impact
Granting roles to the zero address `(0x000...000)` would effectively remove those roles from the contract, as the zero address cannot execute any actions. This could render the contract unusable if critical roles are assigned to the zero address.
## Recommendation
Before calling `_grantRoles`, validate that `_manager` and `_vetoCommittee` are non-zero addresses
```
require(_manager != address(0), "Manager address cannot be zero");
require(_vetoCommittee != address(0), "Veto Committee address cannot be zero");
```