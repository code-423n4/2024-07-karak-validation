### Cache Local Variable Array Length In For Loop
If not cached, the solidity compiler will always read the length of the array during each iteration. If it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

```solidity
Path: ./src/Querier.sol

29:        for (uint256 i = 0; i < stakedVaults.length; i++) {	// @audit-issue

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue

39:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L29-L29), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L39-L39), 


```solidity
Path: ./src/SlashingHandler.sol

36:        for (uint256 i = 0; i < _supportedAssets.length; i++) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L36-L36), 


```solidity
Path: ./src/NativeVault.sol

144:        for (uint256 i = 0; i < balanceProofs.length; i++) {	// @audit-issue

194:        for (uint256 i = 0; i < validatorFieldsProofs.length; i++) {	// @audit-issue
```
[144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L144-L144), [194](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L194-L194), 


```solidity
Path: ./src/entities/Operator.sol

232:        for (uint256 i = 0; i < dssAddresses.length; i++) {	// @audit-issue
```
[232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L232-L232), 


```solidity
Path: ./src/entities/CoreLib.sol

71:        for (uint256 i = 0; i < assets.length; i++) {	// @audit-issue

84:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue

132:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L71-L71), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L84-L84), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L132-L132), 


```solidity
Path: ./src/entities/SlasherLib.sol

50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {	// @audit-issue

85:        for (uint256 i = 0; i < slashingMetadata.vaults.length; ++i) {	// @audit-issue

134:        for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L50-L50), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L85-L85), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L134-L134), 


```solidity
Path: ./src/entities/MerkleProofs.sol

55:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

113:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L55-L55), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L113-L113), 


#### Recommendation

To optimize gas consumption, cache the length of memory arrays before for loop iterations in Solidity. This reduces redundant mload operations, saving 3 gas per iteration after the first and improving overall contract efficiency.

### Another Constant With Same Value Is Already Defined
Defining multiple constants with the same value in a Solidity contract introduces unnecessary redundancy and can lead to confusion and potential errors in contract maintenance. Constants are used to define values that remain unchanged throughout the contract's lifecycle, enhancing readability and efficiency. However, when multiple constants representing the same value are defined, it not only clutters the code but also complicates the process of updating values and understanding the contract's logic. Consolidating these constants into a single definition improves code clarity and maintainability.

```solidity
Path: ./src/entities/BeaconProofsLib.sol

11:    uint256 internal constant BEACON_BLOCK_HEADER_HEIGHT = 3;	// @audit-issue: Same value `3` is already defined on line `10` as variable: `BEACON_STATE_ROOT_IDX`
```
[11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L11-L11), 


#### Recommendation

Identify and consolidate duplicate constants in your Solidity contracts. Examine your contract's constants to find any with identical values and refactor your code to use a single constant definition for each unique value. This may involve choosing the most descriptive and appropriate name for the consolidated constant and updating all references accordingly. Such consolidation not only makes your contract more concise and easier to read but also simplifies future updates to constant values. Document the purpose and usage of each constant clearly, ensuring that the chosen names accurately reflect their role within the contract.

### Unnecessary Variable Initialization
In programming, it's a common practice to declare and initialize variables that will be used later in the code. However, if after declaration, the variable is not used anywhere else in the code, this leads to unnecessary variable initialization. In the context of Solidity and smart contracts, where gas efficiency is paramount, such redundant initializations not only consume extra gas but also clutter the codebase, making it less readable and harder to maintain.

Variables that are declared but never used represent dead code. They take up space in the bytecode, result in wasted gas when the contract is deployed, and can be confusing for anyone reading or auditing the code.


```solidity
Path: ./src/Querier.sol

38:        uint256 latestIndex = 0;	// @audit-issue
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L38-L38), 


#### Recommendation

To avoid unnecessary variable initialization in Solidity code, regularly review and remove unused variables, use meaningful variable names, and avoid overly defensive coding. Prioritize gas efficiency and rigorous testing to maintain clean and efficient code.

### Unnecessary casting as variable is already of the same type
In Solidity, explicitly casting a variable to a type that it already represents is redundant and can lead to confusion and clutter in the code. This unnecessary casting doesn't typically consume additional gas since Solidity's optimizer often removes such redundant conversions during compilation. However, it does affect code readability and may obscure the actual intent of the code, making it harder for developers to understand and maintain. Ensuring that casting is used only when necessary helps maintain clean, clear, and efficient code.

```solidity
Path: ./src/Vault.sol

62:        (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));	// @audit-issue: Variable `_depositToken` is converted to `address` from type `address`.
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L62-L62), 


```solidity
Path: ./src/entities/CoreLib.sol

104:        self.vaultToImplMap[address(expectedNewVaultAddr)] = implementation;	// @audit-issue: Variable `expectedNewVaultAddr` is converted to `address` from type `address`.
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L104-L104), 


#### Recommendation

Review your Solidity code for instances of unnecessary casting where variables are cast to their own type. Remove these redundant casts to enhance code clarity and maintainability. When writing new code, ensure that casting is only applied when changing a variable's type is genuinely needed. This practice helps in keeping the codebase straightforward and understandable, reducing potential confusion and errors associated with misinterpreting the variable types.

### Same cast is done multiple times
It's cheaper to do it once, and store the result to a variable.

```solidity
Path: ./src/SlashingHandler.sol

56:        SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount);	// @audit-issue: Same casting also done in line(s): `[58]`.
```
[56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L56-L56), 


```solidity
Path: ./src/NativeVault.sol

464:            parentBeaconBlockRoot: _getParentBlockRoot(uint64(block.timestamp)),	// @audit-issue: Same casting also done in line(s): `[473, 470]`.
```
[464](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L464-L464), 


```solidity
Path: ./src/entities/CoreLib.sol

114:        emit NewVault(address(vault), implementation);	// @audit-issue: Same casting also done in line(s): `[110, 111]`.
```
[114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L114-L114), 


```solidity
Path: ./src/entities/HookLib.sol

92:            address(dss),	// @audit-issue: Same casting also done in line(s): `[102]`.
```
[92](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L92-L92), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

102:        emit NodeDeployed(msg.sender, address(newNode), self.nodeImpl);	// @audit-issue: Same casting also done in line(s): `[103]`.
```
[102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L102-L102), 


#### Recommendation

Identify instances in your Solidity contracts where the same value is cast to another type multiple times. Refactor these operations by performing the cast once and storing the result in a local variable. Use this variable for all subsequent operations requiring the cast value.

### `address(this)` should be cached
Cacheing saves gas when compared to repeating the calculation at each point it is used in the contract.

```solidity
Path: ./src/Vault.sol

175:            owner: address(this),	// @audit-issue: `adress(this)` also used on line(s): [173, 167]
```
[175](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L175-L175), 


```solidity
Path: ./src/entities/CoreLib.sol

102:            LibClone.predictDeterministicAddressERC1967BeaconProxy(address(this), salt, address(this));	// @audit-issue: `adress(this)` also used on line(s): [107]
```
[102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L102-L102), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

99:        INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue: `adress(this)` also used on line(s): [100]
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L99-L99), 


#### Recommendation

To enhance gas efficiency, cache the contract's address by storing `address(this)` in a state variable at the point of contract deployment or initialization. Use this cached address throughout the contract instead of repeatedly calling `address(this)`. This practice reduces the gas cost associated with multiple computations of the contract's address, leading to more efficient contract execution, especially in scenarios with frequent usage of the contract's address.

### Superfluous event fields
`block.number` and `block.timestamp` are added to the event information by default, so adding them manually will waste additional gas.

```solidity
Path: ./src/NativeVault.sol

473:        emit SnapshotCreated(nodeOwner, node.nodeAddress, uint64(block.timestamp), snapshot.parentBeaconBlockRoot);	// @audit-issue
```
[473](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L473-L473), 


#### Recommendation

Review your smart contracts to identify and remove `block.number` and `block.timestamp` from the parameters of emitted events. Instead of manually adding these fields, rely on the Ethereum blockchain's inherent inclusion of this information within the block context. Simplify your event definitions to include only the essential data specific to the event's purpose, excluding universally available block metadata.

### Unnecessary Event Emitting
Emitting two events in the same function with exactly the same event parameters is redundant and can lead to unnecessary gas consumption, as each `emit` operation adds to the transaction cost. These events can be merged into a single event to streamline contract operations and reduce gas usage, making the smart contract more efficient and cost-effective to interact with. This approach not only optimizes gas costs but also simplifies the contract's event logic for developers and applications integrating with the contract.

```solidity
Path: ./src/entities/HookLib.sol

62:        else emit HookCallFailed(returnData);	// @audit-issue: Exactly same parameters in event emitting also used on line(s): `[61]`
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L62-L62), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

135:        emit SnapshotValidator(nodeOwner, nodeAddress, timestamp, validatorIndex);	// @audit-issue: Exactly same parameters in event emitting also used on line(s): `[131]`
```
[135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L135-L135), 


#### Recommendation

Your code can be optimized with changing the usage:
```solidity
emit SaleEnded(timestamp);
emit ClaimStarted(timestamp);
```
To
```solidity
emit SaleEndedAndClaimStarted(timestamp); // Declare general one and remove old ones.
```


### Revert String Size Optimization
Shortening the revert strings to fit within 32 bytes will decrease deployment time and decrease runtime Gas when the revert condition is met.

Revert strings that are longer than 32 bytes require at least one additional `mstore`, along with additional overhead to calculate memory offset, etc.



```solidity
Path: ./src/entities/MerkleProofs.sol

53:        require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32");	// @audit-issue: String length is `75`

108:        require(	// @audit-issue: String length is `84`
109:            proof.length != 0 && proof.length % 32 == 0,
110:            "Merkle.processInclusionProofSha256: proof length should be a non-zero multiple of 32"
111:        );
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L53-L53), [108](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L108-L111), 


#### Recommendation


To optimize Gas usage in your Solidity contract, it is recommended to keep revert strings as short as possible and to ensure that they fit within 32 bytes. It is possible to use abbreviations or simplified error messages to keep the string length short. Doing so can reduce the amount of Gas used during deployment and runtime when the revert condition is met.


### Custom Errors in Solidity for Gas Efficiency
Starting from Solidity version 0.8.4, the language introduced a feature known as "custom errors". These custom errors provide a way for developers to define more descriptive and semantically meaningful error conditions without relying on string messages. Prior to this version, developers often used the `require` statement with string error messages to handle specific conditions or validations. However, every unique string used as a revert reason consumes gas, making transactions more expensive.

Custom errors, on the other hand, are identified by their name and the types of their parameters only, and they do not have the overhead of string storage. This means that, when using custom errors instead of `require` statements with string messages, the gas consumption can be significantly reduced, leading to more gas-efficient contracts.

```solidity
Path: ./src/entities/MerkleProofs.sol

53:        require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32");	// @audit-issue

108:        require(	// @audit-issue
109:            proof.length != 0 && proof.length % 32 == 0,
110:            "Merkle.processInclusionProofSha256: proof length should be a non-zero multiple of 32"
111:        );
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L53-L53), [108](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L108-L111), 


#### Recommendation


It is recommended to use custom errors instead of revert strings to reduce gas costs, especially during contract deployment. Custom errors can be defined using the error keyword and can include dynamic information.

### Avoid repeating computations
In Solidity development, repeating the same computations within a contract can lead to unnecessary gas consumption and reduce the contract's efficiency. This is particularly relevant in functions that are called frequently or involve complex calculations. Repeating computations not only wastes computational resources but also increases the cost of executing transactions. By identifying and eliminating redundant calculations, developers can optimize contract performance, reduce gas costs, and improve overall execution speed.

```solidity
Path: ./src/Querier.sol

35:            if (results[i] != bytes32(0)) count++;	// @audit-issue: Same binary operation statement in line(s) between: ['40:40']

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue: Same binary operation statement in line(s) between: ['39:39']
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L35-L35), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

85:        uint256 index = (CONTAINER_IDX << (VALIDATOR_HEIGHT + 1)) | uint256(validatorIndex);	// @audit-issue: Same binary operation statement in line(s) between: ['88:88']
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L85-L85), 


```solidity
Path: ./src/entities/MerkleProofs.sol

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue: Same binary operation statement in line(s) between: ['156:156']
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), 


#### Recommendation

Review your Solidity contracts to identify any computations that are performed multiple times with the same inputs. Cache the results of these computations in local variables and reuse them within the function or across function calls if the state remains unchanged.

### Unused State Variables
There are state variables which are declared but not used in any function. This might increase the contract's gas usage unnecessarily.

```solidity
Path: ./src/entities/Pauser.sol

16:    bytes32 private constant PAUSER_STORAGE_SLOT = 0x271441cddf42198c20456f920f5dac04f245854c82f280f2e59e7095958d0b00;	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L16-L16), 


```solidity
Path: ./src/Querier.sol

10:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L10-L10), 


```solidity
Path: ./src/SlashingHandler.sol

