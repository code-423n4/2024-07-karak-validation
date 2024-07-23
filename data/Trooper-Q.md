# L-01 Misleading NatSpec

In the NatSpec of the `getLeverage` function in Core.sol, the description states that a "vault allocates its entire balance to every vault" [here](https://github.com/code-423n4/2024-07-karak/blob/a9658bccc884eb72538875c3940c6b507e06d4ca/src/Core.sol#L345). This is incorrect and should be corrected to "vault allocates its entire balance to every __DSS__"


# L-02 NatSpec does not match the implementation

```
    /// @notice Initializes the vault
...
    /// @param _depositToken Disregarded for NativeVault. Can be address(0).
...
    function initialize(...) external initializer {
...
        if (_depositToken != Constants.DEAD_BEEF) revert DepositTokenNotAccepted();
```
The NatSpec of the `initialize` function in NativeVault.sol states that "@param _depositToken Disregarded for NativeVault. Can be address(0)." [here](https://github.com/code-423n4/2024-07-karak/blob/a9658bccc884eb72538875c3940c6b507e06d4ca/src/NativeVault.sol#L42). This does not match the implementation of that function. It requires that the _depositToken equals the constants "DEAD_BEEF".
Assuming the code was updated later and is correct: The NatSpec should be updated to say that _depositToken MUST be the DEAD_BEEF address (0xDeaDbeefdEAdbeefdEadbEEFdeadbeEFdEaDbeeF).


# L-03 NatSpec does not match the implementation

```
    /// @notice Initializes the vault
...
    /// @param _extraData Serialized bytes consisting {address slashStore, address nodeImplementation}
...
    function initialize(...) external initializer {
...
        (address manager, address slashStore, address nodeImplementation) =
            abi.decode(_extraData, (address, address, address));
```
The NatSpec of the `initialize` function in NativeVault.sol states that "@param _extraData Serialized bytes consisting {address slashStore, address nodeImplementation}" [here](https://github.com/code-423n4/2024-07-karak/blob/a9658bccc884eb72538875c3940c6b507e06d4ca/src/NativeVault.sol#L45). This does not match the implementation of that function.
It decodes the `_extraData` as addresses for manager, slashStore and nodeImplementation. Assuming the code was updated later and is correct: The NatSpec should be correct to represent those changes to make sure the correct parameters are passed.


# L-04 Wrong NatSpec or wrong access rights

The NatSpec of the `changeNodeImplementation` function in NativeVault.sol states that "@notice Allows the owner to change the NativeNode implementation and upgrade all NativeNodes" [here](https://github.com/code-423n4/2024-07-karak/blob/a9658bccc884eb72538875c3940c6b507e06d4ca/src/NativeVault.sol#L81). This does not match the implementation of that function.
The modifier `onlyOwnerOrRoles(Constants.MANAGER_ROLE)` allows the owner and managers to update the contract implementation. Either the NatSpec or the access rights should be adjusted. It should also be noted that per documentation the manager role is intended as "MANAGER - mostly day to day operations, could be multisig or EOA" [source](https://code4rena.com/audits/2024-07-karak-restaking#toc-2-all-trusted-roles-in-the-protocol). Changing the vault implementation is arguably a more serious actions and should possibly be limited to the owner.


# L-05 Wrong NatSpec or wrong access rights

The NatSpec of the `allowlistAssets` function in Core.sol states that "@notice Allows the manager to allowlist assets that then vaults can be created for with the asset as the underlying token." [here](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Core.sol#L82). This does not match the implementation of that function.
The modifier `onlyOwnerOrRoles(Constants.MANAGER_ROLE)` allows the owner and managers to update the contract implementation. Either the NatSpec or the access rights should be adjusted. It should also be noted that per documentation the manager role is intended as "MANAGER - mostly day to day operations, could be multisig or EOA" [source](https://code4rena.com/audits/2024-07-karak-restaking#toc-2-all-trusted-roles-in-the-protocol). Adjusting the allowlist of the assets could be considered a more serious actions and should maybe be limited to the owner.