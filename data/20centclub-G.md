# GAS-1. Unused variable in `NativeNode` contract.

## Description

The nodeOwner storage variable is declared and initialized in the `NativeNode` contract within the initialize function. However, it is not used anywhere else in the contract. Additionally, because the default visibility for storage variables in Solidity is internal, the variable cannot be accessed outside of the contract.

## Code snippet

```
    address nodeOwner; 

    function initialize(address _owner, address _nodeOwner) external initializer {
        _initializeOwner(_owner);
        __Pauser_init();

        nodeOwner = _nodeOwner;
    }
```

## Recomendetion

Consider removing the unused variable to optimize gas usage. If the variable is intended to be accessed externally, change its visibility to public to allow access from outside the contract.

# GAS-2. Storing redundant data in VaultLib.Confi

## Description

In the `initialize` function of the `NativeVault` contract, the `_extraData` is decoded, and all decoded variables (such as `manager`, `slashStore`, `nodeImplementation`) are stored in storage. However, the `_extraData` itself is also stored in `config.extraData`, which results in redundancy.

## Code snippet

```
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

## Recomendetion

Remove the redundtant data stored in storage variable config.

# GAS-3. storage variable can be set as memory

## Description

In the function `validateWithdrawalCredentials`, the variable `self` is marked as a storage variable. However, there are no modifications made to this variable within the function. Therefore, it can be declared as a `memory` variable instead, which can help optimize gas usage.

## Code snippet

```
    function validateWithdrawalCredentials(
        address nodeOwner,
        BeaconProofs.BeaconStateRootProof calldata beaconStateRootProof,
        BeaconProofs.ValidatorFieldsProof[] calldata validatorFieldsProofs
    )
        external
        nonReentrant
        nodeExists(nodeOwner)
        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_VALIDATE_WITHDRAW_CREDS)
    {
        NativeVaultLib.Storage storage self = _state();
        NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner];


        if (beaconStateRootProof.timestamp == block.timestamp) {
            revert BeaconTimestampIsCurrent();
        }
        if (
            beaconStateRootProof.timestamp < node.lastSnapshotTimestamp
                || beaconStateRootProof.timestamp < node.currentSnapshotTimestamp
        ) revert BeaconTimestampTooOld();


        uint256 totalRestakedWei;
        BeaconProofs.validateBeaconStateRootProof(
            _getParentBlockRoot(beaconStateRootProof.timestamp), beaconStateRootProof
        );


        for (uint256 i = 0; i < validatorFieldsProofs.length; i++) {
            totalRestakedWei += self.validateWithdrawalCredentials(
                nodeOwner,
                beaconStateRootProof.timestamp,
                beaconStateRootProof.beaconStateRoot,
                validatorFieldsProofs[i]
            );
        }


        _increaseBalance(nodeOwner, totalRestakedWei);
    }
```

## Recomendetion

Change the variable `self` from `storage` to `memory` to reflect its usage correctly and potentially reduce gas costs.