17:    string public constant VERSION = "2.0.0";	// @audit-issue

20:    bytes32 internal constant CONFIG_SLOT = 0x661dfff6e6cdad10b44554a6ab58129a188fa46a74caae866b07c414cb424500;	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L17-L17), [20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L20-L20), 


```solidity
Path: ./src/Core.sol

36:    string public constant VERSION = "2.0.0";	// @audit-issue

39:    bytes32 internal constant STORAGE_SLOT = 0x13c729cff436dc8ac22d145f2c778f6a709d225083f39538cc5e2674f2f10700;	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L36-L36), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L39-L39), 


```solidity
Path: ./src/NativeVault.sol

29:    bytes32 internal constant STATE_SLOT = 0x0e977c4f52771ae90b9a885786536a06e14de7815be95b6ed56cdea86f6fc300;	// @audit-issue

32:    bytes32 internal constant CONFIG_SLOT = 0xb6497276931248fe2cc1dc985a2850cccba81036959c83b89ec93582a1e00900;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L29-L29), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L32-L32), 


```solidity
Path: ./src/Vault.sol

32:    string public constant VERSION = "2.0.0";	// @audit-issue

35:    bytes32 internal constant STATE_SLOT = 0x5d654853f9da5c5c659891e7f7fc564033f2724663c32c175f373318f8e1e700;	// @audit-issue

37:    bytes32 internal constant CONFIG_SLOT = 0x22a8eb0cbcfbbbc874f794ecd9efdfeeecb09fe60d66cf9327db2eac8a1ff000;	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L32-L32), [35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L35-L35), [37](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L37-L37), 


#### Recommendation

To optimize your contract's gas usage, remove any state variables that are declared but not used in any function. Unnecessary state variables can increase gas costs and should be eliminated during code review.

### Unused `struct`s
Note that there may be cases where a struct superficially appears to be used, but this is only because there are multiple definitions of the struct in different files. In such cases, the struct definition should be moved into a separate file. The instances below are the unused definitions.

```solidity
Path: ./src/entities/BeaconProofsLib.sol

32:    struct ValidatorProof {	// @audit-issue
33:        uint40 validatorIndex;
34:        bytes32 validatorRoot;
35:        bytes proof;
36:    }
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L32-L36), 


#### Recommendation

Identify and remove any unused `struct` definitions from your Solidity contracts. If a `struct` is defined multiple times across different files, centralize its definition in a single file and import it wherever required. This approach reduces code redundancy, ensures consistency in data structures, and helps maintain a clean and efficient codebase. Regularly auditing your contracts for unused or duplicated code elements like `structs` is a good practice for optimal contract maintenance and development.

### Unused Modifier
Modifier is declared in the project, but never used.

```solidity
Path: ./src/entities/Pauser.sol

44:    modifier whenNotPaused() {	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L44-L44), 


#### Recommendation

Remove redundant code..

### Using Prefix Operators Costs Less Gas Than Postfix Operators in Loops
Conditions can be optimized issues in Solidity refer to situations where smart contract developers write conditional statements that can be simplified or optimized for better gas efficiency, readability, and maintainability. Optimizing conditions can lead to more cost-effective and secure smart contracts.

```solidity
Path: ./src/Querier.sol

29:        for (uint256 i = 0; i < stakedVaults.length; i++) {	// @audit-issue

35:            if (results[i] != bytes32(0)) count++;	// @audit-issue

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue

40:            if (results[i] != bytes32(0)) vaults[latestIndex++] = stakedVaults[i];	// @audit-issue

39:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L29-L29), [35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L35-L35), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L40-L40), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L39-L39), 


```solidity
Path: ./src/SlashingHandler.sol

36:        for (uint256 i = 0; i < _supportedAssets.length; i++) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L36-L36), 


```solidity
Path: ./src/Core.sol

139:        updatedStake = self.requestUpdateVaultStakeInDSS(vaultStakeUpdateRequest, self.nonce++, operator);	// @audit-issue

229:        queuedSlashing = self.requestSlashing(dss, slashingRequest, self.nonce++);	// @audit-issue
```
[139](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L139-L139), [229](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L229-L229), 


```solidity
Path: ./src/NativeVault.sol

157:            snapshot.remainingProofs--;	// @audit-issue

144:        for (uint256 i = 0; i < balanceProofs.length; i++) {	// @audit-issue

194:        for (uint256 i = 0; i < validatorFieldsProofs.length; i++) {	// @audit-issue

247:        withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++);	// @audit-issue
```
[157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L157-L157), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L144-L144), [194](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L194-L194), [247](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L247-L247), 


```solidity
Path: ./src/Vault.sol

139:        withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);	// @audit-issue
```
[139](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L139-L139), 


```solidity
Path: ./src/entities/Operator.sol

233:            if (isVaultStakeToDSS(operatorState, IDSS(dssAddresses[i]), address(vault))) count++;	// @audit-issue

232:        for (uint256 i = 0; i < dssAddresses.length; i++) {	// @audit-issue
```
[233](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L233-L233), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L232-L232), 


```solidity
Path: ./src/entities/CoreLib.sol

71:        for (uint256 i = 0; i < assets.length; i++) {	// @audit-issue

84:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue

132:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L71-L71), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L84-L84), [99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L132-L132), 


```solidity
Path: ./src/entities/SlasherLib.sol

50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {	// @audit-issue

134:        for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L50-L50), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L134-L134), 


```solidity
Path: ./src/entities/MerkleProofs.sol

147:        for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue

155:            for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue
```
[147](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L147-L147), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L155-L155), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

128:            self.ownerToNode[nodeOwner].activeValidatorCount--;	// @audit-issue

182:        self.ownerToNode[nodeOwner].activeValidatorCount++;	// @audit-issue
```
[128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L128-L128), [182](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L182-L182), 


```solidity
Path: ./src/utils/ExtSloads.sol

15:            bytes32 slot = slots[i++];	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L15-L15), 


```solidity
Path: ./src/utils/CommonUtils.sol

19:                lastUnsortedInd++;	// @audit-issue

16:        for (uint256 i = left; i < right; i++) {	// @audit-issue

42:        for (uint256 i = 0; i < arr.length - 1; i++) {	// @audit-issue
```
[19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L19-L19), [16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L16-L16), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L42-L42), 


#### Recommendation

To improve gas efficiency in your Solidity code, prefer using prefix operators (e.g., `++i` or `--i`) instead of postfix operators (e.g., `i++` or `i--`) within loops. Prefix operators typically result in lower gas costs and can contribute to more efficient contract execution.

### Multiple accesses of a mapping/array should use a local variable cache
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's keccak256 hash (Gkeccak256 - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

```solidity
Path: ./src/entities/CoreLib.sol

138:                vaultConfigs[i].symbol,	// @audit-issue: Same index access of variable `vaultConfigs` is used also on line(s): ['144', '136', '137', '139'].
```
[138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L138-L138), 


#### Recommendation

When a mapping or array value is accessed multiple times within a function, cache it in a local `storage` or `calldata` variable. This approach minimizes the gas cost by reducing the number of hash computations for mappings and offset calculations for arrays. Carefully review your functions to identify opportunities for such optimizations, especially in functions with frequent or repeated accesses to the same mapping or array element, to enhance gas efficiency in your contracts.

### State Variables That Are Used Multiple Times In a Function Should Be Cached In Stack Variables
When performing multiple operations on a state variable in a function, it is recommended to cache it first. Either multiple reads or multiple writes to a state variable can save gas by caching it on the stack. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses. Saves 100 gas per instance.


```solidity
Path: ./src/NativeVault.sol

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue: State variable `node` is used also on line(s): ['149'].

311:        if (totalAssetsToSlash > self.totalAssets) {	// @audit-issue: State variable `self` is used also on line(s): ['312'].

433:        uint256 slashedWithdrawable = Math.min(node.nodeAddress.balance, slashedAssets);	// @audit-issue: State variable `node` is used also on line(s): ['444', '443'].
```
[140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [311](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L311-L311), [433](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L433-L433), 


```solidity
Path: ./src/entities/Pauser.sol

69:        if ((self._paused & map) != self._paused) revert AttemptedUnpauseWhilePausing();	// @audit-issue: State variable `self` is used also on line(s): ['69'].
```
[69](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L69-L69), 


#### Recommendation

Cache state variables in stack or local memory variables within functions when they are used multiple times. This approach replaces costlier Gwarmaccess operations with cheaper stack reads, saving approximately 100 gas per instance and optimizing overall contract performance.

### State Variables Only Set in The Constructor Should Be Declared `immutable`
Avoids a Gsset(** 20000 gas**) in the constructor, and replaces the first access in each transaction(Gcoldsload - ** 2100 gas **) and each access thereafter(Gwarmacces - ** 100 gas **) with a`PUSH32`(** 3 gas **).

While`string`s are not value types, and therefore cannot be`immutable` / `constant` if not hard - coded outside of the constructor, the same behavior can be achieved by making the current contract `abstract` with `virtual` functions for the`string` accessors, and having a child contract override the functions with the hard - coded implementation - specific values.

```solidity
Path: ./src/Querier.sol

11:    ICore public core;	// @audit-issue
```
[11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L11-L11), 


#### Recommendation

Consider marking state variables as an immutable that never changes on the contract.

### Increments can be `unchecked` in for-loops
Newer versions of the Solidity compiler will check for integer overflows and underflows automatically. This provides safety but increases gas costs.
When an unsigned integer is guaranteed to never overflow, the unchecked feature of Solidity can be used to save gas costs.A common case for this is for-loops using a strictly-less-than comparision in their conditional statement.

```solidity
Path: ./src/entities/MerkleProofs.sol

55:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

113:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

147:        for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue

155:            for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L55-L55), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L113-L113), [147](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L147-L147), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L155-L155), 


```solidity
Path: ./src/utils/CommonUtils.sol

16:        for (uint256 i = left; i < right; i++) {	// @audit-issue

42:        for (uint256 i = 0; i < arr.length - 1; i++) {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L16-L16), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L42-L42), 


#### Recommendation

Use unchecked math to block overflow / underflow check to save Gas.

### Divisions can be unchecked to save gas
The expression type(int).min/(-1) is the only case where division causes an overflow. Therefore, uncheck can be used to save gas in scenarios where it is certain that such an overflow will not occur.

```solidity
Path: ./src/entities/BeaconProofsLib.sol

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue
```
[121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), 


```solidity
Path: ./src/entities/MerkleProofs.sol

143:        uint256 numNodesInLayer = leaves.length / 2;	// @audit-issue
```
[143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L143-L143), 


```solidity
Path: ./src/entities/HookLib.sol

55:        if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas();	// @audit-issue

87:        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L55-L55), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L87-L87), 


#### Recommendation

Utilize 'unchecked' blocks in Solidity for divisions where overflow is impossible, such as when 'type(int).min/(-1)' is not a concern. This can save gas by bypassing overflow checks in these specific cases.

### Add `unchecked {}` for subtractions where the operands cannot underflow because of a previous `require()` or `if`-statement
Unchecked keyword can be added to such scenerios: 
`require(a <= b); x = b - a` => `require(a <= b); unchecked { x = b - a }`

```solidity
Path: ./src/NativeVault.sol

315:        self.totalAssets -= totalAssetsToSlash;	// @audit-issue
```
[315](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L315-L315), 


#### Recommendation

In scenarios where subtraction cannot result in underflow due to prior `require()` or `if`-statements, wrap these operations in an `unchecked` block to save gas. This optimization should only be applied when the safety of the operation is assured. Carefully analyze each case to confirm that underflow is impossible before implementing `unchecked` blocks, as incorrect usage can lead to vulnerabilities in the contract.

### Stack variable is only used once
If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend

```solidity
Path: ./src/NativeVault.sol

237:        NativeVaultLib.NativeNode storage node = self.ownerToNode[msg.sender];	// @audit-issue: node used only on line: 243

416:        (bool success, bytes memory result) = Constants.BEACON_ROOTS_ADDRESS.staticcall(abi.encode(timestamp));	// @audit-issue: success used only on line: 418

430:        uint256 slashedAssets = node.totalRestakedETH - convertToAssets(balanceOf(nodeOwner));	// @audit-issue: slashedAssets used only on line: 433

500:        uint256 shares = convertToShares(assets);	// @audit-issue: shares used only on line: 501
```
[237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L237-L237), [416](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L416-L416), [430](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L430-L430), [500](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L500-L500), 


```solidity
Path: ./src/Vault.sol

62:        (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));	// @audit-issue: decimalsSuccess used only on line: 68

62:        (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));	// @audit-issue: result used only on line: 68

134:        (VaultLib.State storage state, VaultLib.Config storage config) = _storage();	// @audit-issue: config used only on line: 148

137:        uint256 assets = convertToAssets(shares);	// @audit-issue: assets used only on line: 148

162:        (VaultLib.State storage state, VaultLib.Config storage config) = _storage();	// @audit-issue: config used only on line: 183
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L62-L62), [62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L62-L62), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L134-L134), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L137-L137), [162](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L162-L162), 


```solidity
Path: ./src/entities/Operator.sol

