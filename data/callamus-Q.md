Core.sol only.
Issue1. 'registerOperatorToDSS' Does not check if the operator has already been registered to the dss.

In core.sol, the 'registerOperatorToDSS' function allows an operator to register to DSS. The function then checks if the DSS is registered but does not go ahead to check if the operator had already registered with the DSS.
https://github.com/code-423n4/2024-07-karak/blob/main/src/Core.sol#L97C1-L106C62
Operator can double register themselves with the DSS.
Impact
Inconsistent data in the storage such as during slashing assets.

Mitigations
Add checks to check if operator has already registered like :
if (self.isOperatorRegistered(dss, operator)) revert OperatorAlreadyRegistered();


Issue2.In 'unregisterOperatorFromDSS' Operator can unregister from DSS with pending asset delegations contrary to the documentation. 

In core.sol, unregisterOperatorFromDSS function,
https://github.com/code-423n4/2024-07-karak/blob/main/src/Core.sol#L109C1-L125C1
 The function allows operator to unregister from DSS. As per the documentattion, it requires all asset delegations to be 0 before operator unregisters. The function does not check if the assets are 0 before unregistering, it checks only if the operator is registered with the DSS the proceeds to unregister operator from DSS.
Impact
Operator can unregister from DSS with pending assets in the system.

Mitigation
Add checks to check if the asset delegations are zero before unregistering an operator.


issue3.'registerDSS' Does not check if the caller has already been registered as DSS as well as if the slashable percentage is non-zero.

https://github.com/code-423n4/2024-07-karak/blob/main/src/Core.sol#L258C1-L266C67
 In core.sol, 'registerDSS', the function allows caller to register as DSS. But this is only only when the caller is not a smart contract. The function does not check if the caller is already registered as DSS but 'expects' the contract to check if the operator is set by checking if the slashable percentage is non zero. Caller can reregister as DSS causing inconsistency in the storage.
Impact
inconsistent data stored by the protocol such as setting contradicting 'setDSSMaxSlashablePercentageWad' under one caller.
Mitigation 
Add checks to confirm if caller is already registered to DSS.