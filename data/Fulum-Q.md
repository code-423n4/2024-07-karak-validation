# [01] - DSS can slash a little amount even if maxSlashablePercentageWad is set for 0%

## Description

On the core contract, we have this [@dev comment](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L259):
```
    /// @dev If you want to have 0% slashing, set `maxSlashablePercentageWad` to `1` since 0 is used as a default flag for not set
```

Then, when `maxSlashablePercentageWad` is set to 1, the DSS's not supposed can slash the vault, but take a look at the [code](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/entities/SlasherLib.sol#L85-L91) which compute the slash amount : 

```solidity
    earmarkedStakes[i] = Math.mulDiv(
        slashingMetadata.slashPercentagesWad[i],
        IKarakBaseVault(slashingMetadata.vaults[i]).totalAssets(),
        Constants.MAX_SLASHING_PERCENT_WAD
    );
```

It uses the OpenZeppelin Math contract to make the `mulDiv` operation, on some test on Remix, I have this differents output:

```
Inputs:
    - slashPercentagesWad = 1
    - totalAssets() = 100000000000000000000000 (100,000 tokens with 18 decimals)
    - MAX_SLASHING_PERCENT_WAD = 100000000000000000000

Result: 1000
Inputs:
    - slashPercentagesWad = 1
    - totalAssets() = 100000000000000000000000000000 (200,000 tokens with 24 decimals (like YAM-V2))
    - MAX_SLASHING_PERCENT_WAD = 100000000000000000000

Result: 1000000000
```

We can see a very little amount can be slashed when the `totalAssets()` amount is sufficient.

Also if the result of the `Math.mulDiv()` is zero, the `requestSlashing()` function will not revert.

## Recommendations

Add a proper revert on `fetchEarmarkedStakes()` when the `slashPercentagesWad` is equal to 1

# [02] - Mistakes on @params for `initialize()` on `NativeVault`

## Description 

The [param](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeVault.sol#L45) description for the `initialize()` function forgot the `address manager` params :

```
    /// @param _extraData Serialized bytes consisting {address slashStore, address nodeImplementation}
    ...
    (address manager, address slashStore, address nodeImplementation) =
    abi.decode(_extraData, (address, address, address));
```

## Recommendations

Add the address manager: 
```
    /// @param _extraData Serialized bytes consisting {address manager, address slashStore, address nodeImplementation}
```

# [03] - No way to unallow an asset on the protocol 

## Description 

There is no way to unallow an asset on the protocol, it can be problematic, e.g :

- The team use `Core::allowlistAssets()` to allow the asset to be used for vaults creation on the protocol, the `assetSlashingHandlers` mapping set an address other than address(0) and this guarantee the asset is allowed on the protocol.
- After a while, a hack or a finding of a bad behavior happen for an allowed tokens.
- If the vault deployed with the concerned asset suffer from this event,we want to avoid the creation of new vaults with this token.
  
## Recommendations

Consider removing the asset of the `assetSlashingHandlers` by setting the `slashingHandler` to address(0). You can also add a way to blacklist a token address but it invoke more modifications on the codebase.


# [04] - At the beginning of a node creation, user can register a validator with old balance. 

## Description 

We can note that the `NativeNode` address is created on the `NativeVault` contract with CREATE2 method and therefore its a predeterministic adress which can be computed before.

Now imagine this scenario:

A user named Bob have a validator which point his withdrawal address to the `NativeNode` pre-computed address when he have a big balance of ETH on it. A proof is now available at a point of time with a big balance of ETH on it. A valid proof and potential input on `validateWithdrawalCredentials()` is created.

After a long time Bob have a very lower balance on his validator, he decide to now `createNode()` and the `NativeNode` contract is created. When a `NativeNode` is created with `createNode()` on a `NativeVault`, the storage variables `lastSnapshotTimestamp` and `currentSnapshotTimestamp` are equals to zero.

On `validateWithdrawalCredentials()` function, we can see this check: 
```solidity
    if (
        beaconStateRootProof.timestamp < node.lastSnapshotTimestamp
            || beaconStateRootProof.timestamp < node.currentSnapshotTimestamp
    ) revert BeaconTimestampTooOld();
```

Because of his lack of verifications and the not accurated state of theses 2 variables, now the user can insert an old valid proof of the validator state and mint more shares than he is entitled to on the `NativeVault`. Before the user or anyone create a snapshot in the `NativeVault`, the amount of shares minted and state are not correct and can lead to potentials miscomputations of user balance, e.g on a DSS.
Undeniably it broke the correctness of the minting/burning computations for others users on the `NativeVault` during time before the first snapshot is completed.

It's not very useful imo, but if a user is also the operator he can potentially abuse?
If user set the slashStore at the address he want, he can get stay on the control of his ETH even if he is slashed by the protocol.

## Recommendations

The problem can be mitigate in two solutions:
    - In verifying in `validateWithdrawalCredentials()` functions that the proof timestamp is quite recent (less than 2 days for example) to guarantee adding a validator with an accurate state.
    - Verify `lastSnapshotTimestamp` is not equal to `0`, this force the user to create one snapshot to use the `validateWithdrawalCredentials()` function.