187:        State storage operatorState = self.operatorState[operator];	// @audit-issue: operatorState used only on line: 189

189:        address[] memory vaults = getVaultsStakedToDSS(operatorState, dss);	// @audit-issue: vaults used only on line: 190
```
[187](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L187-L187), [189](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L189-L189), 


```solidity
Path: ./src/entities/SlasherLib.sol

101:        uint256[] memory earmarkedStakes = fetchEarmarkedStakes(slashingMetadata);	// @audit-issue: earmarkedStakes used only on line: 107

179:        uint256 currentSlashablePercentageWad = self.dssMaxSlashablePercentageWad[dss];	// @audit-issue: currentSlashablePercentageWad used only on line: 180
```
[101](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L101-L101), [179](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L179-L179), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

81:        bytes32 validatorRoot = Merkle.merkleizeSha256(validatorFields);	// @audit-issue: validatorRoot used only on line: 92

85:        uint256 index = (CONTAINER_IDX << (VALIDATOR_HEIGHT + 1)) | uint256(validatorIndex);	// @audit-issue: index used only on line: 92

102:        uint256 index = (BEACON_STATE_ROOT_IDX << (BEACON_STATE_HEIGHT)) | BALANCE_CONTAINER_IDX;	// @audit-issue: index used only on line: 109

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue: balanceIndex used only on line: 128

133:        uint256 bitShiftAmount = (validatorIndex % 4) * 64;	// @audit-issue: bitShiftAmount used only on line: 134
```
[81](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L81-L81), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L85-L85), [102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L102-L102), [121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), [133](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L133-L133), 


```solidity
Path: ./src/entities/HookLib.sol

91:        (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(	// @audit-issue: success used only on line: 97
92:            address(dss),
93:            abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId),
94:            supportsInterfaceGasLimit
95:        );

91:        (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(	// @audit-issue: result used only on line: 97
92:            address(dss),
93:            abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId),
94:            supportsInterfaceGasLimit
95:        );
```
[91](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L91-L95), [91](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L91-L95), 


```solidity
Path: ./src/entities/Pauser.sol

59:        uint256 mask = 1 << index;	// @audit-issue: mask used only on line: 60
```
[59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L59-L59), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue: salt used only on line: 99
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), 


```solidity
Path: ./src/utils/CommonUtils.sol

30:        address temp = arr[left];	// @audit-issue: temp used only on line: 32
```
[30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L30-L30), 


#### Recommendation

Eliminate single-use stack variables in Solidity to optimize gas consumption. Directly use the assigned value in the place of the variable. This approach saves the 3 gas typically used for the extra stack assignment, streamlining the function's execution and enhancing overall gas efficiency.

### Don't emit events inside a loop
Emitting an event has an overhead of 375 gas, which will be incurred on every iteration of the loop. It is cheaper to emit only once after the loop has finished.

```solidity
Path: ./src/entities/CoreLib.sol

144:            emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);	// @audit-issue
```
[144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L144-L144), 


#### Recommendation

To optimize gas usage, avoid emitting events inside loops in Solidity. Instead, emit a single event after the loop completes, thereby saving the 375 gas overhead incurred on each iteration.

### `Internal` functions only called once can be inlined to save gas
If an internal function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex. Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

```solidity
Path: ./src/entities/Pauser.sol

40:    function __Pauser_init_unchained() internal onlyInitializing {	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L40-L40), 


```solidity
Path: ./src/NativeVault.sol

425:    function _transferToSlashStore(address nodeOwner) internal {	// @audit-issue

517:    function _updateBalance(address _of, int256 assets) internal {	// @audit-issue
```
[425](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L425-L425), [517](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L517-L517), 


```solidity
Path: ./src/entities/Operator.sol

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

103:    function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {	// @audit-issue

209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)	// @audit-issue

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L103-L103), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L209-L209), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), 


```solidity
Path: ./src/entities/CoreLib.sol

56:    function updateGasValues(	// @audit-issue

89:    function createVault(	// @audit-issue

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue
```
[56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L56-L56), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L89), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), 


```solidity
Path: ./src/entities/SlasherLib.sol

42:    function validateVaultsAndSlashPercentages(	// @audit-issue

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L42), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue

73:    function validateValidatorProof(	// @audit-issue

97:    function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {	// @audit-issue

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L73-L73), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L97-L97), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue

141:    function merkleizeSha256(bytes32[] memory leaves) internal pure returns (bytes32) {	// @audit-issue
```
[48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L48), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L103), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L141-L141), 


```solidity
Path: ./src/entities/HookLib.sol

48:    function callHook(	// @audit-issue
```
[48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L48), 


#### Recommendation

Inline 'internal' functions in Solidity that are called only once to save gas. This avoids the additional gas cost of 20 to 40 units associated with extra JUMP instructions and stack operations required for separate function calls, unless the calling function becomes too complex.

### `Private` functions only called once can be inlined to save gas
If a private function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex. Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), 


#### Recommendation

Inline 'private' functions in Solidity that are called only once to save gas. This avoids the additional gas cost of 20 to 40 units associated with extra JUMP instructions and stack operations required for separate function calls, unless the calling function becomes too complex.

### Optimizing Arithmetic with Shift Operators for Division and Multiplication by Powers of Two
In computational operations, especially within contexts where efficiency matters, certain arithmetic operations can be optimized. One such optimization is leveraging shift operators for division and multiplication by powers of two. This stems from the binary nature of numbers in computing, where shifting bits to the left (using `<<`) effectively multiplies a number by 2 for each position shifted, and shifting bits to the right (using `>>`) divides the number by 2 for each position shifted.

In Solidity, and many other programming languages, using shift operators can be more gas-efficient than traditional arithmetic operations for these specific cases. For instance, instead of performing `value * 4`, one can use `value << 2`, and instead of `value / 4`, one can use `value >> 2`. These optimizations can result in reduced gas costs and faster execution times.


```solidity
Path: ./src/entities/BeaconProofsLib.sol

65:        if (beaconStateRootProof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT)) revert InvalidBeaconStateProof();	// @audit-issue

88:        if (validatorProof.length != 32 * ((VALIDATOR_HEIGHT + 1) + BEACON_STATE_HEIGHT)) {	// @audit-issue

98:        if (proof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT + BEACON_STATE_HEIGHT)) {	// @audit-issue

119:        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();	// @audit-issue

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue

133:        uint256 bitShiftAmount = (validatorIndex % 4) * 64;	// @audit-issue
```
[65](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L65-L65), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L88-L88), [98](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L98-L98), [119](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L119-L119), [121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), [133](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L133-L133), 


```solidity
Path: ./src/entities/MerkleProofs.sol

143:        uint256 numNodesInLayer = leaves.length / 2;	// @audit-issue

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

151:        numNodesInLayer /= 2;	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue

159:            numNodesInLayer /= 2;	// @audit-issue
```
[143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L143-L143), [148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [151](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L151-L151), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), [159](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L159-L159), 


```solidity
Path: ./src/entities/HookLib.sol

55:        if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas();	// @audit-issue

87:        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L55-L55), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L87-L87), 


#### Recommendation

When performing division or multiplication by powers of two in Solidity, consider using shift operators (`<<` for multiplication and `>>` for division) for improved gas efficiency. This optimization takes advantage of the binary nature of computing and can lead to reduced gas costs and faster execution times.

### Multiple Pragma Definition
In Solidity, pragma statements are used to specify the compiler version and settings for a smart contract. This issue occurs when multiple pragma statements are defined within the same contract or file. Each pragma statement should be unique within a contract or file, as it sets the compiler version and potentially other compiler-specific configurations.


```solidity
Path: ./src/NativeNode.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L2-L2), 


```solidity
Path: ./src/SlashStore.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L2-L2), 


```solidity
Path: ./src/Querier.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L2-L2), 


```solidity
Path: ./src/SlashingHandler.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L2-L2), 


```solidity
Path: ./src/Core.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L2-L2), 


```solidity
Path: ./src/NativeVault.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L2-L2), 


```solidity
Path: ./src/Vault.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L2-L2), 


```solidity
Path: ./src/entities/Operator.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L2-L2), 


```solidity
Path: ./src/entities/CoreLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L2-L2), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L2-L2), 


```solidity
Path: ./src/entities/SlasherLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L2-L2), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L2-L2), 


```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


```solidity
Path: ./src/entities/VaultLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L2-L2), 


```solidity
Path: ./src/entities/HookLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L2-L2), 


```solidity
Path: ./src/entities/Pauser.sol

3:pragma solidity ^0.8.21;	// @audit-issue
```
[3](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L3-L3), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L2-L2), 


```solidity
Path: ./src/entities/Withdraw.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L2-L2), 


```solidity
Path: ./src/utils/ExtSloads.sol

2:pragma solidity ^0.8.25;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L2-L2), 


```solidity
Path: ./src/utils/CommonUtils.sol

2:pragma solidity ^0.8.21;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L2-L2), 


#### Recommendation

Ensure each Solidity contract or file contains a single, unique pragma statement to clearly specify the intended compiler version and settings. Avoid multiple pragma definitions to prevent confusion and potential compilation issues.

### Use `private` Rather than `public` for Constants 
In Solidity, constants represent immutable values that cannot be changed after they are set at compile-time. By default, constants have internal visibility, meaning they can be accessed within the contract they are declared in and in derived contracts. If a constant is explicitly declared as `public`, Solidity automatically generates a getter function for it. While this might seem harmless, it actually incurs a gas overhead, especially when the contract is deployed, as the EVM needs to generate bytecode for that getter. Conversely, declaring constants as `private` ensures that no additional getter is generated, optimizing gas usage.

```solidity
Path: ./src/Querier.sol

10:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L10-L10), 


```solidity
Path: ./src/SlashingHandler.sol

17:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L17-L17), 


```solidity
Path: ./src/Core.sol

36:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L36-L36), 


```solidity
Path: ./src/Vault.sol

32:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L32-L32), 


#### Recommendation

To optimize gas usage in your Solidity contracts, declare constants with `private` visibility rather than `public` when possible. Using `private` prevents the automatic generation of a getter function, reducing gas overhead, especially during contract deployment.

### Using `this` to access functions results in an external call, wasting gas
External calls have an overhead of **100 gas**, which can be avoided by not referencing the function using `this`. Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from `external` to `public`, so make this change if it's required in order to call the function internally.

```solidity
Path: ./src/Vault.sol

146:        this.transferFrom(msg.sender, address(this), shares);	// @audit-issue
```
[146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L146-L146), 


#### Recommendation

Adopt a consistent timekeeping mechanism across L1 and L2 solutions when using `block.number` or similar timing mechanisms in your Solidity contracts. Consider using a standard clock or timestamp-based system, especially for functionalities like governance that require consistent timing across chains. For contracts on specific L2 solutions, ensure you're using the correct method to obtain block numbers consistent with the intended behavior. Keep abreast of standards and best practices, such as those suggested by OpenZeppelin, and implement appropriate solutions like EIP-6372 to provide a consistent and reliable timing mechanism across different blockchain environments.

### Consider pre-calculating the address of `address(this)` to save gas
Use `foundry`'s [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady`'s [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

```solidity
Path: ./src/NativeNode.sol

46:        emit NodeETHWithdrawn(address(this), to, weiAmount);	// @audit-issue
```
[46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L46-L46), 


```solidity
Path: ./src/SlashStore.sol

34:        emit NodeETHWithdrawn(address(this), to, weiAmount);	// @audit-issue
```
[34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L34-L34), 


```solidity
Path: ./src/SlashingHandler.sol

56:        SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount);	// @audit-issue
```
[56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L56-L56), 


```solidity
Path: ./src/Vault.sol

146:        this.transferFrom(msg.sender, address(this), shares);	// @audit-issue

167:        if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();	// @audit-issue

173:            by: address(this),	// @audit-issue

175:            owner: address(this),	// @audit-issue
```
[146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L146-L146), [167](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L167-L167), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L173-L173), [175](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L175-L175), 


```solidity
Path: ./src/entities/CoreLib.sol

102:            LibClone.predictDeterministicAddressERC1967BeaconProxy(address(this), salt, address(this));	// @audit-issue

107:        vault.initialize(address(this), operator, depositToken, name, symbol, extraData);	// @audit-issue

150:        return IKarakBaseVault(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue
```
[102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L102-L102), [107](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L107-L107), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L150-L150), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

99:        INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue

100:        newNode.initialize(address(this), owner);	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L99-L99), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L100-L100), 


#### Recommendation

