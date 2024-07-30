# 1. Missing DSS Unregistration Function in Core.sol

## Description

The Core.sol contract currently lacks a function that allows DSS (Decentralized Staking Systems) to unregister. This absence makes it challenging for operators to determine if a DSS is active, especially since the rewards are not tracked on-chain.

## Recommendation

Include a function that enables DSS to unregister from the system. This will help operators identify inactive DSS more easily and manage their participation accordingly.

```solidity
function unregisterDSS(uint256 maxSlashablePercentageWad) external {
        IDSS dss = IDSS(msg.sender);
        if (!address(dss).isSmartContract()) revert NotSmartContract();
        if (getDssMaxSlashablePercentageWad(dss) == 0 ) revert NotDSS();
        _self().unSetDSSMaxSlashablePercentageWad(dss);
        emit DSSRegistered(msg.sender, maxSlashablePercentageWad);
    }

function unSetDSSMaxSlashablePercentageWad(
        CoreLib.Storage storage self,
        IDSS dss,
        uint256 dssMaxSlashablePercentageWad
    ) public {
        uint256 currentSlashablePercentageWad = self.dssMaxSlashablePercentageWad[dss];
        if (currentSlashablePercentageWad == 0) revert DSSIsNotPresent();
        self.dssMaxSlashablePercentageWad[dss] = 0;
    }

```

# 2.Missing Validation in Vault Staking/Unstaking Process in Core.sol

## Impact
The lack of a check in the `requestUpdateVaultStakeInDSS()` function to verify whether a vault is already staked in a DSS can lead to inefficient operations and potential errors. Without this check, an operator might mistakenly initiate an unstaking request for a vault that is not actually staked in the DSS, causing unnecessary waiting periods.

This oversight could result in delays in the system, as the operator must wait the full unstaking period (9 days) before the `finalizeUpdateVaultStakeInDSS()` function is called. Which then basically just deletes the `pendingStakeUpdate`

## Proof of Concept

[Code of requestUpdateVaultStakeInDSS()](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L130)

## Tools Used
Manual Review

## Recommended Mitigation Steps

To address this issue, add a verification step in the requestUpdateVaultStakeInDSS() function. If the toStake parameter is false (indicating an unstaking request), the function should check if the vault is currently staked in the specified DSS. If the vault is not staked, the function should revert the transaction to prevent unnecessary operations and waiting periods. This ensures that only valid unstaking requests are processed


```diff
function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_STAKE_UPDATE)
        returns (Operator.QueuedStakeUpdate memory updatedStake)
    {
        address operator = msg.sender;
        CoreLib.Storage storage self = _self();
        self.checkIfOperatorIsRegInRegDSS(operator, vaultStakeUpdateRequest.dss);
+       if(vaultStakeUpdateRequest.toStake){
+         //Check if the vault is already staked in the DSS
+         ...
+       }else{
+         //Check if the vault is not staked in the DSS
+         ...
+       }
        updatedStake = self.requestUpdateVaultStakeInDSS(vaultStakeUpdateRequest, self.nonce++, operator);
        emit RequestedStakeUpdate(updatedStake);
    }
``` 


# 3. Missing Proper Validation in `addVault()` Function in Operator.sol

## Impact
The addVault() function in the Core.sol contract is used to add a vault to the operator's state. However, it lacks proper validation for the maximum capacity of vaults. 

## Recommendation 

System is using ``` operatorState.vaults.length() == Constants.MAX_VAULTS_PER_OPERATOR``` But instead should use ``` if (operatorState.vaults.length() >= Constants.MAX_VAULTS_PER_OPERATOR) revert MaxVaultCapacityReached();
``` for more safety.

# 4. No checking for create2 deployed contract for creating Node correctly

## Impact

In the `deployNode()` function, a new node is deployed using a deterministic ERC1967 beacon proxy. While the function includes an initialization step for the newly deployed node, it does not perform any checks to ensure that the deployemnt was successful. This could lead to issues if the node fails to deploy correctly, potentially causing vulnerabilities. We are checking this while deploying the vaults. Add the extra check while deploying the Node also.

## Code 

```solidity
function deployNode(Storage storage self, VaultLib.Config storage config, address owner)
        internal
        returns (address)
    {
        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));

        INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));
        newNode.initialize(address(this), owner); //@audit - while deploying the vault we are checking that it must be deployed correctly but why not checking for node deployment?

        emit NodeDeployed(msg.sender, address(newNode), self.nodeImpl);
        return address(newNode);
    }

```

## Recommendation

`createVault()` has the check ```
if (expectedNewVaultAddr != address(vault)) {
            revert VaultCreationFailedAddrMismatch(expectedNewVaultAddr, address(vault));
        }
```
Add the similar check for the `deployNode()` Function.