To enhance gas efficiency, cache the contract's address by storing `address(this)` in a state variable at the point of contract deployment or initialization. Use this cached address throughout the contract instead of repeatedly calling `address(this)`. This practice reduces the gas cost associated with multiple computations of the contract's address, leading to more efficient contract execution, especially in scenarios with frequent usage of the contract's address.

### Counting down in for statements is more gas efficient
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

```solidity
Path: ./src/Querier.sol

29:        for (uint256 i = 0; i < stakedVaults.length; i++) {	// @audit-issue

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue

39:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L29-L29), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L39-L39), 


```solidity
Path: ./src/SlashingHandler.sol

36:        for (uint256 i = 0; i < _supportedAssets.length; i++) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L36-L36), 


```solidity
Path: ./src/NativeVault.sol

144:        for (uint256 i = 0; i < balanceProofs.length; i++) {	// @audit-issue

194:        for (uint256 i = 0; i < validatorFieldsProofs.length; i++) {	// @audit-issue
```
[144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L144-L144), [194](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L194-L194), 


```solidity
Path: ./src/entities/Operator.sol

232:        for (uint256 i = 0; i < dssAddresses.length; i++) {	// @audit-issue
```
[232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L232-L232), 


```solidity
Path: ./src/entities/CoreLib.sol

71:        for (uint256 i = 0; i < assets.length; i++) {	// @audit-issue

84:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue

132:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L71-L71), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L84-L84), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L132-L132), 


```solidity
Path: ./src/entities/SlasherLib.sol

50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {	// @audit-issue

85:        for (uint256 i = 0; i < slashingMetadata.vaults.length; ++i) {	// @audit-issue

134:        for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L50-L50), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L85-L85), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L134-L134), 


```solidity
Path: ./src/entities/MerkleProofs.sol

147:        for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue

155:            for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue
```
[147](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L147-L147), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L155-L155), 


```solidity
Path: ./src/utils/CommonUtils.sol

16:        for (uint256 i = left; i < right; i++) {	// @audit-issue

42:        for (uint256 i = 0; i < arr.length - 1; i++) {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L16-L16), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L42-L42), 


#### Recommendation

Where feasible, refactor `for` loops in your Solidity contracts to count downwards. Adjust the loop initialization, condition, and iteration statements to decrement the loop variable and terminate the loop when it reaches zero. This approach can lead to gas savings, making your contract more efficient in terms of execution costs. Ensure that this refactoring aligns with the logic and requirements of your contract, and thoroughly test to confirm that the revised loop behavior matches the intended functionality.

### Use solady library where possible to save gas
The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible

```solidity
Path: ./src/NativeNode.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue

5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";	// @audit-issue

6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L4-L4), [5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L6-L6), 


```solidity
Path: ./src/SlashStore.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue

5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";	// @audit-issue

6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L4-L4), [5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L6-L6), 


```solidity
Path: ./src/Querier.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L4-L4), 


```solidity
Path: ./src/SlashingHandler.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue

7:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L4-L4), [7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L7-L7), 


```solidity
Path: ./src/Core.sol

4:import {OwnableRoles} from "solady/src/auth/OwnableRoles.sol";	// @audit-issue

5:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L4-L4), [5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L5-L5), 


```solidity
Path: ./src/NativeVault.sol

5:import {OwnableRoles} from "solady/src/auth/OwnableRoles.sol";	// @audit-issue

6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L6-L6), 


```solidity
Path: ./src/Vault.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue

6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";	// @audit-issue

10:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L4-L4), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L6-L6), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L10-L10), 


#### Recommendation

Evaluate and, where appropriate, integrate Solady modules in your Solidity contracts as alternatives to similar OpenZeppelin imports. Focus on areas where gas efficiency can be significantly improved. Ensure that any replacement with Solady's modules does not compromise the security or functionality of your contracts. Conduct thorough testing and code reviews when making such substitutions to confirm compatibility and maintain the integrity of your application. Stay informed about updates and community feedback on both libraries to make informed decisions about their use in your projects.

### Consider using solady's 'FixedPointMathLib'
Using Solady's "FixedPointMathLib" for multiplication or division operations in Solidity can lead to significant gas savings. This library is designed to optimize fixed-point arithmetic operations, which are common in financial calculations involving tokens or currencies. By implementing more efficient algorithms and assembly optimizations, "FixedPointMathLib" minimizes the computational resources required for these operations. For contracts that frequently perform such calculations, integrating this library can reduce transaction costs, thereby enhancing overall performance and cost-effectiveness. However, developers must ensure compatibility with their existing codebase and thoroughly test for accuracy and expected behavior to avoid any unintended consequences.

```solidity
Path: ./src/Core.sol

351:        leverage *= Constants.HUNDRED_PERCENT_WAD;	// @audit-issue
```
[351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L351-L351), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

65:        if (beaconStateRootProof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT)) revert InvalidBeaconStateProof();	// @audit-issue

88:        if (validatorProof.length != 32 * ((VALIDATOR_HEIGHT + 1) + BEACON_STATE_HEIGHT)) {	// @audit-issue

98:        if (proof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT + BEACON_STATE_HEIGHT)) {	// @audit-issue

119:        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();	// @audit-issue

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue

133:        uint256 bitShiftAmount = (validatorIndex % 4) * 64;	// @audit-issue

134:        return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;	// @audit-issue

138:        return uint256(fromLittleEndianUint64(validatorFields[BALANCE_IDX])) * 1 gwei;	// @audit-issue
```
[65](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L65-L65), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L88-L88), [98](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L98-L98), [119](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L119-L119), [121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), [133](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L133-L133), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L134-L134), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L138-L138), 


```solidity
Path: ./src/entities/MerkleProofs.sol

143:        uint256 numNodesInLayer = leaves.length / 2;	// @audit-issue

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

151:        numNodesInLayer /= 2;	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue

159:            numNodesInLayer /= 2;	// @audit-issue
```
[143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L143-L143), [148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [151](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L151-L151), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), [159](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L159-L159), 


```solidity
Path: ./src/entities/HookLib.sol

55:        if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas();	// @audit-issue

87:        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L55-L55), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L87-L87), 


#### Recommendation

Consider integrating Solady's 'FixedPointMathLib' into your Solidity contracts for optimized fixed-point arithmetic operations. This library can provide substantial gas savings and enhance the performance of your contract. Before integration, evaluate how 'FixedPointMathLib' aligns with your contract’s requirements. Ensure thorough testing for accuracy and compatibility with your existing contract logic. Carefully document any changes and keep track of how these optimizations affect your contract's operations to maintain transparency and reliability in your application. Adopting 'FixedPointMathLib' should be a considered decision, balancing the benefits of gas efficiency with the need for maintaining code clarity and functionality.

### Reduce Gas Usage by Moving to Solidity 0.8.19 or Later
This issue highlights the opportunity to reduce gas consumption in a smart contract by upgrading the Solidity compiler version to 0.8.19 or a later release. Gas usage is a critical consideration in Ethereum smart contracts, as it directly affects transaction costs and contract execution efficiency. Newer compiler versions often come with optimizations and improvements that can lead to reduced gas costs for certain operations and contract structures.


```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

Consider upgrading to Solidity version 0.8.19 or later to leverage compiler optimizations for reduced gas consumption. Newer versions often include improvements that enhance transaction cost-efficiency and overall contract execution.

### Use bitmap to save gas
Bitmaps in Solidity are essentially a way of representing a set of boolean values within an integer type variable such as `uint256`. Each bit in the integer represents a true or false value (1 or 0), thus allowing efficient storage of multiple boolean values.

Bitmaps can save gas in the Ethereum network because they condense a lot of information into a small amount of storage. In Ethereum, storage is one of the most significant costs in terms of gas usage. By reducing the amount of storage space needed, you can potentially save on gas fees.

Here's a quick comparison:

If you were to represent 256 different boolean values in the traditional way, you would have to declare 256 different `bool` variables. Given that each `bool` occupies a storage slot and each storage slot costs 20,000 gas to initialize, you would end up paying a considerable amount of gas.

On the other hand, if you were to use a bitmap, you could store these 256 boolean values within a single `uint256` variable. In other words, you'd only pay for a single storage slot, resulting in significant gas savings.

However, it's important to note that while bitmaps can provide gas efficiencies, they do add complexity to the code, making it harder to read and maintain. Also, using bitmaps is efficient only when dealing with a large number of boolean variables that are frequently changed or accessed together. 

In contrast, the straightforward counterpart to bitmaps would be using arrays or mappings to store boolean values, with each `bool` value occupying its own storage slot. This approach is simpler and more readable but could potentially be more expensive in terms of gas usage.

```solidity
Path: ./src/SlashingHandler.sol

37:            config.supportedAssets[_supportedAssets[i]] = true;	// @audit-issue

44:        _config().supportedAssets[token] = true;	// @audit-issue
```
[37](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L37-L37), [44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L44-L44), 


```solidity
Path: ./src/entities/CoreLib.sol

154:        self.allowlistedVaultImpl[implementation] = true;	// @audit-issue
```
[154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L154-L154), 


```solidity
Path: ./src/entities/SlasherLib.sol

110:        self.slashingRequests[calculateRoot(queuedSlashing)] = true;	// @audit-issue
```
[110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L110-L110), 


#### Recommendation

Consider using bitmaps in your Solidity contracts when you need to store and manipulate a large set of boolean values. This approach is particularly advantageous in terms of gas efficiency for scenarios involving frequent changes or accesses to these values. However, balance this efficiency with code readability and maintainability. Ensure that the use of bitmaps is well-documented, and consider the complexity it introduces into the code. Employ bitmaps judiciously, especially when their use results in significant gas savings, and the logic they represent is a core aspect of the contract's functionality.

### Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead
When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.
https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html Each operation involving a `uint8` costs an extra [22-28](https://gist.github.com/IllIllI000/9388d20c70f9a4632eb3ca7836f54977) gas (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving `uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the `uint8`, as well as the associated stack operations of doing so. Use a larger size then downcast where needed


```solidity
Path: ./src/Core.sol

57:        uint32 _hookCallGasLimit,	// @audit-issue

58:        uint32 _supportsInterfaceGasLimit,	// @audit-issue

59:        uint32 _hookGasBuffer	// @audit-issue

274:    function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)	// @audit-issue
```
[57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L57-L57), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L58-L58), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L59-L59), [274](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L274-L274), 


```solidity
Path: ./src/NativeVault.sol

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue
```
[384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), 


```solidity
Path: ./src/Vault.sol

62:        (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));	// @audit-issue

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L62-L62), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), 


```solidity
Path: ./src/entities/Operator.sol

64:        uint128 nonce,	// @audit-issue
```
[64](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L64-L64), 


```solidity
Path: ./src/entities/CoreLib.sol

44:        uint32 _hookCallGasLimit,	// @audit-issue

45:        uint32 _supportsInterfaceGasLimit,	// @audit-issue

46:        uint32 _hookGasBuffer	// @audit-issue

58:        uint32 _hookCallGasLimit,	// @audit-issue

59:        uint32 _supportsInterfaceGasLimit,	// @audit-issue

60:        uint32 _hookGasBuffer	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L44-L44), [45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L45-L45), [46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L46-L46), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L58-L58), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L59-L59), [60](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L60-L60), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue

74:        uint40 validatorIndex,	// @audit-issue

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L74-L74), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), 


```solidity
Path: ./src/entities/HookLib.sol

52:        uint32 hookCallGasLimit,	// @audit-issue

53:        uint32 hookGasBuffer	// @audit-issue

83:        uint32 hookCallGasLimit,	// @audit-issue

84:        uint32 supportsInterfaceGasLimit,	// @audit-issue

85:        uint32 hookGasBuffer	// @audit-issue
```
[52](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L52-L52), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L53-L53), [83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L83-L83), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L84-L84), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L85-L85), 


```solidity
Path: ./src/entities/Pauser.sol

49:    modifier whenFunctionNotPaused(uint8 index) {	// @audit-issue

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue
```
[49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L49-L49), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

118:        uint64 timestamp = self.ownerToNode[nodeOwner].currentSnapshotTimestamp;	// @audit-issue

120:        uint40 validatorIndex = validatorDetails.validatorIndex;	// @audit-issue

149:        uint64 updateTimestamp,	// @audit-issue
```
[118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L118-L118), [120](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L120-L120), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L149-L149), 


#### Recommendation

Minimize gas overhead by using 'uint256' or 'int256' instead of smaller integer types in Solidity contracts. The EVM operates more efficiently with 32-byte sizes. Downcast to smaller types only when necessary, as operations with smaller types like 'uint8' incur extra gas due to additional EVM operations for size adjustment.

### Refactor modifiers to call a local function
Modifiers code is copied in all instances where it's used, increasing bytecode size. If deployment gas costs are a concern for this contract, refactoring modifiers into functions can reduce bytecode size significantly at the cost of one JUMP.

```solidity
Path: ./src/NativeVault.sol

529:    modifier nodeExists(address owner) {	// @audit-issue
```
[529](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L529-L529), 


```solidity
Path: ./src/Vault.sol

322:    modifier onlyCore() {	// @audit-issue
```
[322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L322-L322), 


```solidity
Path: ./src/entities/Pauser.sol

44:    modifier whenNotPaused() {	// @audit-issue

49:    modifier whenFunctionNotPaused(uint8 index) {	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L44-L44), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L49-L49), 


#### Recommendation

Evaluate your contract's use of modifiers, particularly those applied across multiple functions, to identify candidates for refactoring into functions. Convert these modifiers into external or public functions that perform the same checks or actions. Then, replace the modifier usage in function declarations with calls to these functions at the start of your functions

### Avoid Unnecessary Public Variables
Public state variables in Solidity automatically generate getter functions, increasing contract size and potentially leading to higher deployment and interaction costs. To optimize gas usage and contract efficiency, minimize the use of public variables unless external access is necessary. Instead, use internal or private visibility combined with explicit getter functions when required. This practice not only reduces contract size but also provides better control over data access and manipulation, enhancing security and readability. Prioritize lean, efficient contracts to ensure cost-effectiveness and better performance on the blockchain.

```solidity
Path: ./src/Querier.sol

10:    string public constant VERSION = "2.0.0";	// @audit-issue

11:    ICore public core;	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L11-L11), 


```solidity
Path: ./src/SlashingHandler.sol

17:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L17-L17), 


```solidity
Path: ./src/Core.sol

36:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L36-L36), 


```solidity
Path: ./src/Vault.sol

32:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L32-L32), 


#### Recommendation

Avoid creating explicit getter functions for 'public' state variables in Solidity. The compiler automatically generates getters for such variables, making additional functions redundant. This practice helps reduce contract size, lowers deployment costs, and simplifies maintenance and understanding of the contract.

### Use `do while` loops intead of for loops
A `do while` loop will cost less gas since the condition is not being checked for the first iteration.
```solidity
uint256 i = 1;
do {                   
    param2 += i;
    i++;
}
while (i < 50);
``` 
is better than
```solidity
for(uint256 i = 1; i< 50; i++){
    param1 += i;
}
```


```solidity
Path: ./src/Querier.sol

29:        for (uint256 i = 0; i < stakedVaults.length; i++) {	// @audit-issue

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue

39:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L29-L29), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L39-L39), 


```solidity
Path: ./src/SlashingHandler.sol

36:        for (uint256 i = 0; i < _supportedAssets.length; i++) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L36-L36), 


```solidity
Path: ./src/NativeVault.sol

144:        for (uint256 i = 0; i < balanceProofs.length; i++) {	// @audit-issue

194:        for (uint256 i = 0; i < validatorFieldsProofs.length; i++) {	// @audit-issue
```
[144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L144-L144), [194](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L194-L194), 


```solidity
Path: ./src/entities/Operator.sol

232:        for (uint256 i = 0; i < dssAddresses.length; i++) {	// @audit-issue
```
[232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L232-L232), 


```solidity
Path: ./src/entities/CoreLib.sol

71:        for (uint256 i = 0; i < assets.length; i++) {	// @audit-issue

84:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue

132:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L71-L71), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L84-L84), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L132-L132), 


```solidity
Path: ./src/entities/SlasherLib.sol

50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {	// @audit-issue

85:        for (uint256 i = 0; i < slashingMetadata.vaults.length; ++i) {	// @audit-issue

134:        for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L50-L50), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L85-L85), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L134-L134), 


```solidity
Path: ./src/entities/MerkleProofs.sol

55:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

113:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

147:        for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue

155:            for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L55-L55), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L113-L113), [147](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L147-L147), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L155-L155), 


```solidity
Path: ./src/utils/ExtSloads.sol

14:        for (uint256 i; i < nSlots;) {	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L14-L14), 


```solidity
Path: ./src/utils/CommonUtils.sol

16:        for (uint256 i = left; i < right; i++) {	// @audit-issue

42:        for (uint256 i = 0; i < arr.length - 1; i++) {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L16-L16), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L42-L42), 


#### Recommendation

Where appropriate, consider using a `do while` loop instead of a `for` loop in your Solidity contracts. This is especially beneficial when the first iteration of the loop does not require a condition check. Refactor your loop logic to fit the `do while` structure for more gas-efficient execution. However, ensure that the loop's logic and termination conditions are correctly implemented to avoid infinite loops or other logical errors. Always balance gas efficiency with code readability and the specific requirements of your contract's logic.

### Using XOR (^) and AND (&) bitwise equivalents for gas optimizations
Given 4 variables a, b, c and d represented as such:
```
0 0 0 0 0 1 1 0 <- a
0 1 1 0 0 1 1 0 <- b
0 0 0 0 0 0 0 0 <- c
1 1 1 1 1 1 1 1 <- d
```
To have a == b means that every 0 and 1 match on both variables. Meaning that a XOR (operator ^) would evaluate to 0 ((a ^ b) == 0), as it excludes by definition any equalities.Now, if a != b, this means that there’s at least somewhere a 1 and a 0 not matching between a and b, making (a ^ b) != 0.Both formulas are logically equivalent and using the XOR bitwise operator costs actually the same amount of gas.However, it is much cheaper to use the bitwise OR operator (|) than comparing the truthy or falsy values.These are logically equivalent too, as the OR bitwise operator (|) would result in a 1 somewhere if any value is not 0 between the XOR (^) statements, meaning if any XOR (^) statement verifies that its arguments are different.


```solidity
Path: ./src/SlashingHandler.sol

53:        if (amount == 0) revert ZeroAmount();	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L53-L53), 


```solidity
Path: ./src/Core.sol

174:        if (newVaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

175:        if (newVaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();	// @audit-issue

188:        if (self.vaultToImplMap[vault] == address(0)) revert VaultNotAChildVault();	// @audit-issue

212:        if (vaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

213:        if (vaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();	// @audit-issue

322:        if (vaultImplOverride == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) {	// @audit-issue
```
[174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L174-L174), [175](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L175-L175), [188](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L188-L188), [212](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L212-L212), [213](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L213-L213), [322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L322-L322), 


```solidity
Path: ./src/NativeVault.sol

62:        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

88:        if (newNodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue

181:        if (beaconStateRootProof.timestamp == block.timestamp) {	// @audit-issue

271:        if (startedWithdrawal.start == 0) revert WithdrawalNotFound();	// @audit-issue

461:        if (revertIfNoBalanceChange && nodeBalanceWei == 0) revert NoBalanceUpdateToSnapshot();	// @audit-issue

481:        if (snapshot.remainingProofs == 0) {	// @audit-issue

530:        if (_state().ownerToNode[owner].nodeAddress == address(0)) revert NotNodeOwner();	// @audit-issue
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L62-L62), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L88-L88), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L181-L181), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L271-L271), [461](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L461-L461), [481](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L481-L481), [530](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L530-L530), 


```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue

100:        if (assets == 0) revert ZeroAmount();	// @audit-issue

117:        if (shares == 0) revert ZeroShares();	// @audit-issue

131:        if (shares == 0) revert ZeroShares();	// @audit-issue

132:        if (beneficiary == address(0)) revert ZeroAddress();	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L100-L100), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), [131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L131-L131), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L132-L132), 


```solidity
Path: ./src/entities/Operator.sol

44:        if (vault == IKarakBaseVault(address(0))) revert ZeroAddress();	// @audit-issue

45:        if (operatorState.vaults.length() == Constants.MAX_VAULTS_PER_OPERATOR) revert MaxVaultCapacityReached();	// @audit-issue

158:        if (operatorState.dssMap.length() == Constants.MAX_DSS_PER_OPERATOR) revert MaxDSSCapacityReached();	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L44-L44), [45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L45-L45), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L158-L158), 


```solidity
Path: ./src/entities/CoreLib.sol

48:        if (_vaultImpl == address(0) || _vetoCommittee == address(0)) {	// @audit-issue

72:            if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress();	// @audit-issue

81:        if (!(implementation == address(0) || isVaultImplAllowlisted(self, implementation))) {	// @audit-issue

85:            if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();	// @audit-issue

127:        if (implementation == address(0)) {	// @audit-issue

158:        return self.allowlistedVaultImpl[implementation] || implementation == self.vaultImpl;	// @audit-issue
```
[48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L48-L48), [72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L72-L72), [81](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L81-L81), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L85-L85), [127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L127-L127), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L158-L158), 


```solidity
Path: ./src/entities/SlasherLib.sol

54:            if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad();	// @audit-issue

74:        if (slashingRequest.vaults.length == 0) revert EmptyArray();	// @audit-issue

181:        if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L54-L54), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L74-L74), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L181-L181), 


```solidity
Path: ./src/entities/MerkleProofs.sol

34:        return processInclusionProofKeccak(proof, leaf, index) == root;	// @audit-issue

53:        require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32");	// @audit-issue

56:            if (index % 2 == 0) {	// @audit-issue

90:        return processInclusionProofSha256(proof, leaf, index) == root;	// @audit-issue

109:            proof.length != 0 && proof.length % 32 == 0,	// @audit-issue

114:            if (index % 2 == 0) {	// @audit-issue
```
[34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L34-L34), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L53-L53), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L56-L56), [90](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L90-L90), [109](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L109-L109), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L114-L114), 


```solidity
Path: ./src/entities/VaultLib.sol

31:        if (qdWithdrawal.start == 0) {	// @audit-issue
```
[31](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L31-L31), 


```solidity
Path: ./src/entities/HookLib.sol

97:        if (!success || result == bytes32(0)) {	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L97-L97), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

127:        if (newBalanceWei == 0) {	// @audit-issue
```
[127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L127-L127), 


```solidity
Path: ./src/utils/CommonUtils.sol

8:        if (arr.length == 0) return;	// @audit-issue

41:        if (arr.length == 0) return false;	// @audit-issue

43:            if (arr[i] == arr[i + 1]) return true;	// @audit-issue
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L8-L8), [41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L41-L41), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L43-L43), 


#### Recommendation

Review your Solidity contracts to identify any computations that are performed multiple times with the same inputs. Cache the results of these computations in local variables and reuse them within the function or across function calls if the state remains unchanged.

### Consider using `bytes32` rather than a `string`
Using the bytes types for fixed-length strings is more efficient than having the EVM have to incur the overhead of string processing. Consider whether the value needs to be a string. A good reason to keep it as a string would be if the variable is defined in an interface that this project does not own.


```solidity
Path: ./src/Querier.sol

10:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L10-L10), 


```solidity
Path: ./src/SlashingHandler.sol

17:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L17-L17), 


```solidity
Path: ./src/Core.sol

36:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L36-L36), 


```solidity
Path: ./src/Vault.sol

32:    string public constant VERSION = "2.0.0";	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L32-L32), 


#### Recommendation

For fixed-length strings, prefer using 'bytes32' over 'string' to leverage EVM efficiency and reduce overhead. Evaluate the necessity of using a string, especially if the variable isn't part of an externally defined interface.

### The result of a function call should be cached rather than re-calling the function
The function calls in solidity are expensive. If the same result of the same function calls are to be used several times, the result should be cached to reduce the gas consumption of repeated calls.        

```solidity
Path: ./src/Vault.sol

202:        ISlashingHandler(slashingHandler).handleSlashing(IERC20(asset()), transferAmount);	// @audit-issue: Function call `asset` is called multiple times at lines [201].
```
[202](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L202-L202), 


```solidity
Path: ./src/entities/SlasherLib.sol

137:                self.assetSlashingHandlers[IKarakBaseVault(queuedSlashing.vaults[i]).asset()]	// @audit-issue: Function call `IKarakBaseVault` is called multiple times at lines [135].
```
[137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L137-L137), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

70:        ) revert InvalidBeaconStateProof();	// @audit-issue: Function call `InvalidBeaconStateProof` is called multiple times at lines [65].

111:        ) revert InvalidBalanceRootProof();	// @audit-issue: Function call `InvalidBalanceRootProof` is called multiple times at lines [99].

130:        ) revert InvalidBalanceProof();	// @audit-issue: Function call `InvalidBalanceProof` is called multiple times at lines [119].
```
[70](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L70-L70), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L111-L111), [130](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L130-L130), 


#### Recommendation

Cache the result of function calls in Solidity instead of making repeated calls to the same function. This practice significantly reduces gas consumption by minimizing costly function call operations.

### Functions guaranteed to `revert` when called by normal users can be marked `payable`
If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

```solidity
Path: ./src/NativeNode.sol

39:    function withdraw(address to, uint256 weiAmount)	// @audit-issue

51:    function pause(uint256 map) external onlyOwner {	// @audit-issue

57:    function unpause(uint256 map) external onlyOwner {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L39), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L51-L51), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L57-L57), 


```solidity
Path: ./src/SlashStore.sol

32:    function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L32-L32), 


```solidity
Path: ./src/SlashingHandler.sol

43:    function addSlashableToken(IERC20 token) external onlyOwner {	// @audit-issue
```
[43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L43-L43), 


```solidity
Path: ./src/Core.sol

72:    function pause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

78:    function unpause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

173:    function changeStandardImplementation(address newVaultImpl) external onlyOwner {	// @audit-issue

183:    function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner {	// @audit-issue

197:    function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

204:    function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

211:    function allowlistVaultImpl(address vaultImpl) external onlyOwner {	// @audit-issue

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue

274:    function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)	// @audit-issue
```
[72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L72-L72), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L78-L78), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L85-L85), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L173-L173), [183](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L183-L183), [197](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L197-L197), [204](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L204-L204), [211](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L211-L211), [235](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L235), [274](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L274-L274), 


```solidity
Path: ./src/NativeVault.sol

83:    function changeNodeImplementation(address newNodeImplementation)	// @audit-issue

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue

322:    function pause(uint256 map) external onlyOwner {	// @audit-issue

328:    function unpause(uint256 map) external onlyOwner {	// @audit-issue

334:    function pauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

340:    function unpauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue
```
[83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L83-L83), [299](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L299), [322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L322-L322), [328](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L328-L328), [334](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L334-L334), [340](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L340-L340), 


```solidity
Path: ./src/Vault.sol

193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue

209:    function pause(uint256 map) external onlyCore {	// @audit-issue

215:    function unpause(uint256 map) external onlyCore {	// @audit-issue
```
[193](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L193-L193), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L209-L209), [215](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L215-L215), 


```solidity
Path: ./src/entities/Pauser.sol

36:    function __Pauser_init() internal onlyInitializing {	// @audit-issue

40:    function __Pauser_init_unchained() internal onlyInitializing {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L36-L36), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L40-L40), 


#### Recommendation

Mark functions with access restrictions like 'onlyOwner' as 'payable' in Solidity. This reduces gas costs for legitimate callers by removing the compiler's checks for incoming payments, as the function will revert for unauthorized users anyway.

### `abi.encode()` is less efficient than `abi.encodePacked()`
When working with Solidity, it is important to pay attention to gas efficiency in order to optimize smart contracts. In this blog post, we will compare the gas costs of `abi.encode()` and `abi.encodepacked()` and explore why the latter is more efficient.Source: [reference](https://github.com/ConnorBlockchain/Solidity-Encode-Gas-Comparison)


```solidity
Path: ./src/NativeVault.sol

416:        (bool success, bytes memory result) = Constants.BEACON_ROOTS_ADDRESS.staticcall(abi.encode(timestamp));	// @audit-issue
```
[416](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L416-L416), 


```solidity
Path: ./src/entities/Operator.sol

50:        return keccak256(abi.encode(newStake));	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L50-L50), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

20:        return keccak256(abi.encode(operator, operatorStateMappingSlot()));	// @audit-issue

28:        return keccak256(abi.encode(vault, pendingStakeUpdateMappingSlot(operator)));	// @audit-issue
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L20-L20), [28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L28-L28), 


```solidity
Path: ./src/entities/SlasherLib.sol

39:        root = keccak256(abi.encode(queuedSlashing));	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L39-L39), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

107:        return keccak256(abi.encode(nodeOwner, nodeOwnerNonce));	// @audit-issue
```
[107](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L107-L107), 


```solidity
Path: ./src/entities/Withdraw.sol

13:        return keccak256(abi.encode(staker, stakerNonce));	// @audit-issue
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L13-L13), 


#### Recommendation

Optimize gas usage by preferring 'abi.encodePacked()' over 'abi.encode()' where appropriate, as 'abi.encodePacked()' is generally more gas-efficient. However, ensure its suitability based on the data type and structure requirements, as 'abi.encodePacked()' can lead to ambiguity in certain cases.

### `x += y` costs more gas than `x = x + y` for stack variables
Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

```solidity
Path: ./src/Core.sol

351:        leverage *= Constants.HUNDRED_PERCENT_WAD;	// @audit-issue
```
[351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L351-L351), 


```solidity
Path: ./src/NativeVault.sol

158:            snapshot.balanceDeltaWei += balanceDeltaWei;	// @audit-issue

195:            totalRestakedWei += self.validateWithdrawalCredentials(	// @audit-issue

241:        self.nodeOwnerToWithdrawAmount[msg.sender] += weiAmount;	// @audit-issue

275:        self.nodeOwnerToWithdrawAmount[startedWithdrawal.nodeOwner] -= startedWithdrawal.assets;	// @audit-issue

283:        node.withdrawableCreditedNodeETH -= startedWithdrawal.assets;	// @audit-issue

315:        self.totalAssets -= totalAssetsToSlash;	// @audit-issue

439:        node.totalRestakedETH -= slashedWithdrawable;	// @audit-issue

484:            node.withdrawableCreditedNodeETH += snapshot.nodeBalanceWei;	// @audit-issue

502:        self.totalAssets += assets;	// @audit-issue

503:        self.ownerToNode[_of].totalRestakedETH += assets;	// @audit-issue

512:        self.totalAssets -= assets;	// @audit-issue

513:        self.ownerToNode[_of].totalRestakedETH -= assets;	// @audit-issue
```
[158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L158-L158), [195](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L195-L195), [241](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L241-L241), [275](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L275-L275), [283](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L283-L283), [315](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L315-L315), [439](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L439-L439), [484](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L484-L484), [502](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L502-L502), [503](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L503-L503), [512](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L512-L512), [513](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L513-L513), 


#### Recommendation

Prefer using 'x = x + y' over 'x += y' for state variable assignments in Solidity to save gas. The latter incurs extra costs due to additional JUMP instructions and stack operations associated with non-inlined function calls.

### Use calldata instead of memory for function arguments that do not get mutated
Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

```solidity
Path: ./src/Core.sol

85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

97:    function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)	// @audit-issue

113:    function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)	// @audit-issue

130:    function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)	// @audit-issue

146:    function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake)	// @audit-issue

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue

248:    function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L85-L85), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L97-L97), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L113-L113), [130](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L130-L130), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L146-L146), [235](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L235), [248](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L248-L248), 


```solidity
Path: ./src/NativeVault.sol

46:    function initialize(
47:        address _owner,
48:        address _operator,
49:        address _depositToken,
50:        string memory _name,	// @audit-issue
51:        string memory _symbol,
52:        bytes memory _extraData
53:    ) external initializer {

46:    function initialize(
47:        address _owner,
48:        address _operator,
49:        address _depositToken,
50:        string memory _name,
51:        string memory _symbol,	// @audit-issue
52:        bytes memory _extraData
53:    ) external initializer {

46:    function initialize(
47:        address _owner,
48:        address _operator,
49:        address _depositToken,
50:        string memory _name,
51:        string memory _symbol,
52:        bytes memory _extraData	// @audit-issue
53:    ) external initializer {

476:    function _updateSnapshot(
477:        NativeVaultLib.NativeNode storage node,
478:        NativeVaultLib.Snapshot memory snapshot,	// @audit-issue
479:        address nodeOwner
480:    ) internal {
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L53), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L53), [52](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L53), [478](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L476-L480), 


```solidity
Path: ./src/Vault.sol

51:    function initialize(
52:        address _owner,
53:        address _operator,
54:        address _depositToken,
55:        string memory _name,	// @audit-issue
56:        string memory _symbol,
57:        bytes memory _extraData
58:    ) external initializer {

51:    function initialize(
52:        address _owner,
53:        address _operator,
54:        address _depositToken,
55:        string memory _name,
56:        string memory _symbol,	// @audit-issue
57:        bytes memory _extraData
58:    ) external initializer {

51:    function initialize(
52:        address _owner,
53:        address _operator,
54:        address _depositToken,
55:        string memory _name,
56:        string memory _symbol,
57:        bytes memory _extraData	// @audit-issue
58:    ) external initializer {
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L58), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L58), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L58), 


```solidity
Path: ./src/entities/Operator.sol

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue

61:    function requestUpdateVaultStakeInDSS(
62:        CoreLib.Storage storage self,
63:        StakeUpdateRequest memory requestStakeUpdate,	// @audit-issue
64:        uint128 nonce,
65:        address operator
66:    ) external returns (QueuedStakeUpdate memory queuedStake) {

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

150:    function registerOperatorToDSS(
151:        CoreLib.Storage storage self,
152:        IDSS dss,
153:        address operator,
154:        bytes memory registrationHookData	// @audit-issue
155:    ) external {

181:    function unregisterOperatorFromDSS(
182:        CoreLib.Storage storage self,
183:        IDSS dss,
184:        address operator,
185:        bytes memory unregistrationHookData	// @audit-issue
186:    ) external {
```
[49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L66), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L150-L155), [185](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L181-L186), 


```solidity
Path: ./src/entities/CoreLib.sol

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

89:    function createVault(
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,	// @audit-issue
94:        string memory symbol,
95:        bytes memory extraData,
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {

89:    function createVault(
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,
94:        string memory symbol,	// @audit-issue
95:        bytes memory extraData,
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {

89:    function createVault(
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,
94:        string memory symbol,
95:        bytes memory extraData,	// @audit-issue
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), [95](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue

42:    function validateVaultsAndSlashPercentages(
43:        CoreLib.Storage storage self,
44:        SlashRequest memory slashingRequest,	// @audit-issue
45:        IDSS dss
46:    ) internal view {

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue

94:    function requestSlashing(
95:        CoreLib.Storage storage self,
96:        IDSS dss,
97:        SlashRequest memory slashingMetadata,	// @audit-issue
98:        uint256 nonce
99:    ) external returns (QueuedSlashing memory queuedSlashing) {

126:    function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue

153:    function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L46), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L99), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L126-L126), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L153-L153), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue
```
[137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue

141:    function merkleizeSha256(bytes32[] memory leaves) internal pure returns (bytes32) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L48), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L85), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L103), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L141-L141), 


```solidity
Path: ./src/entities/HookLib.sol

16:    function performLowLevelCallAndLimitReturnData(address target, bytes memory data, uint256 gasLimit)	// @audit-issue

48:    function callHook(
49:        address target,
50:        bytes memory data,	// @audit-issue
51:        bool ignoreFailure,
52:        uint32 hookCallGasLimit,
53:        uint32 hookGasBuffer
54:    ) internal returns (bool) {

78:    function callHookIfInterfaceImplemented(
79:        IERC165 dss,
80:        bytes memory data,	// @audit-issue
81:        bytes4 interfaceId,
82:        bool ignoreFailure,
83:        uint32 hookCallGasLimit,
84:        uint32 supportsInterfaceGasLimit,
85:        uint32 hookGasBuffer
86:    ) internal returns (bool) {
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L16-L16), [50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L54), [80](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L78-L86), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

110:    function validateSnapshotProof(
111:        Storage storage self,
112:        address nodeOwner,
113:        ValidatorDetails memory validatorDetails,	// @audit-issue
114:        bytes32 balanceRoot,
115:        BeaconProofs.BalanceProof calldata proof
116:    ) internal returns (int256 balanceDeltaWei) {
```
[113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L116), 


```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), 


#### Recommendation

To optimize gas usage in your Solidity functions, mark data types as `calldata` instead of `memory` wherever applicable. This prevents unnecessary data loading into memory. Use `calldata` for function arguments that do not require changes within the function, except when passing them into another function that explicitly requires `memory` storage.

### Splitting `require()` statements that use `&&` saves gas
Instead of using the `&&` operator in a single require statement to check multiple conditions,using multiple require statements with 1 condition per require statement will save 3 GAS per `&&`:

```solidity
Path: ./src/entities/MerkleProofs.sol

108:        require(	// @audit-issue
109:            proof.length != 0 && proof.length % 32 == 0,
110:            "Merkle.processInclusionProofSha256: proof length should be a non-zero multiple of 32"
111:        );
```
[108](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L108-L111), 


#### Recommendation

Split 'require()' statements in Solidity that use '&&' into multiple 'require()' statements, each with a single condition. This approach saves 3 gas per '&&', optimizing overall gas usage in the contract.

### Nesting `if` statements that uses `&&` saves gas
In Solidity, the way conditional checks are structured can impact the gas consumption of a transaction. When conditions are combined using `&&` within an `if` statement, Solidity short-circuits the evaluation, meaning that if the first condition is `false`, the subsequent conditions won't be evaluated. This behavior can lead to gas savings compared to using separate nested `if` statements because not all conditions might need to be checked every time. By efficiently structuring these conditional checks, contracts can optimize the gas required for execution, leading to reduced costs for users.


```solidity
Path: ./src/NativeVault.sol

418:        if (success && result.length > 0) {	// @audit-issue

461:        if (revertIfNoBalanceChange && nodeBalanceWei == 0) revert NoBalanceUpdateToSnapshot();	// @audit-issue
```
[418](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L418-L418), [461](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L461-L461), 


```solidity
Path: ./src/entities/HookLib.sol

59:        if (!ignoreFailure && !success) revert DSSHookCallReverted(returnData);	// @audit-issue
```
[59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L59-L59), 


#### Recommendation


When multiple conditions need to be checked successively, try to combine them in a single `if` statement using `&&` instead of nesting separate `if` statements. This will leverage short-circuit evaluation for potential gas savings.


### Use `!= 0` Instead of `> 0` for Unsigned Integer Comparison
In Solidity, unsigned integers (e.g., `uint256`, `uint8`, etc.) represent non-negative whole numbers, ranging from 0 to a maximum value determined by their bit size. When performing comparisons on these numbers, especially to check if they are non-zero, developers have options. A common practice is to compare against zero using the `>` operator, as in `value > 0`. However, given the nature of unsigned integers, a more straightforward and slightly gas-efficient comparison is to use the `!=` operator, as in `value != 0`.

The primary rationale is that the `!=` comparison directly checks for non-equality, whereas the `>` comparison checks if one value is strictly greater than another. For unsigned integers, where negative values don't exist, the `!= 0` check is both semantically clearer and potentially more efficient at the EVM bytecode level.


```solidity
Path: ./src/NativeVault.sol

360:        return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)].start > 0;	// @audit-issue

418:        if (success && result.length > 0) {	// @audit-issue

518:        if (assets > 0) {	// @audit-issue
```
[360](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L360-L360), [418](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L418-L418), [518](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L518-L518), 


```solidity
Path: ./src/Vault.sol

251:        return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)].start > 0;	// @audit-issue
```
[251](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L251-L251), 


```solidity
Path: ./src/utils/CommonUtils.sol

53:        return size > 0;	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L53-L53), 


#### Recommendation

Use '!= 0' instead of '> 0' for comparing unsigned integers in Solidity. This is semantically clearer and slightly more gas-efficient, as it directly checks for non-zero values without considering unnecessary relational comparisons.

### Constructor Can Be Marked As Payable
`payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A `constructor` can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds.



```solidity
Path: ./src/NativeNode.sol

21:    constructor() {	// @audit-issue
```
[21](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L21-L21), 


```solidity
Path: ./src/SlashStore.sol

14:    constructor() {	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L14-L14), 


```solidity
Path: ./src/Querier.sol

14:    constructor(address coreAddress) {	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L14-L14), 


```solidity
Path: ./src/SlashingHandler.sol

26:    constructor() {	// @audit-issue
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L26-L26), 


```solidity
Path: ./src/Core.sol

42:    constructor() {	// @audit-issue
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L42-L42), 


```solidity
Path: ./src/NativeVault.sol

35:    constructor() {	// @audit-issue
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L35-L35), 


```solidity
Path: ./src/Vault.sol

40:    constructor() {	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L40-L40), 


#### Recommendation

Mark constructors as 'payable' in Solidity contracts to reduce gas costs, as this eliminates the need for the compiler to add checks against incoming payments. This is safe because only the deployer can send funds during contract creation, and typically no funds are sent at this stage.

### Initializers Can Be Marked As Payable
`payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A `initializer` can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds.



```solidity
Path: ./src/NativeNode.sol

28:    function initialize(address _owner, address _nodeOwner) external initializer {	// @audit-issue
```
[28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L28-L28), 


```solidity
Path: ./src/SlashStore.sol

20:    function initialize(address _owner) external initializer {	// @audit-issue
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L20-L20), 


```solidity
Path: ./src/SlashingHandler.sol

33:    function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer {	// @audit-issue
```
[33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L33-L33), 


```solidity
Path: ./src/Core.sol

53:    function initialize(	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L53-L53), 


```solidity
Path: ./src/NativeVault.sol

46:    function initialize(	// @audit-issue
```
[46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L46), 


```solidity
Path: ./src/Vault.sol

51:    function initialize(	// @audit-issue
```
[51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L51), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L40), 


#### Recommendation

Mark initializers as 'payable' in Solidity contracts to reduce gas costs, as this eliminates the need for the compiler to add checks against incoming payments. This is safe because only the deployer can send funds during contract creation, and typically no funds are sent at this stage.

### Optimize names to save gas
`public`/`external` function names and `public` member variable names can be optimized to save gas. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92).


```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


```solidity
Path: ./src/Querier.sol

9:contract Querier {	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L9-L9), 


```solidity
Path: ./src/SlashingHandler.sol

16:contract SlashingHandler is Initializable, Ownable, ISlashingHandler {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L16-L16), 


```solidity
Path: ./src/Core.sol

26:contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {	// @audit-issue
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L26-L26), 


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


```solidity
Path: ./src/entities/Operator.sol

14:library Operator {	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L14-L14), 


```solidity
Path: ./src/entities/CoreLib.sol

16:library CoreLib {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L16-L16), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

13:library CoreStorageSlots {	// @audit-issue
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L13-L13), 


```solidity
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

7:library BeaconProofs {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L7-L7), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Optimize gas usage by renaming 'public'/'external' functions and 'public' member variables in Solidity. Aim for shorter and more efficient names, especially for frequently called functions. This can save gas during deployment and reduce gas costs per call due to lower method ID sorting positions.

### Consider activating `via-ir` for deploying
The IR-based code generator was developed to make code generation more performant by enabling optimization passes that can be applied across functions.

It is possible to activate the IR-based code generator through the command line by using the flag `--via-ir`or by including the option `{"viaIR": true}`.

Keep in mind that compiling with this option may take longer. However, you can simply test it before deploying your code. If you find that it provides better performance, you can add the `--via-ir` flag to your deploy command.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Consider activating `via-ir`.

### Optimize Deployment Size by Fine-tuning IPFS Hash
The Solidity compiler appends 53 bytes of metadata to the smart contract code, incurring an extra cost of 10,600 gas. This additional expense arises from 200 gas per bytecode, plus calldata cost, which amounts to 16 gas for non-zero bytes and 4 gas for zero bytes. This results in a maximum of 848 extra gas in calldata cost.

Reducing this cost is crucial for the following reasons:

The metadata's 53-byte addition leads to a deployment cost increase of 10,600 gas. It can also result in an additional calldata cost of up to 848 gas. Ways to Minimize Gas Consumption:

Employ the `--no-cbor-metadata` compiler option to exclude metadata. Be cautious as this might impact contract verification. Search for code comments that yield an IPFS hash with more zeros, thereby reducing calldata costs.

```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

To optimize deployment size and reduce associated costs, consider the following strategies:
1. **Exclude Metadata with Compiler Option**: Use the `solc` compiler’s `--metadata-hash none` or `--no-cbor-metadata` option to prevent the inclusion of metadata in the compiled bytecode. This action reduces the bytecode size, thus lowering deployment gas costs. However, exercise caution with this approach, as it might affect the ability to verify the contract on platforms like Etherscan.

2. **Optimize IPFS Hash for More Zeros**: If excluding metadata is not desirable, another approach involves optimizing code comments or elements that influence the metadata hash generation to achieve an IPFS hash with a higher proportion of zeros. Since calldata costs are lower for zero bytes, a metadata hash with more zeros can reduce the calldata costs associated with contract interactions.

Example for excluding metadata:
```bash
solc --metadata-hash none YourContract.sol
```


### Assembly: Use scratch space for building calldata
If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

```solidity
Path: ./src/NativeNode.sol

45:        Address.sendValue(payable(to), weiAmount);	// @audit-issue
```
[45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L45-L45), 


```solidity
Path: ./src/SlashStore.sol

33:        Address.sendValue(payable(to), weiAmount);	// @audit-issue
```
[33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L33-L33), 


```solidity
Path: ./src/Querier.sol

27:        address[] memory stakedVaults = core.fetchVaultsStakedInDSS(operator, dss);	// @audit-issue

30:            slots[i] = CoreStorageSlots.vaultPendingStakeUpdateSlot(operator, stakedVaults[i]);	// @audit-issue

32:        bytes32[] memory results = core.extSloads(slots);	// @audit-issue
```
[27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L27-L27), [30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L30-L30), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L32-L32), 


```solidity
Path: ./src/Core.sol

89:        _self().allowlistAssets(assets, slashingHandlers);	// @audit-issue

104:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

120:        self.checkIfOperatorIsRegInRegDSS(operator, dss);	// @audit-issue

138:        self.checkIfOperatorIsRegInRegDSS(operator, vaultStakeUpdateRequest.dss);	// @audit-issue

151:        _self().validateAndUpdateVaultStakeInDSS(queuedStake);	// @audit-issue

185:        if (!self.isVaultImplAllowlisted(newVaultImpl)) revert VaultImplNotAllowlisted();	// @audit-issue

198:        vault.pause(map);	// @audit-issue

205:        vault.unpause(map);	// @audit-issue

215:        _self().allowlistVaultImpl(vaultImpl);	// @audit-issue

228:        self.checkIfOperatorIsRegInRegDSS(slashingRequest.operator, dss);	// @audit-issue

241:        _self().cancelSlashing(queuedSlashing);	// @audit-issue

253:        _self().finalizeSlashing(queuedSlashing);	// @audit-issue

264:        if (!address(dss).isSmartContract()) revert NotSmartContract();	// @audit-issue

265:        _self().setDSSMaxSlashablePercentageWad(dss, maxSlashablePercentageWad);	// @audit-issue

295:        return _self().isVaultImplAllowlisted(vaultImpl);	// @audit-issue

303:        return _self().isOperatorRegisteredToDSS(operator, dss);	// @audit-issue

332:        return _self().operatorState[operator].getVaults();	// @audit-issue

340:        vaults = _self().operatorState[operator].getVaultsStakedToDSS(dss);	// @audit-issue

350:        leverage = _self().getDSSCountVaultStakedTo(IKarakBaseVault(vault));	// @audit-issue

359:        slashablePercentageWad = _self().getDSSMaxSlashablePercentageWad(dss);	// @audit-issue

366:        return _self().isDSSRegistered(dss);	// @audit-issue

379:        res = super.extSloads(slots);	// @audit-issue
```
[89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L89-L89), [104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L104-L104), [120](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L120-L120), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L138-L138), [151](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L151-L151), [185](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L185-L185), [198](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L198-L198), [205](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L205-L205), [215](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L215-L215), [228](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L228-L228), [241](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L241-L241), [253](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L253-L253), [264](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L264-L264), [265](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L265-L265), [295](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L295-L295), [303](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L303-L303), [332](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L332-L332), [340](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L340-L340), [350](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L350-L350), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L359-L359), [366](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L366-L366), [379](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L379-L379), 


```solidity
Path: ./src/NativeVault.sol

102:        address newNodeAddr = self.deployNode(_config(), msg.sender);	// @audit-issue

142:        BeaconProofs.validateBalanceContainer(snapshot.parentBeaconBlockRoot, balanceContainer);	// @audit-issue

190:        BeaconProofs.validateBeaconStateRootProof(	// @audit-issue

247:        withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++);	// @audit-issue

282:        INativeNode(node.nodeAddress).withdraw(startedWithdrawal.to, startedWithdrawal.assets);	// @audit-issue

335:        node.pause(map);	// @audit-issue

341:        node.unpause(map);	// @audit-issue

348:            Math.min(convertToAssets(balanceOf(nodeOwner)), _state().ownerToNode[nodeOwner].withdrawableCreditedNodeETH);	// @audit-issue

360:        return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)].start > 0;	// @audit-issue

368:        return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)];	// @audit-issue

416:        (bool success, bytes memory result) = Constants.BEACON_ROOTS_ADDRESS.staticcall(abi.encode(timestamp));	// @audit-issue

433:        uint256 slashedWithdrawable = Math.min(node.nodeAddress.balance, slashedAssets);	// @audit-issue

436:        INativeNode(node.nodeAddress).withdraw(self.slashStore, slashedWithdrawable);	// @audit-issue
```
[102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L102-L102), [142](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L142-L142), [190](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L190-L190), [247](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L247-L247), [282](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L282-L282), [335](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L335-L335), [341](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L341-L341), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L348-L348), [360](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L360-L360), [368](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L368-L368), [416](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L416-L416), [433](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L433-L433), [436](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L436-L436), 


```solidity
Path: ./src/Vault.sol

86:        return super.deposit(assets, to);	// @audit-issue

101:        shares = super.deposit(assets, to);	// @audit-issue

118:        assets = super.mint(shares, to);	// @audit-issue

139:        withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);	// @audit-issue

164:        WithdrawLib.QueuedWithdrawal memory startedWithdrawal = state.validateQueuedWithdrawal(withdrawalKey);	// @audit-issue

198:        transferAmount = Math.min(totalAssets(), totalAssetsToSlash);	// @audit-issue

202:        ISlashingHandler(slashingHandler).handleSlashing(IERC20(asset()), transferAmount);	// @audit-issue

251:        return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)].start > 0;	// @audit-issue

263:        return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)];	// @audit-issue

268:        return super.totalAssets();	// @audit-issue

273:        return super.owner();	// @audit-issue

291:        res = super.extSloads(slots);	// @audit-issue
```
[86](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L86-L86), [101](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L101-L101), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L118-L118), [139](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L139-L139), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L164-L164), [198](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L198-L198), [202](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L202-L202), [251](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L251-L251), [263](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L263-L263), [268](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L268-L268), [273](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L273-L273), [291](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L291-L291), 


```solidity
Path: ./src/entities/Operator.sol

40:        return operatorState.vaults.values();	// @audit-issue

45:        if (operatorState.vaults.length() == Constants.MAX_VAULTS_PER_OPERATOR) revert MaxVaultCapacityReached();	// @audit-issue

46:        operatorState.vaults.add(address(vault));	// @audit-issue

58:        if (!operatorState.vaults.contains(stakeUpdate.vault)) revert VaultNotAChildVault();	// @audit-issue

105:            operatorState.vaultStakedInDssMap[dss].add(vault);	// @audit-issue

107:            operatorState.vaultStakedInDssMap[dss].remove(vault);	// @audit-issue

140:        return self.operatorState[operator].dssMap.contains(address(dss));	// @audit-issue

144:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

158:        if (operatorState.dssMap.length() == Constants.MAX_DSS_PER_OPERATOR) revert MaxDSSCapacityReached();	// @audit-issue

160:        operatorState.dssMap.add(address(dss));	// @audit-issue

178:        vaults = operatorState.vaultStakedInDssMap[dss].values();	// @audit-issue

193:        self.operatorState[operator].dssMap.remove(address(dss));	// @audit-issue

214:        dssAddresses = self.operatorState[operator].dssMap.values();	// @audit-issue

218:        return operatorState.vaultStakedInDssMap[dss].contains(vault);	// @audit-issue

229:        address operator = vault.vaultConfig().operator;	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L40-L40), [45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L45-L45), [46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L46-L46), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L58-L58), [105](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L105-L105), [107](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L107-L107), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L140-L140), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L144-L144), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L158-L158), [160](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L160-L160), [178](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L178-L178), [193](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L193-L193), [214](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L214-L214), [218](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L218-L218), [229](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L229-L229), 


```solidity
Path: ./src/entities/CoreLib.sol

143:            self.operatorState[operator].addVault(vault);	// @audit-issue

150:        return IKarakBaseVault(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue
```
[143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L143-L143), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L150-L150), 


```solidity
Path: ./src/entities/SlasherLib.sol

47:        if (slashingRequest.vaults.hasDuplicates()) revert DuplicateSlashingVaults();	// @audit-issue

51:            if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {	// @audit-issue

88:                IKarakBaseVault(slashingMetadata.vaults[i]).totalAssets(),	// @audit-issue

135:            IKarakBaseVault(queuedSlashing.vaults[i]).slashAssets(	// @audit-issue

137:                self.assetSlashingHandlers[IKarakBaseVault(queuedSlashing.vaults[i]).asset()]	// @audit-issue
```
[47](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L47-L47), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L51-L51), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L88-L88), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L135-L135), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L137-L137), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

81:        bytes32 validatorRoot = Merkle.merkleizeSha256(validatorFields);	// @audit-issue
```
[81](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L81-L81), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

99:        INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue

100:        newNode.initialize(address(this), owner);	// @audit-issue

153:        bytes32 validatorPubkeyHash = BeaconProofs.getPubkeyHash(validatorFieldsProof.validatorFields);	// @audit-issue

158:        if (BeaconProofs.getExitEpoch(validatorFieldsProof.validatorFields) != type(uint64).max) {	// @audit-issue

163:            BeaconProofs.getWithdrawalCredentials(validatorFieldsProof.validatorFields)	// @audit-issue

169:        uint256 restakedBalanceWei = BeaconProofs.getEffectiveBalanceWei(validatorFieldsProof.validatorFields);	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L99-L99), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L100-L100), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L153-L153), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L158-L158), [163](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L163-L163), [169](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L169-L169), 


#### Recommendation

Review your smart contracts to identify and remove `block.number` and `block.timestamp` from the parameters of emitted events. Instead of manually adding these fields, rely on the Ethereum blockchain's inherent inclusion of this information within the block context. Simplify your event definitions to include only the essential data specific to the event's purpose, excluding universally available block metadata.

### Use assembly to check for `address(0)`
In Solidity, it's a common practice to check whether an Ethereum address variable is set to the zero address (`address(0)`) to handle various scenarios, such as token transfers or contract interactions. Typically, this check is performed using a conditional statement like `if (addressVariable == address(0))`.

However, using this approach in high-frequency or gas-sensitive operations can lead to unnecessary gas costs. A more gas-efficient alternative is to use inline assembly to perform the zero address check, which can significantly reduce gas consumption, especially in loops or complex contract logic.

By utilizing inline assembly for this specific check, you can optimize gas usage and make your Solidity code more efficient.

```solidity
Path: ./src/SlashingHandler.sol

58:        SafeTransferLib.safeTransfer(address(token), address(0), amount);	// @audit-issue
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L58-L58), 


```solidity
Path: ./src/Core.sol

174:        if (newVaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

188:        if (self.vaultToImplMap[vault] == address(0)) revert VaultNotAChildVault();	// @audit-issue

212:        if (vaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

289:        return _self().assetSlashingHandlers[asset] != address(0);	// @audit-issue
```
[174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L174-L174), [188](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L188-L188), [212](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L212-L212), [289](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L289-L289), 


```solidity
Path: ./src/NativeVault.sol

62:        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

88:        if (newNodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L62-L62), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L88-L88), 


```solidity
Path: ./src/Vault.sol

132:        if (beneficiary == address(0)) revert ZeroAddress();	// @audit-issue
```
[132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L132-L132), 


```solidity
Path: ./src/entities/Operator.sol

44:        if (vault == IKarakBaseVault(address(0))) revert ZeroAddress();	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L44-L44), 


```solidity
Path: ./src/entities/CoreLib.sol

48:        if (_vaultImpl == address(0) || _vetoCommittee == address(0)) {	// @audit-issue

72:            if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress();	// @audit-issue

81:        if (!(implementation == address(0) || isVaultImplAllowlisted(self, implementation))) {	// @audit-issue

85:            if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();	// @audit-issue

127:        if (implementation == address(0)) {	// @audit-issue
```
[48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L48-L48), [72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L72-L72), [81](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L81-L81), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L85-L85), [127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L127-L127), 


#### Recommendation

To optimize gas usage in your Solidity code, consider using inline assembly for checking `address(0)`. This approach can significantly reduce gas costs, especially in high-frequency or gas-sensitive operations, leading to more efficient contract execution.

### Use assembly to check for `0`
Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

```solidity
Path: ./src/SlashingHandler.sol

53:        if (amount == 0) revert ZeroAmount();	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L53-L53), 


```solidity
Path: ./src/NativeVault.sol

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue

271:        if (startedWithdrawal.start == 0) revert WithdrawalNotFound();	// @audit-issue

360:        return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)].start > 0;	// @audit-issue

418:        if (success && result.length > 0) {	// @audit-issue

451:        if (node.currentSnapshotTimestamp != 0) revert PendingIncompleteSnapshot();	// @audit-issue

461:        if (revertIfNoBalanceChange && nodeBalanceWei == 0) revert NoBalanceUpdateToSnapshot();	// @audit-issue

481:        if (snapshot.remainingProofs == 0) {	// @audit-issue

518:        if (assets > 0) {	// @audit-issue

520:        } else if (assets < 0) {	// @audit-issue
```
[140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L271-L271), [360](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L360-L360), [418](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L418-L418), [451](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L451-L451), [461](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L461-L461), [481](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L481-L481), [518](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L518-L518), [520](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L520-L520), 


```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue

100:        if (assets == 0) revert ZeroAmount();	// @audit-issue

117:        if (shares == 0) revert ZeroShares();	// @audit-issue

131:        if (shares == 0) revert ZeroShares();	// @audit-issue

251:        return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)].start > 0;	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L100-L100), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), [131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L131-L131), [251](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L251-L251), 


```solidity
Path: ./src/entities/Operator.sol

190:        if (vaults.length != 0) revert AllVaultsNotUnstakedFromDSS();	// @audit-issue
```
[190](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L190-L190), 


```solidity
Path: ./src/entities/CoreLib.sol

162:        return self.dssMaxSlashablePercentageWad[dss] != 0;	// @audit-issue
```
[162](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L162-L162), 


```solidity
Path: ./src/entities/SlasherLib.sol

54:            if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad();	// @audit-issue

74:        if (slashingRequest.vaults.length == 0) revert EmptyArray();	// @audit-issue

180:        if (currentSlashablePercentageWad != 0) revert DSSAlreadyRegistered();	// @audit-issue

181:        if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L54-L54), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L74-L74), [180](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L180-L180), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L181-L181), 


```solidity
Path: ./src/entities/MerkleProofs.sol

53:        require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32");	// @audit-issue

56:            if (index % 2 == 0) {	// @audit-issue

109:            proof.length != 0 && proof.length % 32 == 0,	// @audit-issue

114:            if (index % 2 == 0) {	// @audit-issue

153:        while (numNodesInLayer != 0) {	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L53-L53), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L56-L56), [109](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L109-L109), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L114-L114), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L153-L153), 


```solidity
Path: ./src/entities/VaultLib.sol

31:        if (qdWithdrawal.start == 0) {	// @audit-issue
```
[31](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L31-L31), 


```solidity
Path: ./src/entities/Pauser.sol

55:        return (_getPauserStorage()._paused != 0);	// @audit-issue

60:        return ((_getPauserStorage()._paused & mask) != 0);	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L55-L55), [60](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L60-L60), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

127:        if (newBalanceWei == 0) {	// @audit-issue
```
[127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L127-L127), 


```solidity
Path: ./src/utils/CommonUtils.sol

8:        if (arr.length == 0) return;	// @audit-issue

41:        if (arr.length == 0) return false;	// @audit-issue

53:        return size > 0;	// @audit-issue
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L8-L8), [41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L41-L41), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L53-L53), 


#### Recommendation

To optimize gas usage in your Solidity code, consider using inline assembly for checking `0`. This approach can significantly reduce gas costs, especially in high-frequency or gas-sensitive operations, leading to more efficient contract execution.

### Use assembly to write `address` storage values
Using assembly `{ sstore(state.slot, addr)}` instead of `state = addr` can save gas.


```solidity
Path: ./src/NativeNode.sol

32:        nodeOwner = _nodeOwner;	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L32-L32), 


```solidity
Path: ./src/Querier.sol

15:        core = ICore(coreAddress);	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L15-L15), 


#### Recommendation

To reduce gas costs in your Solidity code, consider using assembly with `{ sstore(state.slot, addr) }` for writing `address` storage values instead of `state = addr`. This approach can result in significant gas savings.

### Use assembly to emit an `event`
To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.


```solidity
Path: ./src/entities/Pauser.sol

71:        emit Paused(_msgSender(), map);	// @audit-issue

78:        emit Unpaused(_msgSender(), map);	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L71-L71), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L78-L78), 


#### Recommendation

To optimize event emission in your Solidity code, consider using assembly with scratch space and the free memory pointer. This approach can help reduce gas costs by avoiding memory expansion expenses. However, it's crucial to ensure safe optimization by caching and restoring the free memory pointer, as demonstrated in examples like Solady's codebase.

### Use assembly to write hashes
Considering using [assembly](https://medium.com/@kalexotsu/understanding-solidity-assembly-hashing-a-string-from-calldata-fbd2ece82263) to write hashes, as it's possible to save a considerable amount of gas.


```solidity
Path: ./src/entities/Operator.sol

50:        return keccak256(abi.encode(newStake));	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L50-L50), 


```solidity
Path: ./src/entities/CoreLib.sol

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

20:        return keccak256(abi.encode(operator, operatorStateMappingSlot()));	// @audit-issue

28:        return keccak256(abi.encode(vault, pendingStakeUpdateMappingSlot(operator)));	// @audit-issue
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L20-L20), [28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L28-L28), 


```solidity
Path: ./src/entities/SlasherLib.sol

39:        root = keccak256(abi.encode(queuedSlashing));	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L39-L39), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue

107:        return keccak256(abi.encode(nodeOwner, nodeOwnerNonce));	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), [107](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L107-L107), 


```solidity
Path: ./src/entities/Withdraw.sol

13:        return keccak256(abi.encode(staker, stakerNonce));	// @audit-issue
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L13-L13), 


#### Recommendation

To achieve gas savings in your Solidity code when writing hashes, consider using assembly, as it can significantly reduce gas consumption. You can refer to this [article](https://medium.com/@kalexotsu/understanding-solidity-assembly-hashing-a-string-from-calldata-fbd2ece82263) for insights on how to efficiently implement hash operations.