### Centralization risk for privileged functions
Contracts with privileged functions need owner/admin to be trusted not to perform malicious updates or drain funds. This may also cause a single point failure.


```solidity
Path: ./src/NativeNode.sol

39:    function withdraw(address to, uint256 weiAmount)
40:        external
41:        onlyOwner	// @audit-issue

51:    function pause(uint256 map) external onlyOwner {	// @audit-issue

57:    function unpause(uint256 map) external onlyOwner {	// @audit-issue
```
[41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L41), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L51-L51), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L57-L57), 


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

85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)
86:        external
87:        onlyRolesOrOwner(Constants.MANAGER_ROLE)	// @audit-issue

173:    function changeStandardImplementation(address newVaultImpl) external onlyOwner {	// @audit-issue

183:    function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner {	// @audit-issue

197:    function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

204:    function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

211:    function allowlistVaultImpl(address vaultImpl) external onlyOwner {	// @audit-issue

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)
236:        external
237:        whenFunctionNotPaused(Constants.PAUSE_CORE_CANCEL_SLASHING)
238:        nonReentrant
239:        onlyRoles(Constants.VETO_COMMITTEE_ROLE)	// @audit-issue

274:    function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)
275:        external
276:        onlyRolesOrOwner(Constants.MANAGER_ROLE)	// @audit-issue
```
[72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L72-L72), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L78-L78), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L85-L87), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L173-L173), [183](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L183-L183), [197](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L197-L197), [204](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L204-L204), [211](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L211-L211), [239](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L239), [276](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L274-L276), 


```solidity
Path: ./src/NativeVault.sol

83:    function changeNodeImplementation(address newNodeImplementation)
84:        external
85:        onlyOwnerOrRoles(Constants.MANAGER_ROLE)	// @audit-issue

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
300:        external
301:        onlyOwner	// @audit-issue

322:    function pause(uint256 map) external onlyOwner {	// @audit-issue

328:    function unpause(uint256 map) external onlyOwner {	// @audit-issue

334:    function pauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue

340:    function unpauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L83-L85), [301](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L301), [322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L322-L322), [328](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L328-L328), [334](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L334-L334), [340](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L340-L340), 


```solidity
Path: ./src/Vault.sol

193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
194:        external
195:        onlyCore	// @audit-issue

209:    function pause(uint256 map) external onlyCore {	// @audit-issue

215:    function unpause(uint256 map) external onlyCore {	// @audit-issue
```
[195](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L193-L195), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L209-L209), [215](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L215-L215), 


```solidity
Path: ./src/entities/Pauser.sol

36:    function __Pauser_init() internal onlyInitializing {	// @audit-issue

40:    function __Pauser_init_unchained() internal onlyInitializing {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L36-L36), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L40-L40), 


#### Recommendation

To mitigate centralization risks associated with privileged functions, consider implementing a multi-signature or decentralized governance mechanism. Instead of relying solely on a single owner/administrator, distribute control and decision-making authority among multiple parties or stakeholders. This approach enhances security, reduces the risk of malicious actions by a single entity, and prevents single points of failure. Explore governance solutions and smart contract frameworks that support decentralized control and decision-making to enhance the trustworthiness and resilience of your contract.

### Missing checks for `address(0)` in constructor/initializers
In Solidity, the Ethereum address `0x0000000000000000000000000000000000000000` is known as the "zero address". This address has significance because it's the default value for uninitialized address variables and is often used to represent an invalid or non-existent address. The "
Missing zero address control" issue arises when a Solidity smart contract does not properly check or prevent interactions with the zero address, leading to unintended behavior.
For instance, a contract might allow tokens to be sent to the zero address without any checks, which essentially burns those tokens as they become irretrievable. While sometimes this is intentional, without proper control or checks, accidental transfers could occur.    
        

```solidity
Path: ./src/NativeNode.sol

29:        _initializeOwner(_owner);	// @audit-issue

32:        nodeOwner = _nodeOwner;	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L29-L29), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L32-L32), 


```solidity
Path: ./src/SlashStore.sol

21:        _initializeOwner(_owner);	// @audit-issue
```
[21](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L21-L21), 


```solidity
Path: ./src/Querier.sol

15:        core = ICore(coreAddress);	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L15-L15), 


```solidity
Path: ./src/SlashingHandler.sol

34:        _initializeOwner(owner);	// @audit-issue
```
[34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L34-L34), 


```solidity
Path: ./src/NativeVault.sol

54:        _initializeOwner(_owner);	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L54-L54), 


```solidity
Path: ./src/Vault.sol

59:        _initializeOwner(_owner);	// @audit-issue
```
[59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L59-L59), 


#### Recommendation

It is strongly recommended to implement checks to prevent the zero address from being set during the initialization of contracts. This can be achieved by adding require statements that ensure address parameters are not the zero address. 

### Missing checks for `address(0)`  when updating state variables
In Solidity, the Ethereum address `0x0000000000000000000000000000000000000000` is known as the "zero address". This address has significance because it's the default value for uninitialized address variables and is often used to represent an invalid or non-existent address. The "
Missing zero address control" issue arises when a Solidity smart contract does not properly check or prevent interactions with the zero address, leading to unintended behavior.
For instance, a contract might allow tokens to be sent to the zero address without any checks, which essentially burns those tokens as they become irretrievable. While sometimes this is intentional, without proper control or checks, accidental transfers could occur.    
        

```solidity
Path: ./src/Core.sol

104:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

366:        return _self().isDSSRegistered(dss);	// @audit-issue
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L104-L104), [366](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L366-L366), 


```solidity
Path: ./src/entities/Operator.sol

107:            operatorState.vaultStakedInDssMap[dss].remove(vault);	// @audit-issue

144:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue
```
[107](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L107-L107), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L144-L144), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

28:        return keccak256(abi.encode(vault, pendingStakeUpdateMappingSlot(operator)));	// @audit-issue
```
[28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L28-L28), 


#### Recommendation

It is strongly recommended to implement checks to prevent the zero address from being set during the initialization of contracts. This can be achieved by adding require statements that ensure address parameters are not the zero address. 

### Security Risks Associated with Relying on `extcodesize` for Contract Verification
The use of `extcodesize` in smart contracts is a common method to distinguish between Externally Owned Accounts (EOAs) and contract accounts. However, this approach has inherent vulnerabilities that can compromise security. Primarily, when `extcodesize` is called within a contract’s constructor, it invariably returns 0. This behavior can be exploited, as it inaccurately suggests the constructor is an EOA, potentially allowing non-EOA entities to bypass checks meant to restrict access to contracts only.

Additionally, a significant limitation arises when `extcodesize` is used to verify an account before it deploys a contract. In such cases, `extcodesize` would return 0, indicating no code at the address, leading to incorrect validation as an EOA. If the account subsequently deploys a contract, the earlier validation becomes obsolete, potentially enabling unauthorized activities or access.

```solidity
Path: ./src/utils/CommonUtils.sol

51:            size := extcodesize(addr)	// @audit-issue
```
[51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L51-L51), 


#### Recommendation

It is recommended to not use `extcodesize` for contract existance check.

### Use `Ownable2Step` rather than `Ownable`
[Ownable2Step](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/3d7a93876a2e5e1d7fe29b5a0e96e222afdc4cfa/contracts/access/Ownable2Step.sol#L31-L56) and [Ownable2StepUpgradeable](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/25aabd286e002a1526c345c8db259d57bdf0ad28/contracts/access/Ownable2StepUpgradeable.sol#L47-L63) prevent the contract ownership from mistakenly being transferred to an address that cannot handle it (e.g. due to a typo in the address), by requiring that the recipient of the owner permissions actively accept via a contract call of its own.


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
Path: ./src/SlashingHandler.sol

16:contract SlashingHandler is Initializable, Ownable, ISlashingHandler {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L16-L16), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


#### Recommendation

Consider using `Ownable2Step` or `Ownable2StepUpgradeable` from OpenZeppelin Contracts to enhance the security of your contract ownership management. These contracts prevent the accidental transfer of ownership to an address that cannot handle it, such as due to a typo, by requiring the recipient of owner permissions to actively accept ownership via a contract call. This two-step ownership transfer process adds an additional layer of security to your contract's ownership management.

### Unsafe downcast may overflow
When a type is downcast to a smaller type, the higher order bits are discarded, resulting in the application of a modulo operation to the original value.

If the downcasted value is large enough, this may result in an overflow that will not revert.


```solidity
Path: ./src/entities/BeaconProofsLib.sol

85:        uint256 index = (CONTAINER_IDX << (VALIDATOR_HEIGHT + 1)) | uint256(validatorIndex);	// @audit-issue: Variable `validatorIndex` is type `uint40` and it is downcasted to `uint256`

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue: Variable `validatorIndex` is type `uint40` and it is downcasted to `uint256`
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L85-L85), [121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), 


#### Recommendation

When downcasting numbers to `addresses` in Solidity, be cautious of potential collisions. Downcasting truncates the upper bytes of the number, which can lead to multiple values mapping to the same `address`. To avoid collisions, consider using a more robust mapping strategy or additional checks to ensure unique mappings.

### Avoid Double `casting`
Consider refactoring the following code, as double casting may introduce unexpected truncations and/or rounding issues.

Furthermore, double type casting can make the code less readable and harder to maintain, increasing the likelihood of errors and misunderstandings during development and debugging.


```solidity
Path: ./src/entities/BeaconProofsLib.sol

55:        n = uint64(uint256(lenum >> 192));	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L55-L55), 


#### Recommendation

To enhance code readability, maintainability, and avoid potential truncation or rounding issues, refactor code that involves double type casting. Minimize the use of double casting to improve code quality and reduce the risk of errors during development and debugging.

### Int casting `block.timestamp` can reduce the lifespan of a contract
In Solidity, `block.timestamp` returns the Unix timestamp of the current block, which is a continuously increasing value. Casting `block.timestamp` to a smaller integer type, like `uint32`, can limit the maximum value it can hold. As time progresses and the Unix timestamp exceeds this maximum value, the casted value will overflow, leading to incorrect and potentially harmful behavior in the contract. This issue can significantly reduce the functional lifespan of a contract, as it becomes unreliable and potentially insecure once the timestamp exceeds the capacity of the casted integer type.

```solidity
Path: ./src/NativeVault.sol

253:        self.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);	// @audit-issue

464:            parentBeaconBlockRoot: _getParentBlockRoot(uint64(block.timestamp)),	// @audit-issue

470:        node.currentSnapshotTimestamp = uint64(block.timestamp);	// @audit-issue

473:        emit SnapshotCreated(nodeOwner, node.nodeAddress, uint64(block.timestamp), snapshot.parentBeaconBlockRoot);	// @audit-issue
```
[253](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L253-L253), [464](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L464-L464), [470](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L470-L470), [473](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L473-L473), 


```solidity
Path: ./src/Vault.sol

142:        state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);	// @audit-issue
```
[142](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L142-L142), 


```solidity
Path: ./src/entities/Operator.sol

71:            startTimestamp: uint48(block.timestamp),	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L71-L71), 


```solidity
Path: ./src/entities/SlasherLib.sol

104:            timestamp: uint96(block.timestamp),	// @audit-issue
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L104-L104), 


#### Recommendation

Avoid casting `block.timestamp` to smaller integer types in your Solidity contracts. Use `uint256` to store timestamp values to accommodate the increasing nature of Unix timestamps and ensure the contract remains functional in the long term. Regularly review and update your contracts to remove any unnecessary casting of `block.timestamp` that could lead to overflows and reduce the contract's lifespan. By doing so, you maintain the contract's reliability and integrity well into the future.

### Unsafe `uint` to `int` conversion
The `int` type in Solidity uses the [two's complement system](https://en.wikipedia.org/wiki/Two%27s_complement), so it is possible to accidentally overflow a very large `uint` to an `int`, even if they share the same number of bytes (e.g. a `uint256 number > type(uint128).max` will overflow a `int256` cast).

Consider using the [SafeCast](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/SafeCast.sol) library to prevent any overflows.


```solidity
Path: ./src/entities/NativeVaultLib.sol

140:            balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);	// @audit-issue: Variable `newBalanceWei` is type `uint256` and it is casted to `int256`

140:            balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);	// @audit-issue: Variable `prevBalanceWei` is type `uint256` and it is casted to `int256`
```
[140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L140-L140), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L140-L140), 


#### Recommendation

To prevent potential overflow issues when converting from `uint` to `int` in Solidity, consider using the SafeCast library. This library helps ensure safe type conversions and avoids unexpected behavior, especially when dealing with very large `uint` values that could overflow when cast to `int`.

### Consider using OpenZeppelin’s `SafeCast` library to prevent unexpected overflows when casting from various type int/uint values
In Solidity, when casting from `int` to `uint` or vice versa, there is a risk of unexpected overflow or underflow, especially when dealing with large values. To mitigate this risk and ensure safe type conversions, you can consider using OpenZeppelin’s `SafeCast` library. This library provides functions that check for overflow/underflow conditions before performing the cast, helping you prevent potential issues related to type conversion in your smart contracts.

```solidity
Path: ./src/NativeVault.sol

253:        self.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);	// @audit-issue

464:            parentBeaconBlockRoot: _getParentBlockRoot(uint64(block.timestamp)),	// @audit-issue

470:        node.currentSnapshotTimestamp = uint64(block.timestamp);	// @audit-issue

473:        emit SnapshotCreated(nodeOwner, node.nodeAddress, uint64(block.timestamp), snapshot.parentBeaconBlockRoot);	// @audit-issue

482:            int256 totalDeltaWei = int256(snapshot.nodeBalanceWei) + snapshot.balanceDeltaWei;	// @audit-issue

519:            _increaseBalance(_of, uint256(assets));	// @audit-issue

521:            _decreaseBalance(_of, uint256(-assets));	// @audit-issue
```
[253](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L253-L253), [464](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L464-L464), [470](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L470-L470), [473](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L473-L473), [482](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L482-L482), [519](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L519-L519), [521](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L521-L521), 


```solidity
Path: ./src/Vault.sol

142:        state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);	// @audit-issue
```
[142](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L142-L142), 


```solidity
Path: ./src/entities/Operator.sol

70:            nonce: uint48(nonce),	// @audit-issue

71:            startTimestamp: uint48(block.timestamp),	// @audit-issue
```
[70](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L70-L70), [71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L71-L71), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

24:        return bytes32(uint256(operatorStateSlot(operator)) + PENDING_STAKE_UPDATE_MAPPING_OFFSET);	// @audit-issue
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L24-L24), 


```solidity
Path: ./src/entities/SlasherLib.sol

104:            timestamp: uint96(block.timestamp),	// @audit-issue
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L104-L104), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

55:        n = uint64(uint256(lenum >> 192));	// @audit-issue

85:        uint256 index = (CONTAINER_IDX << (VALIDATOR_HEIGHT + 1)) | uint256(validatorIndex);	// @audit-issue

121:        uint256 balanceIndex = uint256(validatorIndex / 4);	// @audit-issue

134:        return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;	// @audit-issue

138:        return uint256(fromLittleEndianUint64(validatorFields[BALANCE_IDX])) * 1 gwei;	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L55-L55), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L85-L85), [121](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L121-L121), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L134-L134), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L138-L138), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

140:            balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);	// @audit-issue

164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue
```
[140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L140-L140), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L164-L164), 


#### Recommendation

To enhance the safety and reliability of your Solidity smart contracts, it is advisable to utilize OpenZeppelin’s `SafeCast` library when casting between `int` and `uint` types. Incorporating this library into your codebase will help prevent unexpected overflows and underflows during type conversion, reducing the risk of vulnerabilities and ensuring secure contract execution.

### Initializers can be front-run
Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment.


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


#### Recommendation

To mitigate the risk of initializers being front-run, ensure that they are only callable by a trusted entity, such as the deployer, or through a secure, multi-step initialization process. One approach is to use a constructor for initial setup, which is inherently protected against front-running. If a separate initializer is necessary, consider using a modifier that restricts the initializer function to be called only once by a predefined address, typically the deployer's address. Additionally, implement robust checks within the initializer to validate inputs and reject suspicious or unauthorized initialization attempts.

### External calls in an unbounded loop can result in a DoS
Consider limiting the number of iterations in loops that make external calls, as just a single one of them failing will result in a revert.

```solidity
Path: ./src/Querier.sol

30:            slots[i] = CoreStorageSlots.vaultPendingStakeUpdateSlot(operator, stakedVaults[i]);	// @audit-issue
```
[30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L30-L30), 


```solidity
Path: ./src/NativeVault.sol

153:            int256 balanceDeltaWei = self.validateSnapshotProof(	// @audit-issue

154:                nodeOwner, validatorDetails, balanceContainer.containerRoot, balanceProofs[i]	// @audit-issue

195:            totalRestakedWei += self.validateWithdrawalCredentials(	// @audit-issue

198:                beaconStateRootProof.beaconStateRoot,	// @audit-issue
```
[153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L153-L153), [154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L154-L154), [195](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L195-L195), [198](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L198-L198), 


```solidity
Path: ./src/entities/CoreLib.sol

136:                vaultConfigs[i].asset,	// @audit-issue

137:                vaultConfigs[i].name,	// @audit-issue

138:                vaultConfigs[i].symbol,	// @audit-issue

139:                vaultConfigs[i].extraData,	// @audit-issue

143:            self.operatorState[operator].addVault(vault);	// @audit-issue

144:            emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);	// @audit-issue
```
[136](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L136-L136), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L137-L137), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L138-L138), [139](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L139-L139), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L143-L143), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L144-L144), 


```solidity
Path: ./src/entities/SlasherLib.sol

51:            if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {	// @audit-issue

86:            earmarkedStakes[i] = Math.mulDiv(	// @audit-issue

87:                slashingMetadata.slashPercentagesWad[i],	// @audit-issue

88:                IKarakBaseVault(slashingMetadata.vaults[i]).totalAssets(),	// @audit-issue

89:                Constants.MAX_SLASHING_PERCENT_WAD	// @audit-issue

135:            IKarakBaseVault(queuedSlashing.vaults[i]).slashAssets(	// @audit-issue

136:                queuedSlashing.earmarkedStakes[i],	// @audit-issue

137:                self.assetSlashingHandlers[IKarakBaseVault(queuedSlashing.vaults[i]).asset()]	// @audit-issue
```
[51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L51-L51), [86](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L86-L86), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L87-L87), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L88-L88), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L89-L89), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L135-L135), [136](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L136-L136), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L137-L137), 


#### Recommendation

To mitigate the risk of Denial-of-Service (DoS) attacks in your Solidity code, it's important to limit the number of iterations in loops that involve external calls. A single failed external call in an unbounded loop can lead to a revert, causing disruptions in contract execution. Consider implementing safeguards, such as setting a maximum loop iteration count or employing strategies like batch processing, to reduce the impact of potential external call failures.

### Solidity version 0.8.20 might not work on all chains due to `PUSH0`
The Solidity version 0.8.20 employs the recently introduced PUSH0 opcode in the Shanghai EVM. This opcode might not be universally supported across all blockchain networks and Layer 2 solutions. Thus, as a result, it might be not possible to deploy solution with version 0.8.20 >= on some blockchains.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

The Solidity version 0.8.20 employs the recently introduced PUSH0 opcode in the Shanghai EVM. This opcode might not be universally supported across all blockchain networks and Layer 2 solutions. Thus, as a result, it might be not possible to deploy solution with version 0.8.20 >= on some blockchains.

It is recommended to verify whether solution can be deployed on particular blockchain with the Solidity version 0.8.20 >=. Whenever such deployment is not possible due to lack of PUSH0 opcode support and lowering the Solidity version is a must, it is strongly advised to review all feature changes and bugfixes in [Solidity releases](https://soliditylang.org/blog/category/releases/). Some changes may have impact on current implementation and may impose a necessity of maintaining another version of solution.

### Upgradeable contract is missing `__gap[..]` storage variable
Storage gaps are needed to not break storage layouts when adding new variables to base contracts. Listed contracts may not be inherited from but it is good practice to add it now rather than forgetting later.


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


#### Recommendation

When designing upgradeable contracts, it's important to include `__gap[..]` storage variables as storage gaps to prevent issues with storage layout changes when adding new variables to base contracts in the future. While the listed contracts may not be directly inherited from, it is a good practice to add `__gap[..]` storage variables now to ensure a robust and future-proof upgradeable contract design. This proactive approach helps avoid potential complications and storage layout conflicts in later stages of contract development.

### Contracts are designed to receive ETH but do not implement function for withdrawal
The following contracts can receive ETH but do not provide a function for withdrawal. This means that any ETH sent to these contracts will be permanently stuck, unable to be retrieved by the contract owner or any other party. Additionally, this issue can also apply to baseTokens, resulting in locked tokens and potential loss of funds.


```solidity
Path: ./src/SlashStore.sol

25:    receive() external payable {	// @audit-issue
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L25-L25), 


#### Recommendation

To prevent ETH and token lock-up and potential loss of funds, ensure that contracts designed to receive ETH or tokens implement a function for withdrawal. This function should allow contract owners and users to retrieve their funds when needed. Failure to provide a withdrawal mechanism can lead to locked assets and permanent loss, posing a significant risk to contract users and owners.

### `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()`
Use `abi.encode()` instead which will pad items to 32 bytes, which will [prevent hash collisions](https://docs.soliditylang.org/en/v0.8.13/abi-spec.html#non-standard-packed-mode) (e.g. `abi.encodePacked(0x123,0x456)` => `0x123456` => `abi.encodePacked(0x1,0x23456)`, but `abi.encode(0x123,0x456)` => `0x0...1230...456`). "Unless there is a compelling reason, `abi.encode` should be preferred". If there is only one argument to `abi.encodePacked()` it can often be cast to `bytes()` or `bytes32()` [instead](https://ethereum.stackexchange.com/questions/30912/how-to-compare-strings-in-solidity#answer-82739).
If all arguments are strings and or bytes, `bytes.concat()` should be used instead

```solidity
Path: ./src/entities/CoreLib.sol

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), 


#### Recommendation

To ensure the integrity of hash functions like `keccak256()` in Solidity, prefer using `abi.encode()` instead of `abi.encodePacked()` when dealing with dynamic types. `abi.encode()` pads items to 32 bytes, preventing hash collisions and enhancing security. Only use `abi.encodePacked()` when there is a compelling reason. If there's only one argument to `abi.encodePacked()`, consider casting it to `bytes()` or `bytes32()`. If all arguments are strings or bytes, use `bytes.concat()` for better clarity and reliability.

### Consider bounding input array length
If the number of for loop iterations is unbounded, then it may lead to the transaction to run out of gas. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to require() that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

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

84:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue

132:        for (uint256 i = 0; i < vaultConfigs.length; i++) {	// @audit-issue
```
[84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L84-L84), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L132-L132), 


```solidity
Path: ./src/entities/SlasherLib.sol

50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {	// @audit-issue

85:        for (uint256 i = 0; i < slashingMetadata.vaults.length; ++i) {	// @audit-issue

134:        for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {	// @audit-issue
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L50-L50), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L85-L85), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L134-L134), 


#### Recommendation

Implement a check at the beginning of your Solidity functions to enforce a maximum length on input arrays. Use a `require()` statement to validate that the length of any input array does not exceed a predetermined limit, which should be chosen based on the function's complexity and typical gas usage. This ensures that the function will not attempt to process more data than it can handle within reasonable gas limits, thereby preventing out-of-gas errors and improving the overall user experience. Clearly document this behavior and the rationale behind the chosen array size limit to inform users and developers interacting with your contract.

### Possible loss of precision
Division by large numbers may result in precision loss due to rounding down, or even the result being erroneously equal to zero. Consider adding checks on the numerator to ensure precision loss is handled appropriately.


```solidity
Path: ./src/entities/SlasherLib.sol

86:            earmarkedStakes[i] = Math.mulDiv(	// @audit-issue
```
[86](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L86-L86), 


#### Recommendation

Incorporate strategies in your Solidity contracts to mitigate precision loss in division operations. This can include:
1. Performing checks on the numerator and denominator to ensure they are within a reasonable range to avoid significant rounding errors.
2. Considering the use of fixed-point arithmetic libraries or scaling factors to handle divisions with higher precision.
3. Clearly documenting any inherent limitations of your division logic and providing guidelines for inputs to minimize unexpected behavior.
Always thoroughly test division operations under various scenarios to ensure that the outcomes are consistent with your contract's intended logic and accuracy requirements.

### Library function isn't `internal` or `private`
In a library, using an external or public visibility means that we won't be going through the library with a DELEGATECALL but with a CALL. This changes the context and should be done carefully.

```solidity
Path: ./src/entities/Operator.sol

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

150:    function registerOperatorToDSS(	// @audit-issue

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)	// @audit-issue

181:    function unregisterOperatorFromDSS(	// @audit-issue

224:    function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)	// @audit-issue
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L150-L150), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L173), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L181-L181), [224](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L224-L224), 


```solidity
Path: ./src/entities/CoreLib.sol

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue

118:    function deployVaults(	// @audit-issue
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L118), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue
```
[27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

94:    function requestSlashing(	// @audit-issue

126:    function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue

153:    function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue

174:    function setDSSMaxSlashablePercentageWad(	// @audit-issue
```
[94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L126-L126), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L153-L153), [170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), [174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L174-L174), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue
```
[141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), 


```solidity
Path: ./src/utils/CommonUtils.sol

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Carefully assess the intended use of functions within your libraries and opt for `internal` or `private` visibility unless there's a specific reason to expose them via `external` or `public`. This practice encourages the use of `DELEGATECALL` where appropriate, maintaining the execution context of the calling contract and ensuring consistent access to storage variables.

### Floating Pragma
A "floating pragma" in Solidity refers to the practice of using a pragma statement that does not specify a fixed compiler version but instead allows the contract to be compiled with any compatible compiler version. This issue arises when pragma statements like `pragma solidity ^0.8.0;` are used without a specific version number, allowing the contract to be compiled with the latest available compiler version. This can lead to various compatibility and stability issues.


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

Consider locking the pragma version whenever possible and avoid using a floating pragma in the final deployment. [Consider known bugs](https://github.com/ethereum/solidity/releases) for the compiler version that is chosen.

### Ownership Irrevocability Vulnerability
The smart contract under inspection inherits from the `Ownable` library, which provides basic authorization control functions, simplifying the implementation of user permissions. However, the contract does not provide a mechanism to transfer ownership to another address or account, and it retains the default `renounceOwnership` function from `Ownable`.  
Given this, once the owner renounces ownership using the `renounceOwnership` function, the contract becomes ownerless. As evidenced in the provided transaction logs, after the `renounceOwnership` function is called, attempts to call functions that require owner permissions fail with the error message: `"Ownable: caller is not the owner."`  
This state renders the contract's adjustable parameters immutable and potentially makes the contract useless for any future administrative changes that might be necessary.

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
Path: ./src/SlashingHandler.sol

16:contract SlashingHandler is Initializable, Ownable, ISlashingHandler {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L16-L16), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


#### Recommendation


To mitigate this vulnerability:
* Override the renounceOwnership function to revert transactions: By overriding this function to simply revert any transaction, it will become impossible for the contract owner to unintentionally (or intentionally) render the contract ownerless and thus immutable.
* Implement an ownership transfer function: While the Ownable library does provide a transferOwnership function, if this is not present or has been removed from the current contract, it should be re-implemented to ensure there is a way to transfer ownership in future scenarios.


### Unneeded initializations of integer variable to `0`.
In Solidity, it is common practice to initialize variables with default values when declaring them. However, initializing integer variables to `0` when they are not subsequently used in the code can lead to unnecessary gas consumption and code clutter. This issue points out instances where such initializations are present but serve no functional purpose.

```solidity
Path: ./src/Querier.sol

29:        for (uint256 i = 0; i < stakedVaults.length; i++) {	// @audit-issue

33:        uint256 count = 0;	// @audit-issue

34:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue

38:        uint256 latestIndex = 0;	// @audit-issue

39:        for (uint256 i = 0; i < results.length; i++) {	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L29-L29), [33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L33-L33), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L34-L34), [38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L38-L38), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L39-L39), 


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
Path: ./src/entities/BeaconProofsLib.sol

14:    uint256 internal constant PUBKEY_IDX = 0;	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L14-L14), 


```solidity
Path: ./src/entities/MerkleProofs.sol

147:        for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue

155:            for (uint256 i = 0; i < numNodesInLayer; i++) {	// @audit-issue
```
[147](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L147-L147), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L155-L155), 


```solidity
Path: ./src/utils/CommonUtils.sol

42:        for (uint256 i = 0; i < arr.length - 1; i++) {	// @audit-issue
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L42-L42), 


#### Recommendation


It is recommended not to initialize integer variables to `0` to save some Gas.


### The `nonReentrant modifier` should occur before all other modifiers
In Solidity, the order in which modifiers are applied to a function can significantly impact the function's behavior and security. The `nonReentrant` modifier is crucial for preventing reentrancy attacks, a common vulnerability in smart contracts. This modifier should be the first in the list of applied modifiers to ensure that the reentrancy check is performed before any other logic in the function. Placing `nonReentrant` after other modifiers could potentially lead to security weaknesses, as other modifiers might perform state changes or external calls before the reentrancy protection takes effect. Therefore, correct positioning of the `nonReentrant` modifier is essential for maintaining the integrity and security of the function and, by extension, the entire contract.


```solidity
Path: ./src/NativeNode.sol

39:    function withdraw(address to, uint256 weiAmount)
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L39), 


```solidity
Path: ./src/Core.sol

97:    function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)

161:    function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)

220:    function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)
```
[100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L97-L97), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L161-L161), [223](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L220-L220), [238](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L235), 


```solidity
Path: ./src/NativeVault.sol

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
```
[302](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L299), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)

110:    function mint(uint256 shares, address to)

125:    function startRedeem(uint256 shares, address beneficiary)

331:    function withdraw(uint256 assets, address to, address owner)

348:    function redeem(uint256 shares, address to, address owner)
```
[82](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L78), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L110-L110), [128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L125-L125), [335](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [352](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


#### Recommendation

To ensure the effectiveness of the `nonReentrant` modifier in protecting against reentrancy, it should be placed as the first modifier in a function's list of modifiers, before all other modifiers. This helps prevent reentrancy attacks from being triggered by other modifiers.

### `else`-block not required
One level of nesting can be removed by not having an `else` block when the `if`-block returns, and `if (foo) { return 1; } else { return 2; }` becomes `if (foo) { return 1; } return 2;`


```solidity
Path: ./src/NativeVault.sol

418:        if (success && result.length > 0) {
419:            return abi.decode(result, (bytes32));
420:        } else {	// @audit-issue
421:            revert BeaconRootFetchError();
422:        }
```
[420](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L418-L422), 


#### Recommendation

Consider simplifying code by removing unnecessary `else` blocks when the `if` block returns. You can achieve cleaner and more concise code by directly returning a value after the `if` block instead of using an `else` block for a subsequent return statement.

### Unused import
The identifier is imported but never used within the file.

```solidity
Path: ./src/NativeNode.sol

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Initializable not used in the contract.
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L8-L8), 


```solidity
Path: ./src/Querier.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue: Ownable not used in the contract.
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L4-L4), 


```solidity
Path: ./src/NativeVault.sol

7:import {SafeTransferLib} from "solady/src/utils/SafeTransferLib.sol";	// @audit-issue: SafeTransferLib not used in the contract.

11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Initializable not used in the contract.
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L7-L7), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L11-L11), 


```solidity
Path: ./src/entities/CoreLib.sol

4:import {Create2} from "@openzeppelin/contracts/utils/Create2.sol";	// @audit-issue: Create2 not used in the contract.
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L4-L4), 


```solidity
Path: ./src/entities/HookLib.sol

4:import {Constants} from "../interfaces/Constants.sol";	// @audit-issue: Constants not used in the contract.
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L4-L4), 


#### Recommendation

Regularly review your Solidity code to remove unused imports. This practice declutters the codebase, making it easier to understand and maintain. In addition, consider using tools or IDE features that can automatically detect and highlight unused imports for cleanup. Keeping imports limited to only what is necessary helps maintain a clear understanding of the contract's dependencies and reduces potential confusion for developers working on or reviewing the code.

### Payable Usage Is Unnecessary
The use of the `payable` keyword to convert addresses before sending Ether in Solidity can sometimes be redundant, particularly when the target address (`to`) could be defined as `payable` in the function parameters. This redundancy not only adds unnecessary complexity to the code but also obscures the function's intention of transferring Ether to a specific address. Defining the address as `payable` from the outset clarifies that the function is intended to perform Ether transfers and ensures that the address type is correctly specified for such transactions.

```solidity
Path: ./src/NativeNode.sol

45:        Address.sendValue(payable(to), weiAmount);	// @audit-issue: variable `to` could be defined in the function parameters as `payable to` instead of using `payable` function.
```
[45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L45-L45), 


```solidity
Path: ./src/SlashStore.sol

33:        Address.sendValue(payable(to), weiAmount);	// @audit-issue: variable `to` could be defined in the function parameters as `payable to` instead of using `payable` function.
```
[33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L33-L33), 


#### Recommendation

Review your contract's functions to identify instances where the `payable` keyword is used to convert addresses just before making a call to transfer Ether. Refactor these functions by specifying the `payable` keyword in the function parameters for addresses intended to receive Ether. This practice enhances code clarity, reduces unnecessary conversions, and explicitly indicates which addresses are expected to participate in Ether transactions.

Example before refactoring:
```solidity
function transferEther(address to, uint256 amount) external {
    (bool success, ) = payable(to).call{value: amount}("");
    require(success, "Transfer failed.");
}
```

Example after refactoring:
```solidity
function transferEther(address payable to, uint256 amount) external {
    (bool success, ) = to.call{value: amount}("");
    require(success, "Transfer failed.");
}
```

This approach streamlines the function's design and makes the contract's intentions regarding Ether transfers more transparent.


### Excessive Authorization in Contract Functions
A contract where a high percentage of functions require authorization (e.g., restricted to the contract owner or specific roles) may indicate over-centralization or excessive control. This could limit the contract's flexibility, reduce trust among users, and potentially create bottleneck points that could be exploited or become failure points. While some level of control is necessary for administrative purposes, overly restrictive access can detract from the decentralized nature of blockchain applications and concentrate too much power in the hands of a few.

```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `unpause`, `withdraw`, `pause`
	List of functions that require authorization: `unpause`, `withdraw`, `pause`
	List of functions that doesn't require authorization: None
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `withdraw`
	List of functions that require authorization: `withdraw`
	List of functions that doesn't require authorization: None
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


#### Recommendation

Make contract more decentralized.

### `public` functions not called by the contract should be declared `external` instead
In Solidity, function visibility is an important aspect that determines how and where a function can be called from. Two commonly used visibilities are `public` and `external`. A `public` function can be called both from other functions inside the same contract and from outside transactions, while an `external` function can only be called from outside the contract.
A potential pitfall in smart contract development is the misuse of the `public` keyword for functions that are only meant to be accessed externally. When a function is not used internally within a contract and is only intended for external calls, it should be labeled as `external` rather than `public`. Using `public` unnecessarily can introduce potential vulnerabilities and also make the contract consume more gas than required. This is because `public` functions have to add additional code to handle both internal and external calls, while `external` functions can be more optimized since they only handle external calls.


```solidity
Path: ./src/entities/Pauser.sol

63:    function pausedMap() public view virtual returns (uint256) {	// @audit-issue
```
[63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L63-L63), 


```solidity
Path: ./src/Core.sol

288:    function isAssetAllowlisted(address asset) public view returns (bool) {	// @audit-issue

294:    function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {	// @audit-issue

302:    function isOperatorRegisteredToDSS(address operator, IDSS dss) public view returns (bool) {	// @audit-issue

318:    function implementation(address vault) public view returns (address) {	// @audit-issue

358:    function getDssMaxSlashablePercentageWad(IDSS dss) public view returns (uint256 slashablePercentageWad) {	// @audit-issue
```
[288](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L288-L288), [294](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L294-L294), [302](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L302-L302), [318](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L318-L318), [358](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L358-L358), 


```solidity
Path: ./src/utils/ExtSloads.sol

9:    function extSloads(bytes32[] calldata slots) public view virtual returns (bytes32[] memory res) {	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L9-L9), 


```solidity
Path: ./src/NativeVault.sol

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)	// @audit-issue

631:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue
```
[355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [363](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L363), [631](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L631-L631), 


```solidity
Path: ./src/Vault.sol

237:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue

243:    function getNextWithdrawNonce(address staker) public view returns (uint256) {	// @audit-issue

250:    function isWithdrawalPending(address staker, uint256 _withdrawNonce) public view returns (bool) {	// @audit-issue

258:    function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)	// @audit-issue
```
[237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L237-L237), [243](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L243-L243), [250](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L250-L250), [258](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L258-L258), 


```solidity
Path: ./src/entities/SlasherLib.sol

174:    function setDSSMaxSlashablePercentageWad(	// @audit-issue
```
[174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L174-L174), 


#### Recommendation

To optimize gas usage and improve code clarity, declare functions that are not called internally within the contract and are intended for external access as `external` rather than `public`. This ensures that these functions are only callable externally, reducing unnecessary gas consumption and potential security risks.

### `Internal` Functions Not Called by The Contract Should Be Removed
In Solidity, functions labeled as `internal` are meant to be used only within the contract in which they're defined or in derived contracts. They cannot be accessed from external transactions. While `internal` functions offer modularity and can be leveraged to break down complex logic, it's essential to monitor their relevance during the contract's lifecycle.

A common oversight during smart contract development is the presence of `internal` functions that remain within the contract code but are never called by any other function or part of the contract. These redundant functions occupy space, make the contract's bytecode longer, and, as a consequence, increase the contract deployment cost. Moreover, they can add unnecessary complexity to the code, making it harder to read, maintain, and audit.


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue

43:    function addVault(State storage operatorState, IKarakBaseVault vault) internal {	// @audit-issue

143:    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L43-L43), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L143-L143), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue

153:    function allowlistVaultImpl(Storage storage self, address implementation) internal {	// @audit-issue

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L40), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L153-L153), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L29), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue

110:    function validateSnapshotProof(	// @audit-issue

146:    function validateWithdrawalCredentials(	// @audit-issue
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L110), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L146), 


#### Recommendation

To maintain clean and efficient code, review the contract's `internal` functions to identify and remove any that are no longer in use or serve no purpose. Removing unused `internal` functions can improve code readability, reduce deployment costs, and enhance the overall quality of the smart contract.

### Functions contain the same code
The functions below have the same implementation as is seen in other files. The functions should be refactored into functions of a common base contract.

```solidity
Path: ./src/NativeVault.sol

322:    function pause(uint256 map) external onlyOwner {	// @audit-issue: Seen on line 51 of ./src/NativeNode.sol

328:    function unpause(uint256 map) external onlyOwner {	// @audit-issue: Seen on line 57 of ./src/NativeNode.sol
```
[322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L322-L322), [328](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L328-L328), 


```solidity
Path: ./src/Vault.sol

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue: Seen on line 619 of ./src/NativeVault.sol

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue: Seen on line 623 of ./src/NativeVault.sol

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue: Seen on line 615 of ./src/NativeVault.sol

237:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue: Seen on line 631 of ./src/NativeVault.sol

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue: Seen on line 611 of ./src/NativeVault.sol

303:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue: Seen on line 409 of ./src/NativeVault.sol
```
[222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L237-L237), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [303](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L303-L303), 


#### Recommendation

Identify and consolidate duplicated code blocks in Solidity contracts into reusable modifiers or functions. This approach streamlines the contract by eliminating redundancy, thereby improving clarity, maintainability, and potentially reducing gas costs. For common checks, consider using modifiers for concise and consistent enforcement of conditions. For reusable logic, encapsulate it in functions to avoid code duplication and simplify future updates or bug fixes.

### `if`-statement can be converted to a ternary
The code can be made more compact while also increasing readability by converting the following `if`-statements to ternaries (e.g. `foo += (x > y) ? a : b`)

```solidity
Path: ./src/Core.sol

322:        if (vaultImplOverride == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) {	// @audit-issue
323:            return self.vaultImpl;
324:        }
```
[322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L322-L324), 


```solidity
Path: ./src/NativeVault.sol

278:        if (startedWithdrawal.assets > withdrawableAssets) {	// @audit-issue
279:            startedWithdrawal.assets = withdrawableAssets;
280:        }

311:        if (totalAssetsToSlash > self.totalAssets) {	// @audit-issue
312:            totalAssetsToSlash = self.totalAssets;
313:        }

443:        if (node.nodeAddress.balance < node.withdrawableCreditedNodeETH) {	// @audit-issue
444:            node.withdrawableCreditedNodeETH = node.nodeAddress.balance;
445:        }

520:        } else if (assets < 0) {	// @audit-issue
521:            _decreaseBalance(_of, uint256(-assets));
522:        } else {
523:            return;
524:        }
```
[278](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L278-L280), [311](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L311-L313), [443](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L443-L445), [520](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L520-L524), 


```solidity
Path: ./src/entities/Operator.sol

104:        if (toStake) {	// @audit-issue
105:            operatorState.vaultStakedInDssMap[dss].add(vault);
106:        } else {
107:            operatorState.vaultStakedInDssMap[dss].remove(vault);
108:        }
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L104-L108), 


```solidity
Path: ./src/entities/CoreLib.sol

127:        if (implementation == address(0)) {	// @audit-issue
128:            // Allows us to change all the standard vaults to a new implementation
129:            implementation = Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG;
130:        }
```
[127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L127-L130), 


```solidity
Path: ./src/utils/CommonUtils.sol

23:        if (lastUnsortedInd > left) {	// @audit-issue
24:            sort(arr, left, lastUnsortedInd - 1);
25:        }
```
[23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L23-L25), 


#### Recommendation

Consider using single line if statements as ternary.

### Custom error has no error details
Consider adding parameters to the error to indicate which user or values caused the failure

```solidity
Path: ./src/entities/Pauser.sol

28:    error EnforcedPause();	// @audit-issue

32:    error AttemptedUnpauseWhilePausing();	// @audit-issue

34:    error AttemptedPauseWhileUnpausing();	// @audit-issue
```
[28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L28-L28), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L32-L32), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L34-L34), 


#### Recommendation

When defining custom errors, consider adding parameters or error details that provide information about the specific conditions or inputs that caused the error. Including error details can make debugging and troubleshooting easier by providing context on the cause of the failure.

### Redundant Mathematical Operation
Mathematical operations like multiplication with 1 or adding zero should be removed.

```solidity
Path: ./src/entities/BeaconProofsLib.sol

134:        return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;	// @audit-issue: Multiplication with `1` is redundant.

138:        return uint256(fromLittleEndianUint64(validatorFields[BALANCE_IDX])) * 1 gwei;	// @audit-issue: Multiplication with `1` is redundant.
```
[134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L134-L134), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L138-L138), 


#### Recommendation

Remove redundant mathematical operations.

### Consider moving `msg.sender` checks to `modifier`s
If some functions are only allowed to be called by some specific users, consider using a modifier instead of checking with a require statement, especially if this check is done in multiple functions.

```solidity
Path: ./src/NativeVault.sol

238:        if (weiAmount > withdrawableWei(msg.sender) - self.nodeOwnerToWithdrawAmount[msg.sender]) {
239:            revert WithdrawMoreThanMax();	// @audit-issue
```
[239](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L238-L239), 


#### Recommendation

Consider refactoring your code by moving `msg.sender` checks to modifiers when certain functions are only allowed to be called by specific users. This approach can enhance code readability, reduce redundancy, and make it easier to maintain access control logic.

### Constants in comparisons should appear on the left side
Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html)

```solidity
Path: ./src/SlashingHandler.sol

53:        if (amount == 0) revert ZeroAmount();	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L53-L53), 


```solidity
Path: ./src/NativeVault.sol

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue

271:        if (startedWithdrawal.start == 0) revert WithdrawalNotFound();	// @audit-issue

451:        if (node.currentSnapshotTimestamp != 0) revert PendingIncompleteSnapshot();	// @audit-issue

461:        if (revertIfNoBalanceChange && nodeBalanceWei == 0) revert NoBalanceUpdateToSnapshot();	// @audit-issue

481:        if (snapshot.remainingProofs == 0) {	// @audit-issue
```
[140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L271-L271), [451](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L451-L451), [461](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L461-L461), [481](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L481-L481), 


```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue

100:        if (assets == 0) revert ZeroAmount();	// @audit-issue

117:        if (shares == 0) revert ZeroShares();	// @audit-issue

131:        if (shares == 0) revert ZeroShares();	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L100-L100), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), [131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L131-L131), 


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
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L8-L8), [41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L41-L41), 


#### Recommendation

To prevent typo bugs and improve code readability, it's advisable to place constants on the left side of comparisons. This coding practice helps catch accidental assignment (=) instead of comparison (==) and enhances code quality.

### Convert duplicated codes to modifier/functions
Duplicated code in Solidity contracts, especially when repeated across multiple functions, can lead to inefficiencies and increased maintenance challenges. It not only bloats the contract but also makes it harder to implement changes consistently across the codebase. By identifying common patterns or checks that are repeated and abstracting them into modifiers or separate functions, the code can be made more concise, readable, and maintainable. This practice not only reduces the overall bytecode size, potentially lowering deployment and execution costs, but also enhances the contract's reliability by ensuring consistency in how these common checks or operations are executed.

```solidity
Path: ./src/NativeVault.sol

601:        shares = shares;	// @audit-issue: Exactly same copy pasted functionality between lines: `{'585->588'}`
602:        assets = assets;
603:
604:        revert NotImplemented();
```
[601](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L601-L604), 


#### Recommendation

Identify and consolidate duplicated code blocks in Solidity contracts into reusable modifiers or functions. This approach streamlines the contract by eliminating redundancy, thereby improving clarity, maintainability, and potentially reducing gas costs. For common checks, consider using modifiers for concise and consistent enforcement of conditions. For reusable logic, encapsulate it in functions to avoid code duplication and simplify future updates or bug fixes.

### Style guide: Function ordering does not follow the Solidity style guide
According to the Solidity [style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

```solidity
Path: ./src/SlashStore.sol

25:    receive() external payable {	// @audit-issue
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L25-L25), 


```solidity
Path: ./src/Core.sol

318:    function implementation(address vault) public view returns (address) {	// @audit-issue: implementation should come before than isAssetAllowlisted
```
[318](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L318-L318), 


```solidity
Path: ./src/NativeVault.sol

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue: getNodeOwner should come before than withdrawableWei
```
[371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), 


```solidity
Path: ./src/Vault.sol

94:    function deposit(uint256 assets, address to, uint256 minSharesOut)	// @audit-issue
```
[94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L94-L94), 


```solidity
Path: ./src/entities/Operator.sol

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), 


```solidity
Path: ./src/entities/CoreLib.sol

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue
```
[27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

94:    function requestSlashing(	// @audit-issue
```
[94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue: getPubkeyHash should come before than getEffectiveBalanceWei
```
[141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), 


```solidity
Path: ./src/entities/Pauser.sol

36:    function __Pauser_init() internal onlyInitializing {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L36-L36), 


```solidity
Path: ./src/utils/CommonUtils.sol

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/latest/style-guide.html).

### Style guide: Contract does not follow the Solidity style guide's suggested layout ordering
The [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#order-of-layout) says that, within a contract, the ordering should be 1) Type declarations, 2) State variables, 3) Events, 4) Errors, 5) Modifiers, and 6) Functions, but the contract(s) below do not follow this ordering


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue : Order layout of this contract is not correct. It should be like this: 
	1 -> using NativeVaultLib
	2 -> STATE_SLOT
	3 -> CONFIG_SLOT
	4 -> nodeExists
	5 -> constructor
	6 -> initialize
	7 -> changeNodeImplementation
	8 -> createNode
	9 -> startSnapshot
	10 -> validateSnapshotProofs
	11 -> validateWithdrawalCredentials
	12 -> validateExpiredSnapshot
	13 -> startWithdrawal
	14 -> finishWithdrawal
	15 -> slashAssets
	16 -> pause
	17 -> unpause
	18 -> pauseNode
	19 -> unpauseNode
	20 -> withdrawableWei
	21 -> activeValidatorCount
	22 -> getNextWithdrawNonce
	23 -> isWithdrawalPending
	24 -> getQueuedWithdrawal
	25 -> getNodeOwner
	26 -> getValidatorDetails
	27 -> lastSnapshotTimestamp
	28 -> currentSnapshotTimestamp
	29 -> currentSnapshot
	30 -> _state
	31 -> _config
	32 -> _getParentBlockRoot
	33 -> _transferToSlashStore
	34 -> _startSnapshot
	35 -> _updateSnapshot
	36 -> _increaseBalance
	37 -> _decreaseBalance
	38 -> _updateBalance
	39 -> transfer
	40 -> transferFrom
	41 -> deposit
	42 -> mint
	43 -> withdraw
	44 -> redeem
	45 -> previewDeposit
	46 -> previewRedeem
	47 -> totalAssets
	48 -> decimals
	49 -> asset
	50 -> name
	51 -> symbol
	52 -> implementation
	53 -> vaultConfig

```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue : Order layout of this contract is not correct. It should be like this: 
	1 -> using VaultLib
	2 -> VERSION
	3 -> STATE_SLOT
	4 -> CONFIG_SLOT
	5 -> onlyCore
	6 -> constructor
	7 -> initialize
	8 -> deposit
	9 -> deposit
	10 -> mint
	11 -> startRedeem
	12 -> finishRedeem
	13 -> slashAssets
	14 -> pause
	15 -> unpause
	16 -> name
	17 -> symbol
	18 -> asset
	19 -> vaultConfig
	20 -> getNextWithdrawNonce
	21 -> isWithdrawalPending
	22 -> getQueuedWithdrawal
	23 -> totalAssets
	24 -> owner
	25 -> decimals
	26 -> extSloads
	27 -> _state
	28 -> _config
	29 -> _storage
	30 -> _underlyingDecimals
	31 -> withdraw
	32 -> redeem

```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue : Order layout of this contract is not correct. It should be like this: 
	1 -> PAUSER_STORAGE_SLOT
	2 -> Paused
	3 -> Unpaused
	4 -> EnforcedPause
	5 -> EnforcedPauseFunction
	6 -> AttemptedUnpauseWhilePausing
	7 -> AttemptedPauseWhileUnpausing
	8 -> whenNotPaused
	9 -> whenFunctionNotPaused
	10 -> _getPauserStorage
	11 -> __Pauser_init
	12 -> __Pauser_init_unchained
	13 -> paused
	14 -> paused
	15 -> pausedMap
	16 -> _pause
	17 -> _unpause

```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### Duplicated `require()`/`revert()` checks should be refactored to a modifier or function
In Solidity contracts, it's common to encounter duplicated `require()` or `revert()` statements across multiple functions. These statements are crucial for validating conditions and ensuring contract integrity. However, repeated checks can lead to code redundancy, making the contract larger and more difficult to maintain. This redundancy can be streamlined by encapsulating the repeated logic in a modifier or a dedicated function. By doing so, the code becomes more concise, easier to audit, and more gas-efficient. Furthermore, centralizing the validation logic in a single location makes the codebase more adaptable to changes and reduces the risk of inconsistencies or errors in future updates.

```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue: Same if statement in line(s): ['100']

117:        if (shares == 0) revert ZeroShares();	// @audit-issue: Same if statement in line(s): ['131']
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), 


```solidity
Path: ./src/entities/SlasherLib.sol

128:        if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();	// @audit-issue: Same if statement in line(s): ['155']
```
[128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L128-L128), 


#### Recommendation

Consolidate repeated `require()` or `revert()` checks in Solidity by creating a modifier or a separate function. Apply this modifier to all functions requiring the same validation, or call the function at the beginning of each relevant function. This refactoring enhances contract efficiency, maintainability, and consistency, while potentially reducing gas costs associated with deploying and executing redundant code.

### Duplicate import statements
Contracts often depend on libraries and other contracts to modularize code and reuse functionalities. However, redundant imports occur when a contract imports a library or another contract that is already imported by one of its dependencies. This redundancy does not impact the compiled bytecode but can clutter the codebase, making it harder to understand the direct dependencies of each contract. Simplifying imports by removing these redundancies enhances code readability and maintainability.

```solidity
Path: ./src/NativeNode.sol

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Same library is also imported on: `['Pauser']`, at lines: `[5]`
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L8-L8), 


```solidity
Path: ./src/SlashingHandler.sol

7:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue: Same library is also imported on: `['ISlashingHandler']`, at lines: `[4]`
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L7-L7), 


```solidity
Path: ./src/Core.sol

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Same library is also imported on: `['Pauser']`, at lines: `[5]`

18:import {Constants} from "./interfaces/Constants.sol";	// @audit-issue: Same library is also imported on: `['Core']`, at lines: `[24]`
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L8-L8), [18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L18-L18), 


```solidity
Path: ./src/NativeVault.sol

11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Same library is also imported on: `['Pauser']`, at lines: `[5]`
```
[11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L11-L11), 


```solidity
Path: ./src/Vault.sol

10:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue: Same library is also imported on: `['ISlashingHandler']`, at lines: `[4]`

11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue: Same library is also imported on: `['Pauser']`, at lines: `[5]`
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L11-L11), 


#### Recommendation

Review your Solidity contracts and eliminate duplicate import statements. Ensure each file is imported only once where it's needed. If you find the same import statement across multiple files, consider whether you can restructure your code to centralize common logic or dependencies, potentially through base contracts or libraries. Regularly conduct code audits or utilize linters and other static analysis tools to identify and resolve duplicate imports, thereby enhancing the clarity, structure, and security of your Solidity codebase.

### Adding a return statement when the function defines a named return variable, is redundant
Once the return variable has been assigned (or has its default value), there is no need to explicitly return it at the end of the function, since it's returned automatically.

```solidity
Path: ./src/Core.sol

331:    function getOperatorVaults(address operator) external view returns (address[] memory vaults) {
332:        return _self().operatorState[operator].getVaults();	// @audit-issue
333:    }
```
[332](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L331-L333), 


```solidity
Path: ./src/NativeVault.sol

228:    function startWithdrawal(address to, uint256 weiAmount)
229:        external
230:        nonReentrant
231:        nodeExists(msg.sender)
232:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_START_WITHDRAWAL)
233:        returns (bytes32 withdrawalKey)
234:    {
235:        // TODO: make more recent snapshot compulsory
236:        NativeVaultLib.Storage storage self = _state();
237:        NativeVaultLib.NativeNode storage node = self.ownerToNode[msg.sender];
238:        if (weiAmount > withdrawableWei(msg.sender) - self.nodeOwnerToWithdrawAmount[msg.sender]) {
239:            revert WithdrawMoreThanMax();
240:        }
241:        self.nodeOwnerToWithdrawAmount[msg.sender] += weiAmount;
242:
243:        if (block.timestamp >= node.lastSnapshotTimestamp + Constants.SNAPSHOT_EXPIRY) {
244:            revert SnapshotExpired();
245:        }
246:
247:        withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++);
248:        address nodeOwner = msg.sender;
249:
250:        self.withdrawalMap[withdrawalKey].to = to;
251:        self.withdrawalMap[withdrawalKey].assets = weiAmount;
252:        self.withdrawalMap[withdrawalKey].nodeOwner = nodeOwner;
253:        self.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
254:
255:        emit StartedWithdraw(nodeOwner, _config().operator, withdrawalKey, weiAmount, to);
256:
257:        return withdrawalKey;	// @audit-issue
258:    }

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
300:        external
301:        onlyOwner
302:        nonReentrant
303:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_SLASHER)
304:        returns (uint256 transferAmount)
305:    {
306:        NativeVaultLib.Storage storage self = _state();
307:
308:        if (slashingHandler != self.slashStore) revert NotSlashStore();
309:
310:        // avoid negative totalAssets if slashing amount is greater than totalAssets
311:        if (totalAssetsToSlash > self.totalAssets) {
312:            totalAssetsToSlash = self.totalAssets;
313:        }
314:
315:        self.totalAssets -= totalAssetsToSlash;
316:        emit Slashed(totalAssetsToSlash);
317:        return totalAssetsToSlash;	// @audit-issue
318:    }
```
[257](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L228-L258), [317](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L318), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)
79:        public
80:        override(ERC4626, IVault)
81:        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
82:        nonReentrant
83:        returns (uint256 shares)
84:    {
85:        if (assets == 0) revert ZeroAmount();
86:        return super.deposit(assets, to);	// @audit-issue
87:    }
```
[86](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L87), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {
55:        n = uint64(uint256(lenum >> 192));
56:        return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)	// @audit-issue
57:            | ((0x000000FF00000000 & n) >> 8) | ((0x00000000FF000000 & n) << 8) | ((0x0000000000FF0000 & n) << 24)
58:            | ((0x000000000000FF00 & n) << 40) | ((0x00000000000000FF & n) << 56);
59:    }

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)
115:        internal
116:        view
117:        returns (uint256 validatorBalanceWei)
118:    {
119:        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();
120:
121:        uint256 balanceIndex = uint256(validatorIndex / 4);
122:
123:        if (
124:            !Merkle.verifyInclusionSha256({
125:                proof: proof.proof,
126:                root: balanceRoot,
127:                leaf: proof.balanceRoot,
128:                index: balanceIndex
129:            })
130:        ) revert InvalidBalanceProof();
131:
132:        /// Extract the individual validator's balance from the `balanceRoot`
133:        uint256 bitShiftAmount = (validatorIndex % 4) * 64;
134:        return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;	// @audit-issue
135:    }
```
[56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L59), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L135), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

110:    function validateSnapshotProof(
111:        Storage storage self,
112:        address nodeOwner,
113:        ValidatorDetails memory validatorDetails,
114:        bytes32 balanceRoot,
115:        BeaconProofs.BalanceProof calldata proof
116:    ) internal returns (int256 balanceDeltaWei) {
117:        address nodeAddress = self.ownerToNode[nodeOwner].nodeAddress;
118:        uint64 timestamp = self.ownerToNode[nodeOwner].currentSnapshotTimestamp;
119:
120:        uint40 validatorIndex = validatorDetails.validatorIndex;
121:        uint256 prevBalanceWei = validatorDetails.restakedBalanceWei;
122:        uint256 newBalanceWei = BeaconProofs.validateBalance(balanceRoot, validatorIndex, proof);
123:
124:        validatorDetails.restakedBalanceWei = newBalanceWei;
125:        validatorDetails.lastBalanceUpdateTimestamp = timestamp;
126:
127:        if (newBalanceWei == 0) {
128:            self.ownerToNode[nodeOwner].activeValidatorCount--;
129:            validatorDetails.status = ValidatorStatus.WITHDRAWN;
130:
131:            emit ValidatorWithdrawn(nodeOwner, nodeAddress, timestamp, validatorIndex);
132:        }
133:        self.ownerToNode[nodeOwner].validatorPubkeyHashToDetails[proof.pubkeyHash] = validatorDetails;
134:
135:        emit SnapshotValidator(nodeOwner, nodeAddress, timestamp, validatorIndex);
136:
137:        if (newBalanceWei != prevBalanceWei) {
138:            emit ValidatorBalanceChanged(nodeOwner, nodeAddress, validatorIndex, timestamp, newBalanceWei);
139:
140:            balanceDeltaWei = int256(newBalanceWei) - int256(prevBalanceWei);
141:        }
142:
143:        return balanceDeltaWei;	// @audit-issue
144:    }
```
[143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L144), 


#### Recommendation

When a function defines a named return variable and assigns a value to it, there is no need to add an explicit return statement at the end of the function. The named return variable will be automatically returned with its assigned value. Removing the redundant return statement can lead to cleaner and more concise code, improving readability and reducing the risk of introducing unnecessary errors.

### Consider using `delete` rather than assigning zero to clear values
The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

```solidity
Path: ./src/entities/Pauser.sol

41:        _getPauserStorage()._paused = 0;	// @audit-issue
```
[41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L41-L41), 


#### Recommendation

When you need to clear or reset values in storage variables, consider using the `delete` keyword instead of manually assigning zero or other values. Using `delete` provides a more explicit and efficient way to clear storage variables. For example, instead of `myVariable = 0;`, you can use `delete myVariable;` to clear the value.

### Defined named returns not used within function
Such instances can be replaced with unnamed returns

```solidity
Path: ./src/Core.sol

331:    function getOperatorVaults(address operator) external view returns (address[] memory vaults) {	// @audit-issue: Return param `vaults` is defined but not used in function.
```
[331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L331-L331), 


```solidity
Path: ./src/NativeVault.sol

304:        returns (uint256 transferAmount)	// @audit-issue: Return param `transferAmount` is defined but not used in function.
```
[304](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L304-L304), 


```solidity
Path: ./src/Vault.sol

83:        returns (uint256 shares)	// @audit-issue: Return param `shares` is defined but not used in function.
```
[83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L83-L83), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

117:        returns (uint256 validatorBalanceWei)	// @audit-issue: Return param `validatorBalanceWei` is defined but not used in function.
```
[117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L117-L117), 


#### Recommendation

Inspect your Solidity functions for unused named return variables. If a named return is not actively used in the function, switch to using unnamed return types. This change simplifies the function signature and avoids potential confusion over the function's return behavior. Ensure that the function's documentation and comments clearly describe the return type and purpose, maintaining clarity even with unnamed return variables. This approach contributes to cleaner, more concise function declarations in your Solidity codebase.

### Event is not properly `indexed`
Index event fields make the field more quickly accessible [to off-chain tools](https://ethereum.stackexchange.com/questions/40396/can-somebody-please-explain-the-concept-of-event-indexing) that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each `event` should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be `indexed`.

```solidity
Path: ./src/entities/Pauser.sol

24:    event Paused(address account, uint256 map);	// @audit-issue

26:    event Unpaused(address account, uint256 map);	// @audit-issue
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L24-L24), [26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L26-L26), 


#### Recommendation

Enhance smart contract efficiency post-deployment by utilizing indexed events. This approach aids in efficiently tracking contract activities, significantly contributing to the reduction of gas costs.

### Lines are too long
Usually lines in source code are limited to [80](https://softwareengineering.stackexchange.com/questions/148677/why-is-80-characters-the-standard-limit-for-code-width) characters. Today's screens are much larger so it's reasonable to stretch this in some cases. The solidity style guide recommends a maximumum line length of [120 characters](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#maximum-line-length), so the lines below should be split when they reach that length.        self.impact_details = 


```solidity
Path: ./src/Core.sol

49:    /// @param _vetoCommittee: The address of the veto committee who can cancel/veto slashing requests. Should be a multisig.	// @audit-issue: Length of the line is: 126

82:    /// @notice Allows the manager to allowlist assets that then vaults can be created for with the asset as the underlying token.	// @audit-issue: Length of the line is: 131

259:    /// @dev If you want to have 0% slashing, set `maxSlashablePercentageWad` to `1` since 0 is used as a default flag for not set	// @audit-issue: Length of the line is: 131

260:    /// If a operator is set, it will have a non-zero slashable percentage. Hence we can just check for that to see if a DSS is registered	// @audit-issue: Length of the line is: 139

261:    /// @param maxSlashablePercentageWad The max slashable percent, in the form of wad, that the DSS can slash per cooldown period	// @audit-issue: Length of the line is: 131

370:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557	// @audit-issue: Length of the line is: 155
```
[49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L49-L49), [82](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L82-L82), [259](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L259-L259), [260](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L260-L260), [261](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L261-L261), [370](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L370-L370), 


```solidity
Path: ./src/NativeVault.sol

41:    /// @param _operator The operator of the vault (usually the caller of the deployVault function on Core which triggers this).	// @audit-issue: Length of the line is: 129

62:        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue: Length of the line is: 121

348:            Math.min(convertToAssets(balanceOf(nodeOwner)), _state().ownerToNode[nodeOwner].withdrawableCreditedNodeETH);	// @audit-issue: Length of the line is: 122

454:        // This allows all the ETH that was theoritically slashed in `slashAssets` function call can be moved to a slash store,	// @audit-issue: Length of the line is: 128
```
[41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L41-L41), [62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L62-L62), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L348-L348), [454](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L454-L454), 


```solidity
Path: ./src/Vault.sol

46:    /// @param _operator The operator of the vault (usually the caller of the deployVault function on Core which triggers this)	// @audit-issue: Length of the line is: 128

124:    /// @return withdrawalKey The ID of the withdrawl. This is variable is shared across everyone's withdrawal request in the vault	// @audit-issue: Length of the line is: 132

154:    /// @dev To prevent someone from sitting on queuedWithdrawals to front-run a slashing, DSS shouldn't consider stakes queued in withdrawals	// @audit-issue: Length of the line is: 143

155:    /// @dev Moreover, rewards are meant to be computed off-chain and shouldn't use vault to distribute em as ERC4626 isn't designed for that.	// @audit-issue: Length of the line is: 143

282:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557	// @audit-issue: Length of the line is: 155
```
[46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L46-L46), [124](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L124-L124), [154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L154-L154), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L155-L155), [282](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L282-L282), 


```solidity
Path: ./src/entities/Operator.sol

22:        mapping(IDSS dss => uint256 timestamp) nextSlashableTimestamp; // When this operator can be slashed again by a DSS	// @audit-issue: Length of the line is: 123

23:        mapping(address vault => bytes32 updateHash) pendingStakeUpdates; //Supporting only 1 update per vault at a time	// @audit-issue: Length of the line is: 121

97:            calculateRoot(queuedStakeUpdate) != operatorState.pendingStakeUpdates[queuedStakeUpdate.updateRequest.vault]	// @audit-issue: Length of the line is: 121
```
[22](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L22-L22), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L23-L23), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L97-L97), 


```solidity
Path: ./src/entities/CoreLib.sol

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue: Length of the line is: 121
```
[77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

68:                beaconStateRootProof.proof, beaconBlockRoot, beaconStateRootProof.beaconStateRoot, BEACON_STATE_ROOT_IDX	// @audit-issue: Length of the line is: 121
```
[68](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L68-L68), 


```solidity
Path: ./src/entities/MerkleProofs.sol

136:     * @notice this function returns the merkle root of a tree created from a set of leaves using sha256 as its hash function	// @audit-issue: Length of the line is: 126

139:     *  @dev A pre-condition to this function is that leaves.length is a power of two.  If not, the function will merkleize the inputs incorrectly.	// @audit-issue: Length of the line is: 148
```
[136](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L136-L136), [139](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L139-L139), 


```solidity
Path: ./src/entities/HookLib.sol

67:    /// @dev Returns `false` if the interface is not supported since the call wasn't a success if it actually went through	// @audit-issue: Length of the line is: 123
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L67-L67), 


```solidity
Path: ./src/entities/Pauser.sol

8:/// @dev Pauser contract that modifies https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/master/contracts/utils/PausableUpgradeable.sol	// @audit-issue: Length of the line is: 158
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L8-L8), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

99:        INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));	// @audit-issue: Length of the line is: 121

164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue: Length of the line is: 125
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L99-L99), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L164-L164), 


```solidity
Path: ./src/utils/ExtSloads.sol

6:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557	// @audit-issue: Length of the line is: 155
```
[6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L6-L6), 


#### Recommendation

To adhere to coding standards and enhance code readability, consider splitting long lines of code when they approach the recommended maximum line length. In Solidity, a common guideline is to limit lines to a maximum of 120 characters. Splitting long lines can improve code maintainability and make it easier to understand.

### Dependence on external protocols
External protocols should be monitored as such dependencies may introduce vulnerabilities if a vulnerability is found /introduced in the external protocol

```solidity
Path: ./src/NativeNode.sol

5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";	// @audit-issue

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L5-L5), [8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L8-L8), 


```solidity
Path: ./src/SlashStore.sol

5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";	// @audit-issue

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L5-L5), [8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L8-L8), 


```solidity
Path: ./src/SlashingHandler.sol

6:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue

7:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue
```
[6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L6-L6), [7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L7-L7), 


```solidity
Path: ./src/Core.sol

7:import {IBeacon} from "@openzeppelin/contracts/proxy/beacon/IBeacon.sol";	// @audit-issue

8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L7-L7), [8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L8-L8), 


```solidity
Path: ./src/NativeVault.sol

9:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";	// @audit-issue

10:import {IBeacon} from "@openzeppelin/contracts/proxy/beacon/IBeacon.sol";	// @audit-issue

11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L11-L11), 


```solidity
Path: ./src/Vault.sol

9:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";	// @audit-issue

10:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";	// @audit-issue

11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L11-L11), 


```solidity
Path: ./src/entities/Operator.sol

4:import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L4-L4), 


```solidity
Path: ./src/entities/CoreLib.sol

4:import {Create2} from "@openzeppelin/contracts/utils/Create2.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L4-L4), 


```solidity
Path: ./src/entities/SlasherLib.sol

4:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";	// @audit-issue

5:import "@openzeppelin/contracts/utils/structs/EnumerableMap.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L4-L4), [5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L5-L5), 


```solidity
Path: ./src/entities/HookLib.sol

5:import "@openzeppelin/contracts/interfaces/IERC165.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L5-L5), 


```solidity
Path: ./src/entities/Pauser.sol

5:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";	// @audit-issue

6:import {ContextUpgradeable} from "@openzeppelin-upgradeable/utils/ContextUpgradeable.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L6-L6), 


#### Recommendation

Regularly monitor and review the external protocols your Solidity contracts depend on for any updates or identified vulnerabilities. Consider implementing fallback mechanisms or contingency plans in your contracts to handle potential failures or compromises in these external protocols. Additionally, thoroughly audit and test the integration points with external protocols to ensure they adhere to your contract's security standards. Where possible, design your contract architecture to minimize reliance on external protocols or allow for upgradability in response to changes in these dependencies. Stay informed about developments in the protocols you depend on and actively participate in their community for early awareness of potential issues.

### Incorrect withdraw declaration
In Solidity, it's essential for clarity and interoperability to correctly specify return types in function declarations. If the `withdraw` function is expected to return a `bool` to indicate success or failure, its omission could lead to ambiguity or unexpected behavior when interacting with or calling this function from other contracts or off-chain systems. Missing return values can mislead developers and potentially lead to contract integrations built on incorrect assumptions. To resolve this, the function declaration for `withdraw` should be modified to explicitly include the `bool` return type, ensuring clarity and correctness in contract interactions.

```solidity
Path: ./src/NativeNode.sol

39:    function withdraw(address to, uint256 weiAmount)	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L39), 


```solidity
Path: ./src/SlashStore.sol

32:    function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L32-L32), 


```solidity
Path: ./src/NativeVault.sol

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue
```
[571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), 


```solidity
Path: ./src/Vault.sol

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue
332:        public
333:        override
334:        whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:        nonReentrant
336:        returns (uint256 shares)
```
[331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L336), 


#### Recommendation

Review the function declarations in your Solidity contracts, particularly for critical operations like `withdraw`, to ensure that they correctly specify return types. If a function is intended to indicate success or failure, it should explicitly declare a `bool` return type in its signature. For example, modify the `withdraw` function declaration from:
```solidity
function withdraw(uint256 amount) public {
    // Implementation
}

// to

function withdraw(uint256 amount) public returns (bool) {
    // Implementation
    return true; // Indicate success
}
```


### User Defined Value Types Bug
The current Solidity version has the [User Defined Value Types Bug]() issue.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2021/09/29/user-defined-value-types-bug/).

### Bug in Deduplication of Verbatim Blocks
The current Solidity version has the [Bug in Deduplication of Verbatim Blocks](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/) issue.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


```solidity
Path: ./src/entities/Pauser.sol

3:pragma solidity ^0.8.21;	// @audit-issue
```
[3](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L3-L3), 


```solidity
Path: ./src/utils/CommonUtils.sol

2:pragma solidity ^0.8.21;	// @audit-issue
```
[2](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L2-L2), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/).

### Storage Write Removal Bug On Conditional Early Termination
The current Solidity version has the [Storage Write Removal Bug On Conditional Early Termination](https://soliditylang.org/blog/2022/09/08/storage-write-removal-before-conditional-termination/) issue.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2022/09/08/storage-write-removal-before-conditional-termination/).

### Optimizer Bug Regarding Memory Side Effects of Inline Assembly
The current Solidity version has the [Optimizer Bug Regarding Memory Side Effects of Inline Assembly](https://soliditylang.org/blog/2022/06/15/inline-assembly-memory-side-effects-bug/) issue.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2022/06/15/inline-assembly-memory-side-effects-bug/).

### `abi.encodeCall` Literals Bug
The current Solidity version has the [abi.encodeCall Literals Bug](https://soliditylang.org/blog/2022/03/16/encodecall-bug/) issue.

```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

It is recommended to follow the fix provided in the [link](https://soliditylang.org/blog/2022/03/16/encodecall-bug/).

### Use `bytes.concat()` on `bytes` instead of `abi.encodePacked()` for clearer semantic meaning
Starting with version 0.8.4, Solidity has the `bytes.concat()` function, which allows one to concatenate a list of bytes/strings, without extra padding. Using this function rather than `abi.encodePacked()` makes the intended operation more clear, leading to less reviewer confusion.

```solidity
Path: ./src/entities/CoreLib.sol

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), 


```solidity
Path: ./src/entities/MerkleProofs.sol

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue

164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L164-L164), 


#### Recommendation

Consider using `bytes.concat()` instead of `abi.encodePacked()` for concatenating `bytes` for clearer semantic meaning, especially in Solidity versions 0.8.4 and later.

### Style Guide: Surround top level declarations in Solidity source with two blank lines.
1- Surround top level declarations in Solidity source with two blank lines.
2- Within a contract surround function declarations with a single blank line.


```solidity
Path: ./src/NativeNode.sol

18:    address nodeOwner;
19:
20:    /* ========== MUTATIVE FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
21:    constructor() {

23:    }
24:
25:    /// @notice Initializes the NativeNode
26:    /// @param _owner: The owner of the node, which should be the NativeVault in most cases
27:    /// @param _nodeOwner: The logical owner of the node whom the funds belong to	// @audit-issue: There should be single blank line between function declarations.
28:    function initialize(address _owner, address _nodeOwner) external initializer {

33:    }
34:
35:    /// @notice Lets the NativeVault withdraw funds to the given address.
36:    /// In case of slashed assets the NativeVault withdraws those funds to the slashStore
37:    /// @param to: address of receivers of the funds
38:    /// @param weiAmount: amount to be withdrawn in wei	// @audit-issue: There should be single blank line between function declarations.
39:    function withdraw(address to, uint256 weiAmount)

47:    }
48:
49:    /// @notice Lets the NativeVault pause NativeNode functions
50:    /// @param map: 256 bitmap for paused and unpaused functions, type(uint256).max to pause all functions	// @audit-issue: There should be single blank line between function declarations.
51:    function pause(uint256 map) external onlyOwner {

53:    }
54:
55:    /// @notice Lets the NativeVault unpause NativeNode functions
56:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
57:    function unpause(uint256 map) external onlyOwner {
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L18-L21), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L23-L28), [38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L33-L39), [50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L47-L51), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L53-L57), 


```solidity
Path: ./src/SlashStore.sol

16:    }
17:
18:    /// @notice Initializes the SlashStore
19:    /// @param _owner: The owner of the slashStore allowed to withdraw assets	// @audit-issue: There should be single blank line between function declarations.
20:    function initialize(address _owner) external initializer {

22:    }
23:
24:    /// @notice Emits DepositedSlashedAssets event with address of NativeNode and slashed amount	// @audit-issue: There should be single blank line between function declarations.
25:    receive() external payable {

27:    }
28:
29:    /// @notice Lets the owner of the store withdraw funds to an address.
30:    /// @param to: address of receivers of the funds
31:    /// @param weiAmount: amount to be withdrawn in wei	// @audit-issue: There should be single blank line between function declarations.
32:    function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {
```
[19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L16-L20), [24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L22-L25), [31](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L27-L32), 


```solidity
Path: ./src/Querier.sol

11:    ICore public core;
12:
13:    /* ========== MUTATIVE FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
14:    constructor(address coreAddress) {

16:    }
17:
18:    /* ============ VIEW FUNCTIONS ============ */
19:
20:    /**
21:     * @notice Fetches vaults queued for withdrawal.
22:     * @param operator address of operator
23:     * @param dss address of DSS contract
24:     * @return vaults addresses of vaults queued for withdrawal
25:     */	// @audit-issue: There should be single blank line between function declarations.
26:    function fetchVaultsQueuedForExit(address operator, IDSS dss) external view returns (address[] memory vaults) {
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L11-L14), [25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L16-L26), 


```solidity
Path: ./src/SlashingHandler.sol

28:    }
29:
30:    /// @notice initializes the slashingHandler: sets owner, list of supported assets
31:    /// @param owner address of the owner
32:    /// @param _supportedAssets array of assets can be slashed by the slashinh handler	// @audit-issue: There should be single blank line between function declarations.
33:    function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer {

39:    }
40:
41:    /// @notice Adds the token to list of supported assets
42:    /// @param token address of the token to be added to the list of supported assets	// @audit-issue: There should be single blank line between function declarations.
43:    function addSlashableToken(IERC20 token) external onlyOwner {

45:    }
46:
47:    /// @notice slashes the specified amount of the token
48:    /// The vault needs to give approval to the slashing handler prior to slashing
49:    /// Pulls the assets form the vault and send them to address(0)
50:    /// @param token address of the token to be slashed
51:    /// @param amount quantity of assets to be slashed	// @audit-issue: There should be single blank line between function declarations.
52:    function handleSlashing(IERC20 token, uint256 amount) external {
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L28-L33), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L39-L43), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L45-L52), 


```solidity
Path: ./src/Core.sol

39:    bytes32 internal constant STORAGE_SLOT = 0x13c729cff436dc8ac22d145f2c778f6a709d225083f39538cc5e2674f2f10700;
40:
41:    /* ========== MUTATIVE FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
42:    constructor() {

44:    }
45:
46:    /// @notice Initializes the Core contracts: sets owner, grants roles, and sets default values
47:    /// @param _vaultImpl: The address of the default vault implementation. Usually the standard ERC20 vault impl.
48:    /// @param _manager: The address of the manager who can do operations that don't put funds at risk.
49:    /// @param _vetoCommittee: The address of the veto committee who can cancel/veto slashing requests. Should be a multisig.
50:    /// @param _hookCallGasLimit: Max gas that can be used by hook calls to a DSS
51:    /// @param _supportsInterfaceGasLimit: Max gas that can be used by `supportsInterface` call to a DSS
52:    /// @param _hookGasBuffer: Minimum gas buffer to run the remaining logic after a DSS hook is called	// @audit-issue: There should be single blank line between function declarations.
53:    function initialize(

68:    }
69:
70:    /// @notice Pauses the contract functions in an idemptotent way
71:    /// @param map: 256 bitmap for paused and unpaused functions, type(uint256).max to pause all functions	// @audit-issue: There should be single blank line between function declarations.
72:    function pause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

74:    }
75:
76:    /// @notice Unpauses the contract functions in an idemptotent way
77:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
78:    function unpause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

80:    }
81:
82:    /// @notice Allows the manager to allowlist assets that then vaults can be created for with the asset as the underlying token.
83:    /// @dev If an asset that is already allowlisted is passed, it will be be set to allowlisted again.
84:    /// @param assets: The list of assets to allowlist	// @audit-issue: There should be single blank line between function declarations.
85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)

91:    }
92:
93:    /// @notice Allows a operator to register with a DSS. This then allows them to allocate a portion of the assets
94:    /// delegated to them by stakers.
95:    /// @param dss: The address of the DSS to register with
96:    /// @param registrationHookData: The data to pass to the DSS's beforeRegistrationHook	// @audit-issue: There should be single blank line between function declarations.
97:    function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)

107:    }
108:
109:    /// @notice Allows a operator to unregister from a DSS
110:    /// @dev All asset delegations to the DSS must be 0 before the operator can unregister
111:    /// @param dss: The address of the DSS to unregister from
112:    /// @param unregistrationHookData: The data to pass to the DSS's beforeUnregistrationHook	// @audit-issue: There should be single blank line between function declarations.
113:    function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)

124:    }
125:
126:    /// @notice Allows operator to stake/unstake vault to a DSS
127:    /// @dev Only operator can update the stake of their vaults and
128:    /// logically, only 1 update request is allowed per vault until its completed or canceled
129:    /// @param vaultStakeUpdateRequest: stake update request with to stake/unstake, address of dss and address of vault	// @audit-issue: There should be single blank line between function declarations.
130:    function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)

141:    }
142:
143:    /// @notice Allows anyone to finish the queued request for an operator to update assets delegated to a DSS
144:    /// @dev Only operator can finish their queued request valid only after a
145:    /// minimum delay of `Constants.MIN_STAKE_UPDATE_DELAY` after starting the request	// @audit-issue: There should be single blank line between function declarations.
146:    function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake)

153:    }
154:
155:    /// @notice Deploys a new restaking vault with the given configuration to an operator
156:    /// @dev Emits a DeployedVault event for each vault deployed
157:    /// @dev It is meant to be permissionless since the setting of the standard vault implementation is permissioned
158:    /// @param vaultConfigs: The configurations of the vaults to deploy
159:    /// @param vaultImpl: The address of the vault implementation to use
160:    /// @return vaults {IKarakBaseVault[]} The addresses of the deployed vaults	// @audit-issue: There should be single blank line between function declarations.
161:    function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)

168:    }
169:
170:    /// @notice Allows the owner to change the standard vault implementation and upgrade all vaults using
171:    /// the default implementation to the new implementation.
172:    /// @param newVaultImpl: The address of the new vault implementation	// @audit-issue: There should be single blank line between function declarations.
173:    function changeStandardImplementation(address newVaultImpl) external onlyOwner {

178:    }
179:
180:    /// @notice Allows the owner to change the implementation of a specific vault
181:    /// @param vault: The address of the vault to change the implementation of
182:    /// @param newVaultImpl: The address of the new vault implementation. Must be a allowlisted implementation	// @audit-issue: There should be single blank line between function declarations.
183:    function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner {

192:    }
193:
194:    /// @notice Allows the owner or manager to pause functions of a vault
195:    /// @param vault: The address of the vault to pause
196:    /// @param map: 256 bitmap for vault paused and unpaused functions, type(uint256).max to pause all functions	// @audit-issue: There should be single blank line between function declarations.
197:    function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

199:    }
200:
201:    /// @notice Allows the owner or manager to unpause functions of a vault
202:    /// @param vault: The address of the vault to unpause
203:    /// @param map: 256 bitmap for vault paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
204:    function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

206:    }
207:
208:    /// @notice Allows the owner to allowlist a new vault implementation
209:    /// This is meant for custom 4626 vaults like native restaking vaults
210:    /// @param vaultImpl {address}: The address of the vault implementation to allowlist	// @audit-issue: There should be single blank line between function declarations.
211:    function allowlistVaultImpl(address vaultImpl) external onlyOwner {

216:    }
217:
218:    /// @notice Allows a slashing to be requested for a given operator+vault by a DSS
219:    /// @param slashingRequest: The request to slash the operator	// @audit-issue: There should be single blank line between function declarations.
220:    function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)

231:    }
232:
233:    /// @notice Allows the veto committee to cancel a queued slashing
234:    /// @param queuedSlashing: The slashing to cancel	// @audit-issue: There should be single blank line between function declarations.
235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)

243:    }
244:
245:    /// @notice Allows anyone to finalize a queued slashing and send the slashed assets
246:    /// @notice to the slashing handler
247:    /// @param queuedSlashing: The slashing to finish	// @audit-issue: There should be single blank line between function declarations.
248:    function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)

256:    }
257:
258:    /// @notice Allows the caller to register as a DSS and set the max slashable percentage
259:    /// @dev If you want to have 0% slashing, set `maxSlashablePercentageWad` to `1` since 0 is used as a default flag for not set
260:    /// If a operator is set, it will have a non-zero slashable percentage. Hence we can just check for that to see if a DSS is registered
261:    /// @param maxSlashablePercentageWad The max slashable percent, in the form of wad, that the DSS can slash per cooldown period	// @audit-issue: There should be single blank line between function declarations.
262:    function registerDSS(uint256 maxSlashablePercentageWad) external {

267:    }
268:
269:    /// @notice Sets gas limits for DSS hook calls
270:    /// @dev Set to prevent DOS vector as malicious DSS can block calls by using infinite gas
271:    /// @param _hookCallGasLimit: Gas limit to perform call to DSS for corresponding hook call
272:    /// @param _hookGasBuffer: Buffer gas to perform the rest of hook call
273:    /// @param _supportsInterfaceGasLimit: Gas limit for `supportsInterface` call to DSS	// @audit-issue: There should be single blank line between function declarations.
274:    function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)

279:    }
280:
281:    /* ======================================== */
282:
283:    /* ============ VIEW FUNCTIONS ============ */
284:    /// @notice Returns if a given asset is allowlisted
285:    /// @dev Only matters for the `deployVault` flow. Allowlisting is not required for custom vaults.
286:    /// @param asset: The address of the ERC20 asset to check
287:    /// @return bool if the asset is allowlisted, false otherwise	// @audit-issue: There should be single blank line between function declarations.
288:    function isAssetAllowlisted(address asset) public view returns (bool) {

290:    }
291:
292:    /// @notice checks whether the given `vaultImplementation` is allowlisted or not
293:    /// @param vaultImpl address of the implementaion	// @audit-issue: There should be single blank line between function declarations.
294:    function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {

296:    }
297:
298:    /// @notice Returns true if a given operator is registered to a DSS
299:    /// @param operator: The address of the operator to check
300:    /// @param dss: The address of the DSS to check
301:    /// @return {bool} True if the operator is registered to the DSS, false otherwise	// @audit-issue: There should be single blank line between function declarations.
302:    function isOperatorRegisteredToDSS(address operator, IDSS dss) public view returns (bool) {

304:    }
305:
306:    /// @notice Returns the implementation of the vault for the given operator
307:    /// @return {address} The address of the vault implementation	// @audit-issue: There should be single blank line between function declarations.
308:    function implementation() external view override returns (address) {

310:    }
311:
312:    /// @notice Returns the implementation for a given vault
313:    /// @dev Doesn't revert if the vault is not set yet because during `deployVault`
314:    /// theres a period before we set it to the default flag where the vault
315:    /// needs an impl to be initialized against
316:    /// @param vault: The address of the vault to get the implementation for
317:    /// @return {address} The address of the given vault's implementation	// @audit-issue: There should be single blank line between function declarations.
318:    function implementation(address vault) public view returns (address) {

326:    }
327:
328:    /// @notice Returns the vaults for a given operator
329:    /// @param operator: The address of the operator to get the vaults for
330:    /// @return vaults {address[]} The addresses of the vaults attached to the operator	// @audit-issue: There should be single blank line between function declarations.
331:    function getOperatorVaults(address operator) external view returns (address[] memory vaults) {

333:    }
334:
335:    /// @notice Returns the vaults staked for a given operator in a DSS
336:    /// @param operator: The address of the operator to get the stakes for
337:    /// @param dss: The address of the DSS that the operator is validating for
338:    /// @return vaults {address[]} The addresses of the vaults that the operator is validating for attached to this DSS	// @audit-issue: There should be single blank line between function declarations.
339:    function fetchVaultsStakedInDSS(address operator, IDSS dss) external view returns (address[] memory vaults) {

341:    }
342:
343:    /// @notice Returns the leverage of a given vault
344:    /// @dev Leverage is done in whole numbers 1x, 2x, Nx, where n is the number of DSS the vault is delegated to
345:    /// this is because a vault allocates its entire balance to every vault. Hence why this function just takes
346:    /// the number of DSSs a vault is allocated to and multiplies it by 100e18 (100%)
347:    /// @param vault Address of the vault
348:    /// @return leverage {uint256} Leverage of vault in percentageWad	// @audit-issue: There should be single blank line between function declarations.
349:    function getLeverage(address vault) external view returns (uint256 leverage) {

352:    }
353:
354:    /// @notice Returns the max slashable percentageWad by DSS per slashing request.
355:    /// @dev A DSS has to wait a `SLASHING_COOLDOWN` before it can slash again
356:    /// @param dss The address of dss.
357:    /// @return slashablePercentageWad {uint256} The maximum slashable percentageWad per slashing event by DSS.	// @audit-issue: There should be single blank line between function declarations.
358:    function getDssMaxSlashablePercentageWad(IDSS dss) public view returns (uint256 slashablePercentageWad) {

360:    }
361:
362:    /// @notice Returns true if dss is registered in the protocol.
363:    /// @param dss address of the dss.
364:    /// @return boolean indicating dss is registered or not.	// @audit-issue: There should be single blank line between function declarations.
365:    function isDSSRegistered(IDSS dss) public view returns (bool) {

367:    }
368:
369:    /// @notice Allows reading of arbitrary storage slots. Useful for reading inside embedded structs
370:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557
371:    /// @param slots The storage slots to read
372:    /// @return res {bytes32 memory} The values stored in the given storage slots	// @audit-issue: There should be single blank line between function declarations.
373:    function extSloads(bytes32[] calldata slots)

380:    }
381:
382:    /* ======================================== */
383:
384:    /* ========== INTERNAL FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
385:    function _self() internal pure returns (CoreLib.Storage storage $) {
```
[41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L39-L42), [52](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L44-L53), [71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L68-L72), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L74-L78), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L80-L85), [96](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L91-L97), [112](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L107-L113), [129](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L124-L130), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L141-L146), [160](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L153-L161), [172](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L168-L173), [182](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L178-L183), [196](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L192-L197), [203](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L199-L204), [210](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L206-L211), [219](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L216-L220), [234](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L231-L235), [247](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L243-L248), [261](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L256-L262), [273](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L267-L274), [287](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L279-L288), [293](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L290-L294), [301](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L296-L302), [307](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L304-L308), [317](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L310-L318), [330](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L326-L331), [338](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L333-L339), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L341-L349), [357](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L352-L358), [364](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L360-L365), [372](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L367-L373), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L380-L385), 


```solidity
Path: ./src/NativeVault.sol

32:    bytes32 internal constant CONFIG_SLOT = 0xb6497276931248fe2cc1dc985a2850cccba81036959c83b89ec93582a1e00900;
33:
34:    /* ========== MUTATIVE FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
35:    constructor() {

37:    }
38:
39:    /// @notice Initializes the vault
40:    /// @param _owner The owner of the NativeVault, which should be Core in most cases.
41:    /// @param _operator The operator of the vault (usually the caller of the deployVault function on Core which triggers this).
42:    /// @param _depositToken Disregarded for NativeVault. Can be address(0).
43:    /// @param _name The name of the vault
44:    /// @param _symbol The symbol of the vault
45:    /// @param _extraData Serialized bytes consisting {address slashStore, address nodeImplementation}	// @audit-issue: There should be single blank line between function declarations.
46:    function initialize(

79:    }
80:
81:    /// @notice Allows the owner to change the NativeNode implementation and upgrade all NativeNodes
82:    /// @param newNodeImplementation: The address of the new node implementation	// @audit-issue: There should be single blank line between function declarations.
83:    function changeNodeImplementation(address newNodeImplementation)

92:    }
93:
94:    /// @notice Deploys a new NativeNode for the caller	// @audit-issue: There should be single blank line between function declarations.
95:    function createNode()

106:    }
107:
108:    /// @notice Lets the owner start a snapshot for their NativeNode which is completed
109:    /// only when balance proofs are submitted for all active validators of the node.
110:    /// Reverts if there is a pending snapshot in progress or if there is no balance change
111:    /// from the last snapshot.	// @audit-issue: There should be single blank line between function declarations.
112:    function startSnapshot(bool revertIfNoBalanceChange)

119:    }
120:
121:    /// @notice Validates snapshot proofs that can be submitted by anyone for active
122:    /// validators in the NativeNode and awards or burns shares for balance changes.
123:    /// @param nodeOwner: address of the owner whose NativeNode the proof is submitted for
124:    /// @param balanceProofs: proofs for validators balance validated against the balance container root
125:    /// @param balanceContainer: balance container proof validated against the snapshot's beacon block root	// @audit-issue: There should be single blank line between function declarations.
126:    function validateSnapshotProofs(

162:    }
163:
164:    /// @notice Validates that a validator's withdrawal credentials are pointed to the an owner's NativeNode.
165:    /// @param nodeOwner: address of the owner whose NativeNode the proof is submitted for
166:    /// @param beaconStateRootProof: proof of a beacon state root against the beacon block root
167:    /// @param validatorFieldsProofs: validator fields proofs validated against the beacon state root	// @audit-issue: There should be single blank line between function declarations.
168:    function validateWithdrawalCredentials(

204:    }
205:
206:    /// @notice Allows anyone to start a new snapshot if the last snapshot has expired,
207:    /// i.e. older than `Constants.SNAPSHOT_EXPIRY since the last completed timestamp.
208:    /// Does not revert if there is no change in balance.
209:    /// @param nodeOwner: address of the owner whose NativeNode has expired snapshot	// @audit-issue: There should be single blank line between function declarations.
210:    function validateExpiredSnapshot(address nodeOwner)

223:    }
224:
225:    /// @notice Allows caller to start a withdrawal to withdraw ETH accrued on their NativeNode
226:    /// @param to: address to withdraw the funds to
227:    /// @param weiAmount: amount to be withdrawn in wei	// @audit-issue: There should be single blank line between function declarations.
228:    function startWithdrawal(address to, uint256 weiAmount)

258:    }
259:
260:    /// @notice Allows caller to finish a pending withdrawal
261:    /// @param withdrawalKey: The ID of the withdrawal request returned by startWithdrawal	// @audit-issue: There should be single blank line between function declarations.
262:    function finishWithdrawal(bytes32 withdrawalKey)

294:    }
295:
296:    /// @notice Allows the owner to slash the vault with given amount
297:    /// @param totalAssetsToSlash: amount to slash in wei
298:    /// @param slashingHandler: address of the slash store	// @audit-issue: There should be single blank line between function declarations.
299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)

318:    }
319:
320:    /// @notice Lets the owner pause NativeVault functions
321:    /// @param map: 256 bitmap for paused and unpaused functions, type(uint256).max to pause all functions	// @audit-issue: There should be single blank line between function declarations.
322:    function pause(uint256 map) external onlyOwner {

324:    }
325:
326:    /// @notice Lets the owner unpause NativeVault functions
327:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
328:    function unpause(uint256 map) external onlyOwner {

330:    }
331:
332:    /// @notice Lets the owner or manager of the NativeVault pause NativeNode functions
333:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
334:    function pauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

336:    }
337:
338:    /// @notice Lets the owner or manager of the NativeVault unpause NativeNode functions
339:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
340:    function unpauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {

342:    }
343:    /* ======================================== */
344:
345:    /* ============ VIEW FUNCTIONS ============ */	// @audit-issue: There should be single blank line between function declarations.
346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {

399:    }
400:    /* ======================================== */
401:
402:    /* ========== INTERNAL FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
403:    function _state() internal pure returns (NativeVaultLib.Storage storage $) {

525:    }
526:    /* ======================================== */
527:
528:    /* ============== MODIFIERS =============== */	// @audit-issue: There should be single blank line between function declarations.
529:    modifier nodeExists(address owner) {

532:    }
533:    /* ======================================== */
534:
535:    /* ============== OVERRIDES =============== */	// @audit-issue: There should be single blank line between function declarations.
536:    function transfer(address to, uint256 amount) public pure override returns (bool) {
```
[34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L32-L35), [45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L37-L46), [82](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L79-L83), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L92-L95), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L106-L112), [125](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L119-L126), [167](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L162-L168), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L204-L210), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L223-L228), [261](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L258-L262), [298](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L294-L299), [321](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L318-L322), [327](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L324-L328), [333](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L330-L334), [339](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L336-L340), [345](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L342-L346), [402](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L399-L403), [528](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L525-L529), [535](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L532-L536), 


```solidity
Path: ./src/Vault.sol

37:    bytes32 internal constant CONFIG_SLOT = 0x22a8eb0cbcfbbbc874f794ecd9efdfeeecb09fe60d66cf9327db2eac8a1ff000;
38:
39:    /* ========== MUTATIVE FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
40:    constructor() {

42:    }
43:
44:    /// @notice Initializes the vault
45:    /// @param _owner The owner of the vault (usually the Core contract which is the caller in most cases)
46:    /// @param _operator The operator of the vault (usually the caller of the deployVault function on Core which triggers this)
47:    /// @param _depositToken The underlying token of the vault
48:    /// @param _name The name of the vault
49:    /// @param _symbol The symbol of the vault
50:    /// @param _extraData Serialized bytes of extra data that different implemetations can use for their own purposes	// @audit-issue: There should be single blank line between function declarations.
51:    function initialize(

71:    }
72:
73:    /// @notice Deposits assets into the vault
74:    /// @dev checks if the amount is not 0 then passes to Solady's implementation
75:    /// @dev if you want slippage protection use the overload of this function with minSharesOut
76:    /// @param assets The amount of assets to deposit
77:    /// @param to The address to mint the shares to	// @audit-issue: There should be single blank line between function declarations.
78:    function deposit(uint256 assets, address to)

87:    }
88:
89:    /// @notice Deposits assets into the vault with a minimum amount of shares to mint
90:    /// @dev This is to prevent any malicious frontrunning in ERC4626
91:    /// @param assets The amount of assets to deposit
92:    /// @param to The address to mint the shares to
93:    /// @param minSharesOut The minimum amount of shares to mint else revert	// @audit-issue: There should be single blank line between function declarations.
94:    function deposit(uint256 assets, address to, uint256 minSharesOut)

103:    }
104:
105:    /// @notice Mints shares for a given amount of assets
106:    /// @dev Included to better comply with ERC4626
107:    /// @param shares The amount of shares to mint
108:    /// @param to The address to mint the shares to
109:    /// @return assets The amount of assets used to mint the shares	// @audit-issue: There should be single blank line between function declarations.
110:    function mint(uint256 shares, address to)

119:    }
120:
121:    /// @notice Starts a redeem process for a given amount of shares
122:    /// and transfers those shares from the user to the vault
123:    /// @param shares The amount of shares to redeem
124:    /// @return withdrawalKey The ID of the withdrawl. This is variable is shared across everyone's withdrawal request in the vault	// @audit-issue: There should be single blank line between function declarations.
125:    function startRedeem(uint256 shares, address beneficiary)

149:    }
150:
151:    /// @notice Finishes a redeem process after waiting the required delay
152:    /// @notice Can be called by anyone on anyone's behalf
153:    /// @dev Most of this logic is copied from the underlying Solady 4626 implementation's redeem function
154:    /// @dev To prevent someone from sitting on queuedWithdrawals to front-run a slashing, DSS shouldn't consider stakes queued in withdrawals
155:    /// @dev Moreover, rewards are meant to be computed off-chain and shouldn't use vault to distribute em as ERC4626 isn't designed for that.
156:    /// @param withdrawalKey The ID of the withdrawal request given by startRedeem tx	// @audit-issue: There should be single blank line between function declarations.
157:    function finishRedeem(bytes32 withdrawalKey)

188:    }
189:
190:    /// @notice Slash the assets in the vault by a certain amount portion to a slashing handler contract
191:    /// @param totalAssetsToSlash The amount of assets to slash in absolute amounts
192:    /// @param slashingHandler The address of the slashing handler	// @audit-issue: There should be single blank line between function declarations.
193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)

205:    }
206:
207:    /// @notice Lets the Core contract pause the vault functions
208:    /// @param map: 256 bitmap for paused and unpaused functions, type(uint256).max to pause all functions	// @audit-issue: There should be single blank line between function declarations.
209:    function pause(uint256 map) external onlyCore {

211:    }
212:
213:    /// @notice Lets the Core contract unpause the vault functions
214:    /// @param map: 256 bitmap for paused and unpaused functions, 0 to unpause all functions	// @audit-issue: There should be single blank line between function declarations.
215:    function unpause(uint256 map) external onlyCore {

217:    }
218:    /* ======================================== */
219:
220:    /* ============ VIEW FUNCTIONS ============ */
221:    /// @notice Fetches name of the vault token	// @audit-issue: There should be single blank line between function declarations.
222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {

224:    }
225:
226:    /// @notice Fetches symbol of the vault token	// @audit-issue: There should be single blank line between function declarations.
227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {

229:    }
230:
231:    /// @notice Fetches underlying asset of the vault	// @audit-issue: There should be single blank line between function declarations.
232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {

234:    }
235:
236:    /// @notice Fetches vault config	// @audit-issue: There should be single blank line between function declarations.
237:    function vaultConfig() public pure returns (VaultLib.Config memory) {

239:    }
240:
241:    /// @notice Fetches the next withdrawal nonce of the staker
242:    /// @param staker the address of the staker	// @audit-issue: There should be single blank line between function declarations.
243:    function getNextWithdrawNonce(address staker) public view returns (uint256) {

245:    }
246:
247:    /// @notice Checks if the withdrawal is pending for given nonce
248:    /// @param staker address of the staker
249:    /// @param _withdrawNonce withdrawal nonce of the staker at the time of withdrawal	// @audit-issue: There should be single blank line between function declarations.
250:    function isWithdrawalPending(address staker, uint256 _withdrawNonce) public view returns (bool) {

252:    }
253:
254:    /// @notice Fetches queued withdrawal metadata for given nonce
255:    /// @param staker address of the staker
256:    /// @param _withdrawNonce withdrawal nonce of the staker at the time of withdrawal
257:    /// @return QueuedWithdrawal params	// @audit-issue: There should be single blank line between function declarations.
258:    function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)

264:    }
265:
266:    /// @notice Total underlying assets deposited in vault	// @audit-issue: There should be single blank line between function declarations.
267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {

269:    }
270:
271:    /// @notice owner of the vault	// @audit-issue: There should be single blank line between function declarations.
272:    function owner() public view override(Ownable, IVault) returns (address) {

274:    }
275:
276:    /// @notice decimals of the vault tokens	// @audit-issue: There should be single blank line between function declarations.
277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {

279:    }
280:
281:    /// @notice Allows reading of arbitrary storage slots. Useful for reading inside embedded structs
282:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557
283:    /// @param slots The storage slots to read
284:    /// @return res The values stored in the given storage slots	// @audit-issue: There should be single blank line between function declarations.
285:    function extSloads(bytes32[] calldata slots)

292:    }
293:
294:    /* ======================================== */
295:
296:    /* ========== INTERNAL FUNCTIONS ========== */	// @audit-issue: There should be single blank line between function declarations.
297:    function _state() internal pure returns (VaultLib.State storage $) {

318:    }
319:    /* ======================================== */
320:
321:    /* ============== MODIFIERS =============== */	// @audit-issue: There should be single blank line between function declarations.
322:    modifier onlyCore() {

325:    }
326:    /* ======================================== */
327:
328:    /* ============== OVERRIDES =============== */
329:
330:    /// @notice will revert	// @audit-issue: There should be single blank line between function declarations.
331:    function withdraw(uint256 assets, address to, address owner)

345:    }
346:
347:    /// @notice will revert	// @audit-issue: There should be single blank line between function declarations.
348:    function redeem(uint256 shares, address to, address owner)
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L37-L40), [50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L42-L51), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L71-L78), [93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L87-L94), [109](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L103-L110), [124](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L119-L125), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L149-L157), [192](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L188-L193), [208](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L205-L209), [214](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L211-L215), [221](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L217-L222), [226](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L224-L227), [231](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L229-L232), [236](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L234-L237), [242](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L239-L243), [249](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L245-L250), [257](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L252-L258), [266](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L264-L267), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L269-L272), [276](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L274-L277), [284](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L279-L285), [296](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L292-L297), [321](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L318-L322), [330](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L325-L331), [347](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L345-L348), 


```solidity
Path: ./src/entities/Operator.sol

203:    }
204:
205:    /// Fetches the DSSs the operator is registered in
206:    /// @param self Reference to the Core's storage
207:    /// @param operator address of the operator
208:    /// @return dssAddresses List of DSSs	// @audit-issue: There should be single blank line between function declarations.
209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)

219:    }
220:
221:    /// Fetches the list of DSSs an operator's vault is staked to
222:    /// @param self Reference to the Core's storage
223:    /// @return count Count of the DSSs the operator's vault is staked to	// @audit-issue: There should be single blank line between function declarations.
224:    function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)
```
[208](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L203-L209), [223](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L219-L224), 


```solidity
Path: ./src/entities/MerkleProofs.sol

35:    }
36:
37:    /**
38:     * @dev Returns the rebuilt hash obtained by traversing a Merkle tree up
39:     * from `leaf` using `proof`. A `proof` is valid if and only if the rebuilt
40:     * hash matches the root of the tree. The tree is built assuming `leaf` is
41:     * the 0 indexed `index`'th leaf from the bottom left of the tree.
42:     * @dev If the proof length is 0 then the leaf hash is returned.
43:     *
44:     * _Available since v4.4._
45:     *
46:     * Note this is for a Merkle tree using the keccak/sha3 hash function
47:     */	// @audit-issue: There should be single blank line between function declarations.
48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)

75:    }
76:
77:    /**
78:     * @dev Returns the rebuilt hash obtained by traversing a Merkle tree up
79:     * from `leaf` using `proof`. A `proof` is valid if and only if the rebuilt
80:     * hash matches the root of the tree. The tree is built assuming `leaf` is
81:     * the 0 indexed `index`'th leaf from the bottom left of the tree.
82:     *
83:     * Note this is for a Merkle tree using the sha256 hash function
84:     */	// @audit-issue: There should be single blank line between function declarations.
85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)

91:    }
92:
93:    /**
94:     * @dev Returns the rebuilt hash obtained by traversing a Merkle tree up
95:     * from `leaf` using `proof`. A `proof` is valid if and only if the rebuilt
96:     * hash matches the root of the tree. The tree is built assuming `leaf` is
97:     * the 0 indexed `index`'th leaf from the bottom left of the tree.
98:     *
99:     * _Available since v4.4._
100:     *
101:     * Note this is for a Merkle tree using the sha256 hash function
102:     */	// @audit-issue: There should be single blank line between function declarations.
103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)

133:    }
134:
135:    /**
136:     * @notice this function returns the merkle root of a tree created from a set of leaves using sha256 as its hash function
137:     *  @param leaves the leaves of the merkle tree
138:     *  @return The computed Merkle root of the tree.
139:     *  @dev A pre-condition to this function is that leaves.length is a power of two.  If not, the function will merkleize the inputs incorrectly.
140:     */	// @audit-issue: There should be single blank line between function declarations.
141:    function merkleizeSha256(bytes32[] memory leaves) internal pure returns (bytes32) {
```
[47](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L35-L48), [84](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L75-L85), [102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L91-L103), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L133-L141), 


```solidity
Path: ./src/entities/HookLib.sol

39:    }
40:
41:    /// @notice Performs low level call to the DSS
42:    /// @param target address of DSS contract
43:    /// @param data the calldata
44:    /// @param ignoreFailure whether to revert tx incase call to DSS fails
45:    /// @param hookCallGasLimit max gas to perform call with
46:    /// @param hookGasBuffer gas to perform this function call
47:    /// @return boolean indicating call succeeded or not	// @audit-issue: There should be single blank line between function declarations.
48:    function callHook(

64:    }
65:
66:    /// @notice performs a low level call to the dss with given data, returns boolean incase of success or failure
67:    /// @dev Returns `false` if the interface is not supported since the call wasn't a success if it actually went through
68:    /// If the call to the DSS is not successful then the tx is reverted based on the `ignoreFailure` param
69:    /// gas checks are performed to ensure calls are not failed due to OOG error
70:    /// @param dss address of the DSS
71:    /// @param data the calldata
72:    /// @param interfaceId interface to be called
73:    /// @param ignoreFailure whether the call to DSS can be ignored or not
74:    /// @param hookCallGasLimit gasLimit to perform call to the DSS
75:    /// @param supportsInterfaceGasLimit gasLimit to perform `supportsInterface` call to the DSS
76:    /// @param hookGasBuffer gas to perform this function call
77:    /// @return boolean indicating hook call passed or failed	// @audit-issue: There should be single blank line between function declarations.
78:    function callHookIfInterfaceImplemented(
```
[47](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L39-L48), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L64-L78), 


```solidity
Path: ./src/utils/CommonUtils.sol

33:    }
34:
35:    /// @notice Sorts the array and checks for duplicates
36:    /// Intent was to get the array unchanges after sorting
37:    /// @param arr Array of addresses to check duplicates
38:    /// @return boolean indicates whether array has duplicates or not	// @audit-issue: There should be single blank line between function declarations.
39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L33-L39), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/latest/style-guide.html#blank-lines).

### `constants` should be defined rather than using magic numbers
Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

```solidity
Path: ./src/entities/BeaconProofsLib.sol

55:        n = uint64(uint256(lenum >> 192));	// @audit-issue

56:        return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)	// @audit-issue

57:            | ((0x000000FF00000000 & n) >> 8) | ((0x00000000FF000000 & n) << 8) | ((0x0000000000FF0000 & n) << 24)	// @audit-issue

58:            | ((0x000000000000FF00 & n) << 40) | ((0x00000000000000FF & n) << 56);	// @audit-issue

65:        if (beaconStateRootProof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT)) revert InvalidBeaconStateProof();	// @audit-issue

88:        if (validatorProof.length != 32 * ((VALIDATOR_HEIGHT + 1) + BEACON_STATE_HEIGHT)) {	// @audit-issue

98:        if (proof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT + BEACON_STATE_HEIGHT)) {	// @audit-issue

119:        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L55-L55), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L56-L56), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L57-L57), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L58-L58), [65](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L65-L65), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L88-L88), [98](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L98-L98), [119](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L119-L119), 


```solidity
Path: ./src/entities/MerkleProofs.sol

53:        require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32");	// @audit-issue

56:            if (index % 2 == 0) {	// @audit-issue

55:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

109:            proof.length != 0 && proof.length % 32 == 0,	// @audit-issue

114:            if (index % 2 == 0) {	// @audit-issue

113:        for (uint256 i = 32; i <= proof.length; i += 32) {	// @audit-issue

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

151:        numNodesInLayer /= 2;	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue

159:            numNodesInLayer /= 2;	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L53-L53), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L56-L56), [55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L55-L55), [109](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L109-L109), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L114-L114), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L113-L113), [148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [151](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L151-L151), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), [159](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L159-L159), 


```solidity
Path: ./src/entities/HookLib.sol

55:        if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas();	// @audit-issue

87:        if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) {	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L55-L55), [87](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L87-L87), 


#### Recommendation

Consider defining constants with meaningful names for magic numbers and hexadecimal literals to improve code readability and maintainability.

### Constant redefined elsewhere
Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

```solidity
Path: ./src/SlashingHandler.sol

17:    string public constant VERSION = "2.0.0";	// @audit-issue seen in: ./src/Querier.sol
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L17-L17), 


```solidity
Path: ./src/Core.sol

36:    string public constant VERSION = "2.0.0";	// @audit-issue seen in: ./src/SlashingHandler.sol
```
[36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L36-L36), 


```solidity
Path: ./src/NativeVault.sol

32:    bytes32 internal constant CONFIG_SLOT = 0xb6497276931248fe2cc1dc985a2850cccba81036959c83b89ec93582a1e00900;	// @audit-issue seen in: ./src/SlashingHandler.sol
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L32-L32), 


```solidity
Path: ./src/Vault.sol

32:    string public constant VERSION = "2.0.0";	// @audit-issue seen in: ./src/Core.sol

35:    bytes32 internal constant STATE_SLOT = 0x5d654853f9da5c5c659891e7f7fc564033f2724663c32c175f373318f8e1e700;	// @audit-issue seen in: ./src/NativeVault.sol

37:    bytes32 internal constant CONFIG_SLOT = 0x22a8eb0cbcfbbbc874f794ecd9efdfeeecb09fe60d66cf9327db2eac8a1ff000;	// @audit-issue seen in: ./src/NativeVault.sol
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L32-L32), [35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L35-L35), [37](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L37-L37), 


#### Recommendation

To avoid constant values being redefined in multiple locations, consider defining constants in a single contract, such as a library, using internal constants. This approach ensures that values remain consistent and reduces the risk of synchronization issues. If a variable serves as a local cache of another contract's value, make the cache variable internal or private, requiring external users to query the contract with the source of truth to prevent synchronization problems.

### Lack of index element validation in function
There's no validation to check whether the index element provided as an argument actually exists in the call. This omission could lead to unintended behavior if an element that does not exist in the call is passed to the function. The function should validate that the provided index element exists in the call before proceeding.

```solidity
Path: ./src/SlashingHandler.sol

37:            config.supportedAssets[_supportedAssets[i]] = true;	// @audit-issue
```
[37](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L37-L37), 


```solidity
Path: ./src/NativeVault.sol

154:                nodeOwner, validatorDetails, balanceContainer.containerRoot, balanceProofs[i]	// @audit-issue

199:                validatorFieldsProofs[i]	// @audit-issue
```
[154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L154-L154), [199](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L199-L199), 


```solidity
Path: ./src/entities/CoreLib.sol

73:            self.assetSlashingHandlers[assets[i]] = slashingHandlers[i];	// @audit-issue

85:            if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();	// @audit-issue

144:            emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);	// @audit-issue
```
[73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L73-L73), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L85-L85), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L144-L144), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

138:        return uint256(fromLittleEndianUint64(validatorFields[BALANCE_IDX])) * 1 gwei;	// @audit-issue

142:        return validatorFields[PUBKEY_IDX];	// @audit-issue

146:        return fromLittleEndianUint64(validatorFields[EXIT_EPOCH_IDX]);	// @audit-issue

150:        return validatorFields[WITHDRAWAL_CREDENTIALS_IDX];	// @audit-issue
```
[138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L138-L138), [142](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L142-L142), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L146-L146), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L150-L150), 


```solidity
Path: ./src/entities/MerkleProofs.sol

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), 


```solidity
Path: ./src/utils/ExtSloads.sol

15:            bytes32 slot = slots[i++];	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L15-L15), 


```solidity
Path: ./src/utils/CommonUtils.sol

17:            if (arr[i] <= arr[pivot]) {	// @audit-issue

31:        arr[left] = arr[right];	// @audit-issue

32:        arr[right] = temp;	// @audit-issue

43:            if (arr[i] == arr[i + 1]) return true;	// @audit-issue
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L17-L17), [31](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L31-L31), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L32-L32), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L43-L43), 


#### Recommendation

Integrate explicit index validation checks at the beginning of functions that operate based on index elements. Use conditional statements to verify that the provided index falls within the valid range of existing elements. For array operations, ensure the index is less than the array's length. For mappings, consider additional logic to confirm the presence of a key. For example, in an array-based function:
```solidity
function getElementByIndex(uint256 index) public view returns (ElementType) {
    require(index < array.length, "Index out of bounds");
    return array[index];
}
```


### Contract should expose an `interface`
All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.


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
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


#### Recommendation

Consider defining an `interface` that includes all `external`/`public` functions of the contract. Exposing a well-defined interface helps ensure that the entire API is extracted and provides a clear and standardized way for other contracts or users to interact with your contract.

### Polymorphic functions make security audits more time-consuming and error-prone
The instances below point to one of two functions with the same name. Consider naming each function differently, in order to make code navigation and analysis easier.

```solidity
Path: ./src/Core.sol

318:    function implementation(address vault) public view returns (address) {	// @audit-issue same function also on line(s): 308
```
[318](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L318-L318), 


```solidity
Path: ./src/Vault.sol

94:    function deposit(uint256 assets, address to, uint256 minSharesOut)	// @audit-issue same function also on line(s): 78
```
[94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L94-L94), 


```solidity
Path: ./src/entities/Pauser.sol

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue same function also on line(s): 54
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), 


#### Recommendation

Rename one or both of the polymorphic functions to have distinct names, improving code readability and making security audits more efficient and less error-prone. Clear and unique function names help prevent confusion and ensure that the intended function is called.

### Consider using named returns
Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

```solidity
Path: ./src/Core.sol

288:    function isAssetAllowlisted(address asset) public view returns (bool) {	// @audit-issue

294:    function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {	// @audit-issue

302:    function isOperatorRegisteredToDSS(address operator, IDSS dss) public view returns (bool) {	// @audit-issue

308:    function implementation() external view override returns (address) {	// @audit-issue

318:    function implementation(address vault) public view returns (address) {	// @audit-issue

365:    function isDSSRegistered(IDSS dss) public view returns (bool) {	// @audit-issue
```
[288](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L288-L288), [294](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L294-L294), [302](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L302-L302), [308](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L308-L308), [318](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L318-L318), [365](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L365-L365), 


```solidity
Path: ./src/NativeVault.sol

95:    function createNode()
96:        external
97:        nonReentrant
98:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_CREATE_NODE)
99:        returns (address)	// @audit-issue

346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue

351:    function activeValidatorCount(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)
364:        public
365:        view
366:        returns (NativeVaultLib.QueuedWithdrawal memory)	// @audit-issue

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)
376:        external
377:        view
378:        nodeExists(nodeOwner)
379:        returns (NativeVaultLib.ValidatorDetails memory)	// @audit-issue

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue

392:    function currentSnapshot(address nodeOwner)
393:        external
394:        view
395:        nodeExists(nodeOwner)
396:        returns (NativeVaultLib.Snapshot memory)	// @audit-issue

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

627:    function implementation() external view override returns (address) {	// @audit-issue

631:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L95-L99), [346](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L346-L346), [351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L351-L351), [355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [366](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L366), [371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), [379](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L379), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [396](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L396), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), [631](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L631-L631), 


```solidity
Path: ./src/Vault.sol

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue

237:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue

243:    function getNextWithdrawNonce(address staker) public view returns (uint256) {	// @audit-issue

250:    function isWithdrawalPending(address staker, uint256 _withdrawNonce) public view returns (bool) {	// @audit-issue

258:    function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)
259:        public
260:        view
261:        returns (WithdrawLib.QueuedWithdrawal memory)	// @audit-issue

267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue

272:    function owner() public view override(Ownable, IVault) returns (address) {	// @audit-issue

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue
```
[222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L237-L237), [243](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L243-L243), [250](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L250-L250), [261](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L258-L261), [267](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L267-L267), [272](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L272-L272), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), 


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)
136:        internal
137:        view
138:        returns (bool)	// @audit-issue

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L138), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), 


```solidity
Path: ./src/entities/CoreLib.sol

89:    function createVault(
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,
94:        string memory symbol,
95:        bytes memory extraData,
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {	// @audit-issue

118:    function deployVaults(
119:        Storage storage self,
120:        address operator,
121:        address implementation,
122:        VaultLib.Config[] calldata vaultConfigs
123:    ) external returns (IKarakBaseVault[] memory) {	// @audit-issue

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), [123](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L123), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue
```
[170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue
```
[137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)
30:        internal
31:        pure
32:        returns (bool)	// @audit-issue

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)
49:        internal
50:        pure
51:        returns (bytes32)	// @audit-issue

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)
86:        internal
87:        view
88:        returns (bool)	// @audit-issue

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)
104:        internal
105:        view
106:        returns (bytes32)	// @audit-issue

141:    function merkleizeSha256(bytes32[] memory leaves) internal pure returns (bytes32) {	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L32), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L51), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L88), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L106), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L141-L141), 


```solidity
Path: ./src/entities/HookLib.sol

48:    function callHook(
49:        address target,
50:        bytes memory data,
51:        bool ignoreFailure,
52:        uint32 hookCallGasLimit,
53:        uint32 hookGasBuffer
54:    ) internal returns (bool) {	// @audit-issue

78:    function callHookIfInterfaceImplemented(
79:        IERC165 dss,
80:        bytes memory data,
81:        bytes4 interfaceId,
82:        bool ignoreFailure,
83:        uint32 hookCallGasLimit,
84:        uint32 supportsInterfaceGasLimit,
85:        uint32 hookGasBuffer
86:    ) internal returns (bool) {	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L54), [86](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L78-L86), 


```solidity
Path: ./src/entities/Pauser.sol

54:    function paused() public view virtual returns (bool) {	// @audit-issue

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue

63:    function pausedMap() public view virtual returns (uint256) {	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L54-L54), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), [63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L63-L63), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)
94:        internal
95:        returns (address)	// @audit-issue

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue

146:    function validateWithdrawalCredentials(
147:        Storage storage self,
148:        address nodeOwner,
149:        uint64 updateTimestamp,
150:        bytes32 beaconStateRoot,
151:        BeaconProofs.ValidatorFieldsProof calldata validatorFieldsProof
152:    ) internal returns (uint256) {	// @audit-issue
```
[95](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L95), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [152](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L152), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Adopt named returns in your Solidity functions, especially in cases where functions contain a single return statement. This approach enhances code readability and documentation by making the return values clear and explicit. When defining your function, specify the return types with names, and manipulate these named variables directly within your function logic. Additionally, leverage named returns to streamline your NatSpec documentation, providing clear descriptions for each return variable. Evaluate your current contracts for opportunities to refactor functions to use named returns, prioritizing those with simple return patterns for immediate benefits in gas efficiency and code clarity.

### Use `abi.encodeCall()` instead of `abi.encodeWithSignature()`/`abi.encodeWithSelector()`
Starting with version 0.8.11, abi.encodeCall() has compiler [type safety](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/3693), whereas the other two functions do not.

```solidity
Path: ./src/entities/Operator.sol

80:            data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate),	// @audit-issue

126:            data: abi.encodeWithSelector(dss.finishUpdateStakeHook.selector, msg.sender),	// @audit-issue

164:            data: abi.encodeWithSelector(dss.registrationHook.selector, operator, registrationHookData),	// @audit-issue

196:            data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData),	// @audit-issue
```
[80](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L80-L80), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L126-L126), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L164-L164), [196](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L196-L196), 


```solidity
Path: ./src/entities/SlasherLib.sol

115:            data: abi.encodeWithSelector(	// @audit-issue
116:                dss.requestSlashingHook.selector, slashingMetadata.operator, slashingMetadata.slashPercentagesWad
117:            ),

144:            data: abi.encodeWithSelector(dss.finishSlashingHook.selector, queuedSlashing.operator),	// @audit-issue

161:            data: abi.encodeWithSelector(dss.cancelSlashingHook.selector, queuedSlashing.operator),	// @audit-issue
```
[115](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L115-L117), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L144-L144), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L161-L161), 


```solidity
Path: ./src/entities/HookLib.sol

93:            abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId),	// @audit-issue
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L93-L93), 


#### Recommendation

In Solidity version 0.8.11 and later, it's recommended to use `abi.encodeCall()` for creating function call data, as it provides better type safety compared to `abi.encodeWithSignature()` or `abi.encodeWithSelector()`. This helps prevent type-related errors and ensures more reliable contract interactions.

### Missing events in initializers/deploys
As a best practice, consider emitting an event when the contract is initialized. In this way, it's easy for the user to track the exact point in time when the contract was initialized, by filtering the emitted events.

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

To provide transparency and enable users to track the initialization of the contract, consider emitting an event within the contract's initializer function. Emitting an event during initialization can help users pinpoint the exact moment the contract was initialized by filtering and monitoring the emitted events.

### Inefficient Array Usage
Use mappings instead of arrays for managing lists of data in order to conserve gas. Mappings are less expensive and more efficient for accessing any value without having to iterate through an array.

```solidity
Path: ./src/Querier.sol

27:        address[] memory stakedVaults = core.fetchVaultsStakedInDSS(operator, dss);	// @audit-issue

28:        bytes32[] memory slots = new bytes32[](stakedVaults.length);	// @audit-issue

32:        bytes32[] memory results = core.extSloads(slots);	// @audit-issue
```
[27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L27-L27), [28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L28-L28), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L32-L32), 


```solidity
Path: ./src/SlashingHandler.sol

33:    function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer {	// @audit-issue
```
[33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L33-L33), 


```solidity
Path: ./src/Core.sol

85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

161:    function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)	// @audit-issue

373:    function extSloads(bytes32[] calldata slots)	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L85-L85), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L161-L161), [373](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L373-L373), 


```solidity
Path: ./src/NativeVault.sol

128:        BeaconProofs.BalanceProof[] calldata balanceProofs,	// @audit-issue

171:        BeaconProofs.ValidatorFieldsProof[] calldata validatorFieldsProofs	// @audit-issue
```
[128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L128-L128), [171](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L171-L171), 


```solidity
Path: ./src/Vault.sol

285:    function extSloads(bytes32[] calldata slots)	// @audit-issue
```
[285](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L285-L285), 


```solidity
Path: ./src/entities/Operator.sol

189:        address[] memory vaults = getVaultsStakedToDSS(operatorState, dss);	// @audit-issue

230:        address[] memory dssAddresses = getDSSsOperatorIsRegisteredTo(self, operator);	// @audit-issue
```
[189](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L189-L189), [230](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L230-L230), 


```solidity
Path: ./src/entities/CoreLib.sol

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue

122:        VaultLib.Config[] calldata vaultConfigs	// @audit-issue

125:        IKarakBaseVault[] memory vaults = new IKarakBaseVault[](vaultConfigs.length);	// @audit-issue
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), [122](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L122-L122), [125](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L125-L125), 


```solidity
Path: ./src/entities/SlasherLib.sol

101:        uint256[] memory earmarkedStakes = fetchEarmarkedStakes(slashingMetadata);	// @audit-issue
```
[101](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L101-L101), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

75:        bytes32[] calldata validatorFields,	// @audit-issue

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue
```
[75](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L75-L75), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

112:        bytes32[1] memory computedHash = [leaf];	// @audit-issue

141:    function merkleizeSha256(bytes32[] memory leaves) internal pure returns (bytes32) {	// @audit-issue

145:        bytes32[] memory layer = new bytes32[](numNodesInLayer);	// @audit-issue
```
[112](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L112-L112), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L145-L145), 


```solidity
Path: ./src/entities/HookLib.sol

20:        bytes32[1] memory returnData;	// @audit-issue
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L20-L20), 


```solidity
Path: ./src/utils/ExtSloads.sol

9:    function extSloads(bytes32[] calldata slots) public view virtual returns (bytes32[] memory res) {	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L9-L9), 


```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), 


#### Recommendation

In scenarios where data access efficiency is critical, prefer using mappings over arrays in Solidity contracts. Mappings offer more efficient and gas-effective data retrieval and updates, especially when dealing with large or frequently accessed datasets. Ensure to structure your data and choose keys thoughtfully to maximize the efficiency gains offered by mappings. While arrays might be suitable for ordered data or when the entire dataset needs to be iterated, for most other use cases, mappings are likely to be the more gas-efficient choice.

### Enum values should be used in place of constant array indexes
Consider using an `enum` instead of hardcoding an index access to make the code easier to understand.

```solidity
Path: ./src/entities/MerkleProofs.sol

132:        return computedHash[0];	// @audit-issue

162:        return layer[0];	// @audit-issue
```
[132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L132-L132), [162](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L162-L162), 


```solidity
Path: ./src/entities/HookLib.sol

38:        returnVal = returnData[0];	// @audit-issue
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L38-L38), 


#### Recommendation

To improve code readability and maintainability, replace hardcoded array indexes with corresponding enum values. Enum values provide descriptive names for array elements, making your code more self-explanatory and reducing the risk of errors when working with arrays. This enhances the overall clarity and robustness of your smart contract code.

### Complex math should be split into multiple steps
Consider splitting long arithmetic calculations (more than 4 operations) into multiple steps to improve the code readability.

```solidity
Path: ./src/entities/BeaconProofsLib.sol

56:        return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)	// @audit-issue
57:            | ((0x000000FF00000000 & n) >> 8) | ((0x00000000FF000000 & n) << 8) | ((0x0000000000FF0000 & n) << 24)
58:            | ((0x000000000000FF00 & n) << 40) | ((0x00000000000000FF & n) << 56);

56:        return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)	// @audit-issue
57:            | ((0x000000FF00000000 & n) >> 8) | ((0x00000000FF000000 & n) << 8) | ((0x0000000000FF0000 & n) << 24)

56:        return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)	// @audit-issue
```
[56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L56-L58), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L56-L57), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L56-L56), 


#### Recommendation

To enhance code readability and maintainability, it's advisable to break down complex arithmetic calculations into multiple steps. This not only makes the code more understandable but also helps in debugging and verifying the correctness of calculations.

### Lack of specific import identifier
It is better to use `import {<identifier>} from "<file.sol>"` instead of `import "<file.sol>"` to improve readability and speed up the compilation time.

```solidity
Path: ./src/NativeNode.sol

13:import "./interfaces/Errors.sol";	// @audit-issue

14:import "./interfaces/Events.sol";	// @audit-issue

15:import "./interfaces/Constants.sol";	// @audit-issue
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L13-L13), [14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L14-L14), [15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L15-L15), 


```solidity
Path: ./src/SlashStore.sol

10:import "./interfaces/Events.sol";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L10-L10), 


```solidity
Path: ./src/Querier.sol

6:import "./entities/CoreStorageSlots.sol";	// @audit-issue

7:import "./Core.sol";	// @audit-issue
```
[6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L6-L6), [7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L7-L7), 


```solidity
Path: ./src/SlashingHandler.sol

9:import "./interfaces/ISlashingHandler.sol";	// @audit-issue

10:import "./interfaces/Errors.sol";	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L10-L10), 


```solidity
Path: ./src/Core.sol

22:import "./interfaces/Errors.sol";	// @audit-issue

23:import "./interfaces/Events.sol";	// @audit-issue

24:import "./interfaces/Constants.sol";	// @audit-issue
```
[22](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L22-L22), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L23-L23), [24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L24-L24), 


```solidity
Path: ./src/NativeVault.sol

21:import "./interfaces/Errors.sol";	// @audit-issue

22:import "./interfaces/Events.sol";	// @audit-issue

23:import "./interfaces/Constants.sol";	// @audit-issue
```
[21](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L21-L21), [22](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L22-L22), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L23-L23), 


```solidity
Path: ./src/Vault.sol

23:import "./interfaces/Errors.sol";	// @audit-issue

24:import "./interfaces/Events.sol";	// @audit-issue
```
[23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L23-L23), [24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L24-L24), 


```solidity
Path: ./src/entities/Operator.sol

10:import "../interfaces/Errors.sol";	// @audit-issue

11:import "../interfaces/Constants.sol";	// @audit-issue

12:import "../interfaces/IDSS.sol";	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L11-L11), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L12-L12), 


```solidity
Path: ./src/entities/CoreLib.sol

12:import "../interfaces/Constants.sol";	// @audit-issue

13:import "../interfaces/Errors.sol";	// @audit-issue

14:import "../interfaces/Events.sol";	// @audit-issue
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L12-L12), [13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L13-L13), [14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L14-L14), 


```solidity
Path: ./src/entities/SlasherLib.sol

5:import "@openzeppelin/contracts/utils/structs/EnumerableMap.sol";	// @audit-issue

12:import "../interfaces/Errors.sol";	// @audit-issue

13:import "../interfaces/Constants.sol";	// @audit-issue

14:import "../interfaces/IDSS.sol";	// @audit-issue

15:import "../interfaces/IKarakBaseVault.sol";	// @audit-issue

16:import "../interfaces/Events.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L5-L5), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L12-L12), [13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L13-L13), [14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L14-L14), [15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L15-L15), [16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L16-L16), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

4:import "../interfaces/Errors.sol";	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L4-L4), 


```solidity
Path: ./src/entities/VaultLib.sol

5:import "./Withdraw.sol";	// @audit-issue

6:import "../interfaces/Errors.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L6-L6), 


```solidity
Path: ./src/entities/HookLib.sol

5:import "@openzeppelin/contracts/interfaces/IERC165.sol";	// @audit-issue

6:import "../interfaces/Errors.sol";	// @audit-issue

7:import "../interfaces/Events.sol";	// @audit-issue
```
[5](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L5-L5), [6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L6-L6), [7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L7-L7), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

6:import "./VaultLib.sol";	// @audit-issue

7:import "../interfaces/Errors.sol";	// @audit-issue

8:import "../interfaces/Events.sol";	// @audit-issue

9:import "../interfaces/Constants.sol";	// @audit-issue

10:import "../interfaces/INativeNode.sol";	// @audit-issue

12:import "../entities/BeaconProofsLib.sol";	// @audit-issue
```
[6](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L6-L6), [7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L7-L7), [8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L8-L8), [9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L10-L10), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L12-L12), 


#### Recommendation

To improve code clarity and avoid naming conflicts, it's recommended to use specific import identifiers when importing from other contracts or libraries. Instead of using `import "<file.sol>";`, specify the desired identifiers using `import { <identifier1>, <identifier2> } from "<file.sol>";`. This not only enhances readability but also can speed up compilation times by only importing the necessary symbols.

### Consider using a `struct` rather than having many function input parameters
In Solidity, functions with a large number of input parameters can become cumbersome to manage and call. This can lead to readability issues and increased likelihood of errors, especially if the order of parameters is complex or not intuitive. To streamline this, consider consolidating multiple parameters into a single `struct`. This approach not only simplifies function signatures but also enhances code clarity. Structs allow for grouping related data together, making it easier to understand the relationship between parameters and manage them as a single entity.

```solidity
Path: ./src/Core.sol

53:    function initialize(
54:        address _vaultImpl,
55:        address _manager,
56:        address _vetoCommittee,
57:        uint32 _hookCallGasLimit,
58:        uint32 _supportsInterfaceGasLimit,
59:        uint32 _hookGasBuffer
60:    ) external initializer {
```
[68](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L53-L60), 


```solidity
Path: ./src/NativeVault.sol

46:    function initialize(
47:        address _owner,
48:        address _operator,
49:        address _depositToken,
50:        string memory _name,
51:        string memory _symbol,
52:        bytes memory _extraData
53:    ) external initializer {
```
[79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L53), 


```solidity
Path: ./src/Vault.sol

51:    function initialize(
52:        address _owner,
53:        address _operator,
54:        address _depositToken,
55:        string memory _name,
56:        string memory _symbol,
57:        bytes memory _extraData
58:    ) external initializer {
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L58), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(
41:        Storage storage self,
42:        address _vaultImpl,
43:        address _vetoCommittee,
44:        uint32 _hookCallGasLimit,
45:        uint32 _supportsInterfaceGasLimit,
46:        uint32 _hookGasBuffer
47:    ) internal {

89:    function createVault(
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,
94:        string memory symbol,
95:        bytes memory extraData,
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L47), [116](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), 


```solidity
Path: ./src/entities/HookLib.sol

48:    function callHook(
49:        address target,
50:        bytes memory data,
51:        bool ignoreFailure,
52:        uint32 hookCallGasLimit,
53:        uint32 hookGasBuffer
54:    ) internal returns (bool) {

78:    function callHookIfInterfaceImplemented(
79:        IERC165 dss,
80:        bytes memory data,
81:        bytes4 interfaceId,
82:        bool ignoreFailure,
83:        uint32 hookCallGasLimit,
84:        uint32 supportsInterfaceGasLimit,
85:        uint32 hookGasBuffer
86:    ) internal returns (bool) {
```
[64](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L54), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L78-L86), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

110:    function validateSnapshotProof(
111:        Storage storage self,
112:        address nodeOwner,
113:        ValidatorDetails memory validatorDetails,
114:        bytes32 balanceRoot,
115:        BeaconProofs.BalanceProof calldata proof
116:    ) internal returns (int256 balanceDeltaWei) {

146:    function validateWithdrawalCredentials(
147:        Storage storage self,
148:        address nodeOwner,
149:        uint64 updateTimestamp,
150:        bytes32 beaconStateRoot,
151:        BeaconProofs.ValidatorFieldsProof calldata validatorFieldsProof
152:    ) internal returns (uint256) {
```
[144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L116), [192](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L152), 


#### Recommendation

When faced with functions having numerous input parameters, refactor them to accept a `struct` instead. Define a `struct` that encapsulates all these parameters, thereby simplifying the function signature and improving code readability and maintainability. This method is particularly effective in complex functions or those with parameters that are logically related, making the code more intuitive and less error-prone.

### Some variables have a implicit default visibility
Consider always adding an explicit visibility modifier for variables, as the default is `internal`.

```solidity
Path: ./src/NativeNode.sol

18:    address nodeOwner;	// @audit-issue
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L18-L18), 


#### Recommendation

Always add an explicit visibility modifier for variables to enhance code clarity and avoid potential issues. The default visibility for variables is `internal`, but specifying it explicitly makes your intentions clear.

### Outdated Solidity Version
The current Solidity version used in the contract is outdated. Consider using a more recent version for improved features and security.

0.8.4: bytes.concat() instead of abi.encodePacked(,)

0.8.12: string.concat() instead of abi.encodePacked(,)

0.8.13: Ability to use using for with a list of free functions

0.8.14: ABI Encoder: When ABI-encoding values from calldata that contain nested arrays, correctly validate the nested array length against calldatasize() in all cases. Override Checker: Allow changing data location for parameters only when overriding external functions.

0.8.15: Code Generation: Avoid writing dirty bytes to storage when copying bytes arrays. Yul Optimizer: Keep all memory side-effects of inline assembly blocks.

0.8.16: Code Generation: Fix data corruption that affected ABI-encoding of calldata values represented by tuples: structs at any nesting level; argument lists of external functions, events and errors; return value lists of external functions. The 32 leading bytes of the first dynamically-encoded value in the tuple would get zeroed when the last component contained a statically-encoded array.

0.8.17: Yul Optimizer: Prevent the incorrect removal of storage writes before calls to Yul functions that conditionally terminate the external EVM call.


```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L4), 


#### Recommendation

Upgrade the contract to a more recent version of Solidity to take advantage of the latest features, improvements, and security enhancements. It's important to stay up-to-date with the Solidity releases to ensure the contract's robustness and compatibility with the Ethereum ecosystem.

### Unnecessary Use of override Keyword
In Solidity version 0.8.8 and later, the use of the override keyword becomes superfluous when a function is overriding solely from an interface and the function isn't present in multiple base contracts. Previously, the override keyword was required as an explicit indication to the compiler. However, this is no longer the case, and the extraneous use of the keyword can make the code less clean and more verbose.
Solidity documentation on [Function Overriding](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding).


```solidity
Path: ./src/Core.sol

308:    function implementation() external view override returns (address) {	// @audit-issue

373:    function extSloads(bytes32[] calldata slots)	// @audit-issue
374:        public
375:        view
376:        override(ExtSloads, ICore)
377:        returns (bytes32[] memory res)
378:    {
```
[308](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L308-L308), [373](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L373-L378), 


```solidity
Path: ./src/NativeVault.sol

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

627:    function implementation() external view override returns (address) {	// @audit-issue
```
[536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)	// @audit-issue
79:        public
80:        override(ERC4626, IVault)
81:        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
82:        nonReentrant
83:        returns (uint256 shares)
84:    {

110:    function mint(uint256 shares, address to)	// @audit-issue
111:        public
112:        override(ERC4626, IVault)
113:        whenFunctionNotPaused(Constants.PAUSE_VAULT_MINT)
114:        nonReentrant
115:        returns (uint256 assets)
116:    {

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue

267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue

272:    function owner() public view override(Ownable, IVault) returns (address) {	// @audit-issue

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue

285:    function extSloads(bytes32[] calldata slots)	// @audit-issue
286:        public
287:        view
288:        override(ExtSloads, IVault)
289:        returns (bytes32[] memory res)
290:    {

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue
332:        public
333:        override
334:        whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:        nonReentrant
336:        returns (uint256 shares)
337:    {

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue
349:        public
350:        override
351:        whenFunctionNotPaused(Constants.PAUSE_VAULT_REDEEM)
352:        nonReentrant
353:        returns (uint256 assets)
354:    {
```
[78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L84), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L110-L116), [222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [267](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L267-L267), [272](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L272-L272), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [285](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L285-L290), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L337), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L354), 


#### Recommendation

In Solidity versions 0.8.8 and later, the `override` keyword is no longer required for functions that are solely overriding from an interface and not present in multiple base contracts. Removing the unnecessary `override` keyword can make the code cleaner and less verbose.

### Use a single file for all system-wide constants
System-wide constants should be declared in a single file for better maintainability and readability. This contract seems to contain constants which could potentially be system-wide and could be better managed if they were centralized in a single location.

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


```solidity
Path: ./src/entities/BeaconProofsLib.sol

9:    uint256 internal constant BEACON_STATE_HEIGHT = 5;	// @audit-issue

10:    uint256 internal constant BEACON_STATE_ROOT_IDX = 3;	// @audit-issue

11:    uint256 internal constant BEACON_BLOCK_HEADER_HEIGHT = 3;	// @audit-issue

14:    uint256 internal constant PUBKEY_IDX = 0;	// @audit-issue

15:    uint256 internal constant NUM_FIELDS = 8;	// @audit-issue

16:    uint256 internal constant BALANCE_IDX = 2;	// @audit-issue

17:    uint256 internal constant CONTAINER_IDX = 11;	// @audit-issue

18:    uint256 internal constant EXIT_EPOCH_IDX = 6;	// @audit-issue

19:    uint256 internal constant VALIDATOR_HEIGHT = 40;	// @audit-issue

20:    uint256 internal constant WITHDRAWAL_CREDENTIALS_IDX = 1;	// @audit-issue

23:    uint256 internal constant BALANCE_CONTAINER_IDX = 12;	// @audit-issue

24:    uint256 internal constant BALANCE_HEIGHT = 38;	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L11-L11), [14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L14-L14), [15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L15-L15), [16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L16-L16), [17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L17-L17), [18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L18-L18), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L19-L19), [20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L20-L20), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L23-L23), [24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L24-L24), 


#### Recommendation

Consider centralizing system-wide constants in a single file for better maintainability and readability. This practice makes it easier to manage and update constants across the contract and promotes consistency in your codebase.

### Include sender information in events
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

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
Path: ./src/Core.sol

90:        emit AllowlistedAssets(assets);	// @audit-issue

106:        emit RegisteredOperatorToDSS(operator, address(dss));	// @audit-issue

123:        emit UnregisteredOperatorToDSS(operator, address(dss));	// @audit-issue

140:        emit RequestedStakeUpdate(updatedStake);	// @audit-issue

152:        emit FinishedStakeUpdate(queuedStake);	// @audit-issue

177:        emit UpgradedAllVaults(newVaultImpl);	// @audit-issue

191:        emit UpgradedVault(newVaultImpl, vault);	// @audit-issue

230:        emit RequestedSlashing(address(dss), slashingRequest);	// @audit-issue
```
[90](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L90-L90), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L106-L106), [123](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L123-L123), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L140-L140), [152](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L152-L152), [177](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L177-L177), [191](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L191-L191), [230](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L230-L230), 


```solidity
Path: ./src/NativeVault.sol

78:        emit NativeVaultInitialized(_owner, manager, _operator, slashStore);	// @audit-issue

91:        emit UpgradedAllNodes(newNodeImplementation);	// @audit-issue

255:        emit StartedWithdraw(nodeOwner, _config().operator, withdrawalKey, weiAmount, to);	// @audit-issue

287:        emit FinishedWithdraw(	// @audit-issue

316:        emit Slashed(totalAssetsToSlash);	// @audit-issue

473:        emit SnapshotCreated(nodeOwner, node.nodeAddress, uint64(block.timestamp), snapshot.parentBeaconBlockRoot);	// @audit-issue

491:            emit SnapshotFinished(nodeOwner, node.nodeAddress, node.lastSnapshotTimestamp, totalDeltaWei);	// @audit-issue

504:        emit IncreasedBalance(self.ownerToNode[_of].totalRestakedETH);	// @audit-issue

514:        emit DecreasedBalance(self.ownerToNode[_of].totalRestakedETH);	// @audit-issue
```
[78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L78-L78), [91](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L91-L91), [255](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L255-L255), [287](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L287-L287), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L316-L316), [473](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L473-L473), [491](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L491-L491), [504](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L504-L504), [514](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L514-L514), 


```solidity
Path: ./src/Vault.sol

148:        emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);	// @audit-issue

180:        emit FinishedRedeem(	// @audit-issue

204:        emit Slashed(transferAmount);	// @audit-issue
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L148-L148), [180](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L180-L180), [204](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L204-L204), 


```solidity
Path: ./src/entities/CoreLib.sol

114:        emit NewVault(address(vault), implementation);	// @audit-issue

144:            emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);	// @audit-issue
```
[114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L114-L114), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L144-L144), 


```solidity
Path: ./src/entities/HookLib.sol

61:        if (success) emit HookCallSucceeded(returnData);	// @audit-issue

62:        else emit HookCallFailed(returnData);	// @audit-issue

99:            emit InterfaceNotSupported();	// @audit-issue
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L61-L61), [62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L62-L62), [99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L99-L99), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

131:            emit ValidatorWithdrawn(nodeOwner, nodeAddress, timestamp, validatorIndex);	// @audit-issue

135:        emit SnapshotValidator(nodeOwner, nodeAddress, timestamp, validatorIndex);	// @audit-issue

138:            emit ValidatorBalanceChanged(nodeOwner, nodeAddress, validatorIndex, timestamp, newBalanceWei);	// @audit-issue

184:        emit RestakedValidator(	// @audit-issue
```
[131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L131-L131), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L135-L135), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L138-L138), [184](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L184-L184), 


#### Recommendation

To improve the usability and analysis of your smart contract events, consider including the `msg.sender` address as part of the event data. This enables easier filtering and identification of the sender's actions within your contract, providing valuable insights for users and external tools.

### Don't use `_msgSender()` if not supporting EIP-2771
Use `msg.sender` if the code does not implement [EIP-2771 trusted forwarder](https://eips.ethereum.org/EIPS/eip-2771) support.

```solidity
Path: ./src/entities/Pauser.sol

71:        emit Paused(_msgSender(), map);	// @audit-issue

78:        emit Unpaused(_msgSender(), map);	// @audit-issue
```
[71](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L71-L71), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L78-L78), 


#### Recommendation

Consider refactoring your code by moving `msg.sender` checks to modifiers when certain functions are only allowed to be called by specific users. This approach can enhance code readability, reduce redundancy, and make it easier to maintain access control logic.

### Avoid external calls in modifiers
It is unusual to have external calls in modifiers, and doing so will make reviewers more likely to miss important external interactions. Consider moving the external call to an internal function, and calling that function from the modifier.

```solidity
Path: ./src/NativeVault.sol

530:        if (_state().ownerToNode[owner].nodeAddress == address(0)) revert NotNodeOwner();	// @audit-issue
```
[530](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L530-L530), 


#### Recommendation

Refrain from incorporating external calls directly within modifiers. Instead, encapsulate the external call within an internal function and invoke this function from within the body of the functions that use the modifier. This approach enhances code readability and security, making it easier for reviewers and auditors to track external interactions. Additionally, it centralizes external calls, simplifying the management and review of these potentially risky operations. Always ensure external calls are handled with care, implementing checks, balances, and reentrancy guards as necessary to protect your contract from malicious actors and unintended consequences.

### Unnecessary Constant Variable in Function Parameters
Passing a constant variable as a function parameter is redundant because the function can access the constant directly.

```solidity
Path: ./src/NativeVault.sol

161:        _updateSnapshot(node, snapshot, nodeOwner);	// @audit-issue

203:        _increaseBalance(nodeOwner, totalRestakedWei);	// @audit-issue

222:        _startSnapshot(node, false, nodeOwner);	// @audit-issue

456:        _transferToSlashStore(nodeOwner);	// @audit-issue

471:        _updateSnapshot(node, snapshot, nodeOwner);	// @audit-issue

490:            _updateBalance(nodeOwner, totalDeltaWei);	// @audit-issue
```
[161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L161-L161), [203](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L203-L203), [222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L222-L222), [456](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L456-L456), [471](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L471-L471), [490](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L490-L490), 


```solidity
Path: ./src/entities/Operator.sol

145:        if (!isOperatorRegisteredToDSS(self, operator, dss)) {	// @audit-issue

157:        if (isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorAlreadyRegisteredToDSS();	// @audit-issue

189:        address[] memory vaults = getVaultsStakedToDSS(operatorState, dss);	// @audit-issue

191:        if (!isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorNotValidatingForDSS();	// @audit-issue

230:        address[] memory dssAddresses = getDSSsOperatorIsRegisteredTo(self, operator);	// @audit-issue
```
[145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L145-L145), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L157-L157), [189](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L189-L189), [191](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L191-L191), [230](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L230-L230), 


```solidity
Path: ./src/entities/CoreLib.sol

81:        if (!(implementation == address(0) || isVaultImplAllowlisted(self, implementation))) {	// @audit-issue

124:        validateVaultConfigs(self, vaultConfigs, implementation);	// @audit-issue

133:            IKarakBaseVault vault = createVault(
134:                self,
135:                operator,	// @audit-issue
136:                vaultConfigs[i].asset,
137:                vaultConfigs[i].name,
138:                vaultConfigs[i].symbol,
139:                vaultConfigs[i].extraData,
140:                implementation
141:            );

133:            IKarakBaseVault vault = createVault(
134:                self,
135:                operator,
136:                vaultConfigs[i].asset,
137:                vaultConfigs[i].name,
138:                vaultConfigs[i].symbol,
139:                vaultConfigs[i].extraData,
140:                implementation	// @audit-issue
141:            );
```
[81](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L81-L81), [124](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L124-L124), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L133-L141), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L133-L141), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

24:        return bytes32(uint256(operatorStateSlot(operator)) + PENDING_STAKE_UPDATE_MAPPING_OFFSET);	// @audit-issue

28:        return keccak256(abi.encode(vault, pendingStakeUpdateMappingSlot(operator)));	// @audit-issue
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L24-L24), [28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L28-L28), 


```solidity
Path: ./src/entities/SlasherLib.sol

49:        uint256 maxSlashPercentageWad = getDSSMaxSlashablePercentageWad(self, dss);	// @audit-issue

76:        validateVaultsAndSlashPercentages(self, slashingRequest, dss);	// @audit-issue

100:        validateRequestSlashingParams(self, slashingMetadata, dss);	// @audit-issue

110:        self.slashingRequests[calculateRoot(queuedSlashing)] = true;	// @audit-issue

127:        bytes32 slashRoot = calculateRoot(queuedSlashing);	// @audit-issue

154:        bytes32 slashRoot = calculateRoot(queuedSlashing);	// @audit-issue
```
[49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L49-L49), [76](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L76-L76), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L100-L100), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L110-L110), [127](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L127-L127), [154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L154-L154), 


#### Recommendation


        Reference constant variables directly within the function body instead of passing them as parameters. This simplifies the function signature and conserves gas.


### Control structures do not follow the Solidity Style Guide
Refer to the [Solidity style guide - Control Structures](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#control-structures).

```solidity
Path: ./src/NativeNode.sol

39:    function withdraw(address to, uint256 weiAmount)	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L39), 


```solidity
Path: ./src/Core.sol

85:    function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

97:    function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)	// @audit-issue

113:    function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)	// @audit-issue

130:    function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)
131:        external
132:        nonReentrant
133:        whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_STAKE_UPDATE)
134:        returns (Operator.QueuedStakeUpdate memory updatedStake)	// @audit-issue

146:    function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake)	// @audit-issue

161:    function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)
162:        external
163:        whenFunctionNotPaused(Constants.PAUSE_CORE_DEPLOY_VAULTS)
164:        nonReentrant
165:        returns (IKarakBaseVault[] memory vaults)	// @audit-issue

220:    function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)
221:        external
222:        whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
223:        nonReentrant
224:        returns (SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue

248:    function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue

274:    function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)	// @audit-issue

373:    function extSloads(bytes32[] calldata slots)
374:        public
375:        view
376:        override(ExtSloads, ICore)
377:        returns (bytes32[] memory res)	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L85-L85), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L97-L97), [113](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L113-L113), [134](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L130-L134), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L146-L146), [165](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L161-L165), [224](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L220-L224), [235](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L235), [248](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L248-L248), [274](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L274-L274), [377](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L373-L377), 


```solidity
Path: ./src/NativeVault.sol

83:    function changeNodeImplementation(address newNodeImplementation)	// @audit-issue

95:    function createNode()
96:        external
97:        nonReentrant
98:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_CREATE_NODE)
99:        returns (address)	// @audit-issue

112:    function startSnapshot(bool revertIfNoBalanceChange)	// @audit-issue

126:    function validateSnapshotProofs(
127:        address nodeOwner,
128:        BeaconProofs.BalanceProof[] calldata balanceProofs,
129:        BeaconProofs.BalanceContainer calldata balanceContainer
130:    )	// @audit-issue

168:    function validateWithdrawalCredentials(
169:        address nodeOwner,
170:        BeaconProofs.BeaconStateRootProof calldata beaconStateRootProof,
171:        BeaconProofs.ValidatorFieldsProof[] calldata validatorFieldsProofs
172:    )	// @audit-issue

184:        if (
185:            beaconStateRootProof.timestamp < node.lastSnapshotTimestamp
186:                || beaconStateRootProof.timestamp < node.currentSnapshotTimestamp	// @audit-issue

210:    function validateExpiredSnapshot(address nodeOwner)	// @audit-issue

228:    function startWithdrawal(address to, uint256 weiAmount)
229:        external
230:        nonReentrant
231:        nodeExists(msg.sender)
232:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_START_WITHDRAWAL)
233:        returns (bytes32 withdrawalKey)	// @audit-issue

262:    function finishWithdrawal(bytes32 withdrawalKey)	// @audit-issue

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
300:        external
301:        onlyOwner
302:        nonReentrant
303:        whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_SLASHER)
304:        returns (uint256 transferAmount)	// @audit-issue

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)
364:        public
365:        view
366:        returns (NativeVaultLib.QueuedWithdrawal memory)	// @audit-issue

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)
376:        external
377:        view
378:        nodeExists(nodeOwner)
379:        returns (NativeVaultLib.ValidatorDetails memory)	// @audit-issue

392:    function currentSnapshot(address nodeOwner)
393:        external
394:        view
395:        nodeExists(nodeOwner)
396:        returns (NativeVaultLib.Snapshot memory)	// @audit-issue

448:    function _startSnapshot(NativeVaultLib.NativeNode storage node, bool revertIfNoBalanceChange, address nodeOwner)	// @audit-issue
```
[83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L83-L83), [99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L95-L99), [112](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L112-L112), [130](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L126-L130), [172](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L168-L172), [186](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L184-L186), [210](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L210-L210), [233](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L228-L233), [262](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L262-L262), [304](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L304), [366](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L366), [379](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L379), [396](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L396), [448](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L448-L448), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)
79:        public
80:        override(ERC4626, IVault)
81:        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
82:        nonReentrant
83:        returns (uint256 shares)	// @audit-issue

94:    function deposit(uint256 assets, address to, uint256 minSharesOut)
95:        external
96:        nonReentrant
97:        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT_SLIPPAGE)
98:        returns (uint256 shares)	// @audit-issue

110:    function mint(uint256 shares, address to)
111:        public
112:        override(ERC4626, IVault)
113:        whenFunctionNotPaused(Constants.PAUSE_VAULT_MINT)
114:        nonReentrant
115:        returns (uint256 assets)	// @audit-issue

125:    function startRedeem(uint256 shares, address beneficiary)
126:        external
127:        whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:        nonReentrant
129:        returns (bytes32 withdrawalKey)	// @audit-issue

157:    function finishRedeem(bytes32 withdrawalKey)	// @audit-issue

193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
194:        external
195:        onlyCore
196:        returns (uint256 transferAmount)	// @audit-issue

258:    function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)
259:        public
260:        view
261:        returns (WithdrawLib.QueuedWithdrawal memory)	// @audit-issue

285:    function extSloads(bytes32[] calldata slots)
286:        public
287:        view
288:        override(ExtSloads, IVault)
289:        returns (bytes32[] memory res)	// @audit-issue

331:    function withdraw(uint256 assets, address to, address owner)
332:        public
333:        override
334:        whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:        nonReentrant
336:        returns (uint256 shares)	// @audit-issue

348:    function redeem(uint256 shares, address to, address owner)
349:        public
350:        override
351:        whenFunctionNotPaused(Constants.PAUSE_VAULT_REDEEM)
352:        nonReentrant
353:        returns (uint256 assets)	// @audit-issue
```
[83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L83), [98](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L94-L98), [115](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L110-L115), [129](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L125-L129), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L157-L157), [196](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L193-L196), [261](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L258-L261), [289](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L285-L289), [336](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L336), [353](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L353), 


```solidity
Path: ./src/entities/Operator.sol

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

96:        if (
97:            calculateRoot(queuedStakeUpdate) != operatorState.pendingStakeUpdates[queuedStakeUpdate.updateRequest.vault]	// @audit-issue

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)
136:        internal
137:        view
138:        returns (bool)	// @audit-issue

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)
174:        public
175:        view
176:        returns (address[] memory vaults)	// @audit-issue

209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)
210:        internal
211:        view
212:        returns (address[] memory dssAddresses)	// @audit-issue

224:    function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)
225:        external
226:        view
227:        returns (uint256 count)	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L96-L97), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [138](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L138), [176](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L176), [212](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L209-L212), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L224-L227), 


```solidity
Path: ./src/entities/CoreLib.sol

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue
```
[67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), 


```solidity
Path: ./src/entities/SlasherLib.sol

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)
80:        internal
81:        view
82:        returns (uint256[] memory earmarkedStakes)	// @audit-issue
```
[59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [82](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L82), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue

66:        if (
67:            !Merkle.verifyInclusionSha256(
68:                beaconStateRootProof.proof, beaconBlockRoot, beaconStateRootProof.beaconStateRoot, BEACON_STATE_ROOT_IDX
69:            )	// @audit-issue

104:        if (
105:            !Merkle.verifyInclusionSha256({
106:                proof: proof.proof,
107:                root: beaconBlockRoot,
108:                leaf: proof.containerRoot,
109:                index: index
110:            })	// @audit-issue

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)
115:        internal
116:        view
117:        returns (uint256 validatorBalanceWei)	// @audit-issue

123:        if (
124:            !Merkle.verifyInclusionSha256({
125:                proof: proof.proof,
126:                root: balanceRoot,
127:                leaf: proof.balanceRoot,
128:                index: balanceIndex
129:            })	// @audit-issue
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [69](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L66-L69), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L104-L110), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L117), [129](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L123-L129), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)
30:        internal
31:        pure
32:        returns (bool)	// @audit-issue

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)
49:        internal
50:        pure
51:        returns (bytes32)	// @audit-issue

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)
86:        internal
87:        view
88:        returns (bool)	// @audit-issue

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)
104:        internal
105:        view
106:        returns (bytes32)	// @audit-issue
```
[32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L32), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L51), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L88), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L106), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)
25:        internal
26:        view
27:        returns (WithdrawLib.QueuedWithdrawal memory qdWithdrawal)	// @audit-issue
```
[27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L27), 


```solidity
Path: ./src/entities/HookLib.sol

16:    function performLowLevelCallAndLimitReturnData(address target, bytes memory data, uint256 gasLimit)
17:        internal
18:        returns (bool success, bytes32 returnVal)	// @audit-issue
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L16-L18), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)
94:        internal
95:        returns (address)	// @audit-issue

162:        if (
163:            BeaconProofs.getWithdrawalCredentials(validatorFieldsProof.validatorFields)
164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue
```
[95](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L95), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L162-L164), 


#### Recommendation

Adhere to the Solidity style guide regarding control structures by avoiding the definition of multiple functions with identical names in a contract. Unique and descriptive function names improve code clarity and prevent potential confusion or errors. Consult [Solidity style guide - Control Structures](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#control-structures) for best practices.

### Consider making contracts `Upgradeable`
This allows for bugs to be fixed in production, at the expense of significantly increasing centralization.

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


#### Recommendation

Assess the need for upgradeability in your Solidity contracts based on the project's requirements and lifecycle. If chosen, implement a well-known proxy pattern ensuring rigorous security and governance mechanisms are in place. Be aware of the increased centralization and plan accordingly to mitigate potential risks, such as through decentralized governance models or multi-sig control for upgrade decisions.

### Consider using descriptive `constants` when passing zero as a function argument
Passing zero as a function argument can sometimes result in a security issue (e.g. passing zero as the slippage parameter). Consider using a `constant` variable with a descriptive name, so it's clear that the argument is intentionally being used, and for the right reasons.

```solidity
Path: ./src/NativeVault.sol

463:        NativeVaultLib.Snapshot memory snapshot = NativeVaultLib.Snapshot({
464:            parentBeaconBlockRoot: _getParentBlockRoot(uint64(block.timestamp)),
465:            nodeBalanceWei: nodeBalanceWei,
466:            balanceDeltaWei: 0,	// @audit-issue
467:            remainingProofs: node.activeValidatorCount
468:        });
```
[466](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L463-L468), 


```solidity
Path: ./src/utils/CommonUtils.sol

9:        sort(arr, 0, arr.length - 1);	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L9-L9), 


#### Recommendation

Replace direct usage of zero as a function argument with a well-named `constant`. For example, use something like `uint256 constant NO_SLIPPAGE = 0;` when zero is intended to signify 'no slippage'. This approach enhances code readability, reduces ambiguity, and helps ensure that the function is used correctly and for its intended purpose.

### Don't define functions with the same name in a contract
In Solidity, while function overriding allows for functions with the same name to coexist, it is advisable to avoid this practice to enhance code readability and maintainability. Having multiple functions with the same name, even with different parameters or in inherited contracts, can cause confusion and increase the likelihood of errors during development, testing, and debugging. Using distinct and descriptive function names not only clarifies the purpose and behavior of each function, but also helps prevent unintended function calls or incorrect overriding. By adopting a clear and consistent naming convention, developers can create more comprehensible and maintainable smart contracts.

```solidity
Path: ./src/Core.sol

318:    function implementation(address vault) public view returns (address) {	// @audit-issue: Different function with name name found on line: 308
```
[318](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L318-L318), 


```solidity
Path: ./src/Vault.sol

94:    function deposit(uint256 assets, address to, uint256 minSharesOut)	// @audit-issue: Different function with name name found on line: 78
```
[94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L94-L94), 


```solidity
Path: ./src/entities/Pauser.sol

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue: Different function with name name found on line: 54
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), 


#### Recommendation

Avoid defining multiple functions with the same name within a Solidity contract, including inherited contracts. Use distinct and descriptive names for each function to enhance readability, prevent confusion, and reduce the risk of errors in development and usage.

### Non-`external`/`public` function names should begin with an underscore
According to the Solidity Style Guide, Non-external/public function names should begin with an [underscore](https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue

43:    function addVault(State storage operatorState, IKarakBaseVault vault) internal {	// @audit-issue

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue

103:    function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {	// @audit-issue

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)	// @audit-issue

143:    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {	// @audit-issue

209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)	// @audit-issue

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L43-L43), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L103-L103), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L135), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L143-L143), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L209-L209), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue
41:        Storage storage self,
42:        address _vaultImpl,
43:        address _vetoCommittee,
44:        uint32 _hookCallGasLimit,
45:        uint32 _supportsInterfaceGasLimit,
46:        uint32 _hookGasBuffer
47:    ) internal {

56:    function updateGasValues(	// @audit-issue
57:        Storage storage self,
58:        uint32 _hookCallGasLimit,
59:        uint32 _supportsInterfaceGasLimit,
60:        uint32 _hookGasBuffer
61:    ) internal {

89:    function createVault(	// @audit-issue
90:        Storage storage self,
91:        address operator,
92:        address depositToken,
93:        string memory name,
94:        string memory symbol,
95:        bytes memory extraData,
96:        address implementation
97:    ) internal returns (IKarakBaseVault) {

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue

153:    function allowlistVaultImpl(Storage storage self, address implementation) internal {	// @audit-issue

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L47), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L56-L61), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L97), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L153-L153), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue

42:    function validateVaultsAndSlashPercentages(	// @audit-issue
43:        CoreLib.Storage storage self,
44:        SlashRequest memory slashingRequest,
45:        IDSS dss
46:    ) internal view {

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L46), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue

73:    function validateValidatorProof(	// @audit-issue
74:        uint40 validatorIndex,
75:        bytes32[] calldata validatorFields,
76:        bytes calldata validatorProof,
77:        bytes32 beaconStateRoot
78:    ) internal view {

97:    function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {	// @audit-issue

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L73-L78), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L97-L97), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


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
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/HookLib.sol

16:    function performLowLevelCallAndLimitReturnData(address target, bytes memory data, uint256 gasLimit)	// @audit-issue

48:    function callHook(	// @audit-issue
49:        address target,
50:        bytes memory data,
51:        bool ignoreFailure,
52:        uint32 hookCallGasLimit,
53:        uint32 hookGasBuffer
54:    ) internal returns (bool) {

78:    function callHookIfInterfaceImplemented(	// @audit-issue
79:        IERC165 dss,
80:        bytes memory data,
81:        bytes4 interfaceId,
82:        bool ignoreFailure,
83:        uint32 hookCallGasLimit,
84:        uint32 supportsInterfaceGasLimit,
85:        uint32 hookGasBuffer
86:    ) internal returns (bool) {
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L16-L16), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L54), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L78-L86), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue

110:    function validateSnapshotProof(	// @audit-issue
111:        Storage storage self,
112:        address nodeOwner,
113:        ValidatorDetails memory validatorDetails,
114:        bytes32 balanceRoot,
115:        BeaconProofs.BalanceProof calldata proof
116:    ) internal returns (int256 balanceDeltaWei) {

146:    function validateWithdrawalCredentials(	// @audit-issue
147:        Storage storage self,
148:        address nodeOwner,
149:        uint64 updateTimestamp,
150:        bytes32 beaconStateRoot,
151:        BeaconProofs.ValidatorFieldsProof calldata validatorFieldsProof
152:    ) internal returns (uint256) {
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L116), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L152), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), 


#### Recommendation

To adhere to the Solidity Style Guide, consider prefixing the names of non-`external`/`public` functions with an underscore (_). This naming convention enhances code readability and helps distinguish the visibility of functions.

### Non-`external`/`public` variable names should begin with an underscore
According to the Solidity Style Guide, non-external/public variable names should begin with an underscore


```solidity
Path: ./src/NativeNode.sol

18:    address nodeOwner;	// @audit-issue
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L18-L18), 


#### Recommendation

To adhere to the Solidity Style Guide, consider prefixing the names of non-`external`/`public` variables with an underscore (_). This naming convention enhances code readability and helps distinguish the visibility of  variables.

### Names of `private`/`internal` state variables should be prefixed with an underscore
It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

```solidity
Path: ./src/SlashingHandler.sol

20:    bytes32 internal constant CONFIG_SLOT = 0x661dfff6e6cdad10b44554a6ab58129a188fa46a74caae866b07c414cb424500;	// @audit-issue name should be: _ONFIG_SLOT
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L20-L20), 


```solidity
Path: ./src/Core.sol

39:    bytes32 internal constant STORAGE_SLOT = 0x13c729cff436dc8ac22d145f2c778f6a709d225083f39538cc5e2674f2f10700;	// @audit-issue name should be: _TORAGE_SLOT
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L39-L39), 


```solidity
Path: ./src/NativeVault.sol

29:    bytes32 internal constant STATE_SLOT = 0x0e977c4f52771ae90b9a885786536a06e14de7815be95b6ed56cdea86f6fc300;	// @audit-issue name should be: _TATE_SLOT

32:    bytes32 internal constant CONFIG_SLOT = 0xb6497276931248fe2cc1dc985a2850cccba81036959c83b89ec93582a1e00900;	// @audit-issue name should be: _ONFIG_SLOT
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L29-L29), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L32-L32), 


```solidity
Path: ./src/Vault.sol

35:    bytes32 internal constant STATE_SLOT = 0x5d654853f9da5c5c659891e7f7fc564033f2724663c32c175f373318f8e1e700;	// @audit-issue name should be: _TATE_SLOT

37:    bytes32 internal constant CONFIG_SLOT = 0x22a8eb0cbcfbbbc874f794ecd9efdfeeecb09fe60d66cf9327db2eac8a1ff000;	// @audit-issue name should be: _ONFIG_SLOT
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L35-L35), [37](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L37-L37), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

9:    uint256 internal constant BEACON_STATE_HEIGHT = 5;	// @audit-issue name should be: _EACON_STATE_HEIGHT

10:    uint256 internal constant BEACON_STATE_ROOT_IDX = 3;	// @audit-issue name should be: _EACON_STATE_ROOT_IDX

11:    uint256 internal constant BEACON_BLOCK_HEADER_HEIGHT = 3;	// @audit-issue name should be: _EACON_BLOCK_HEADER_HEIGHT

14:    uint256 internal constant PUBKEY_IDX = 0;	// @audit-issue name should be: _UBKEY_IDX

15:    uint256 internal constant NUM_FIELDS = 8;	// @audit-issue name should be: _UM_FIELDS

16:    uint256 internal constant BALANCE_IDX = 2;	// @audit-issue name should be: _ALANCE_IDX

17:    uint256 internal constant CONTAINER_IDX = 11;	// @audit-issue name should be: _ONTAINER_IDX

18:    uint256 internal constant EXIT_EPOCH_IDX = 6;	// @audit-issue name should be: _XIT_EPOCH_IDX

19:    uint256 internal constant VALIDATOR_HEIGHT = 40;	// @audit-issue name should be: _ALIDATOR_HEIGHT

20:    uint256 internal constant WITHDRAWAL_CREDENTIALS_IDX = 1;	// @audit-issue name should be: _ITHDRAWAL_CREDENTIALS_IDX

23:    uint256 internal constant BALANCE_CONTAINER_IDX = 12;	// @audit-issue name should be: _ALANCE_CONTAINER_IDX

24:    uint256 internal constant BALANCE_HEIGHT = 38;	// @audit-issue name should be: _ALANCE_HEIGHT
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L9-L9), [10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L10-L10), [11](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L11-L11), [14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L14-L14), [15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L15-L15), [16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L16-L16), [17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L17-L17), [18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L18-L18), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L19-L19), [20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L20-L20), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L23-L23), [24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L24-L24), 


```solidity
Path: ./src/entities/Pauser.sol

16:    bytes32 private constant PAUSER_STORAGE_SLOT = 0x271441cddf42198c20456f920f5dac04f245854c82f280f2e59e7095958d0b00;	// @audit-issue name should be: _AUSER_STORAGE_SLOT
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L16-L16), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### Using zero as a parameter
Taking 0 as a valid argument in Solidity without checks can lead to severe security issues. A historical example is the infamous 0x0 address bug where numerous tokens were lost. This happens because '0' can be interpreted as an uninitialized address, leading to transfers to the '0x0' address, effectively burning tokens. Moreover, 0 as a denominator in division operations would cause a runtime exception. It's also often indicative of a logical error in the caller's code. It's important to always validate input and handle edge cases like 0 appropriately. Use `require()` statements to enforce conditions and provide clear error messages to facilitate debugging and safer code.

```solidity
Path: ./src/utils/CommonUtils.sol

9:        sort(arr, 0, arr.length - 1);	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L9-L9), 


#### Recommendation

Implement stringent checks in your Solidity contracts to validate inputs and avoid the unsafe use of zero. Utilize `require()` statements to ensure that critical parameters, such as addresses and denominators in division operations, are not zero. Provide clear and informative error messages in these `require()` statements to aid in debugging and to clearly communicate the nature of the error. This practice not only enhances the security of your contract but also helps prevent logical errors and facilitates safer interactions with the contract.

### Avoid using `owner` or `_owner` as a parameter name
Using 'owner' or '_owner' as a parameter name in functions, especially in contracts inheriting from or interacting with OpenZeppelin's `Ownable` contract, can lead to confusion and potential bugs. These contracts often have a state variable named `owner`, managed by the `Ownable` pattern for access control. Using the same name for function parameters may obscure the contract's `owner` state variable, complicating code readability and maintenance. Prefer alternative descriptive names for parameters to maintain clarity and prevent conflicts with established ownership patterns.

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
Path: ./src/NativeVault.sol

47:        address _owner,	// @audit-issue

529:    modifier nodeExists(address owner) {	// @audit-issue

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue
```
[47](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L47-L47), [529](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L529-L529), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), 


```solidity
Path: ./src/Vault.sol

52:        address _owner,	// @audit-issue

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue
```
[52](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L52-L52), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), 


#### Recommendation

Refactor your Solidity contracts to use descriptive and unambiguous names for function parameters, avoiding the use of `owner` or `_owner` if your contract inherits from or interacts with the `Ownable` contract or follows a similar ownership pattern. Opt for alternative names that clearly indicate the parameter's purpose without conflicting with the `owner` state variable.

### Employ Explicit Casting to Bytes or Bytes32 for Enhanced Code Clarity and Meaning
Smart contracts are complex entities, and clarity in their operations is fundamental to ensure that they function as intended. Casting a single argument instead of utilizing 'abi.encodePacked()' improves the transparency of the operation. It elucidates the intent of the code, reducing ambiguity and making it easier for auditors and developers to understand the code’s purpose. Such practices promote readability and maintainability, thus reducing the likelihood of errors and misunderstandings. Therefore, it's recommended to employ explicit casts for single arguments where possible, to increase the contract's comprehensibility and ensure a smoother review process.

```solidity
Path: ./src/entities/CoreLib.sol

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), 


```solidity
Path: ./src/entities/MerkleProofs.sol

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue

164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L164-L164), 


#### Recommendation

Consider using `bytes.concat()` instead of `abi.encodePacked()` for concatenating `bytes` for clearer semantic meaning, especially in Solidity versions 0.8.4 and later.

### Revert statements within external and public functions can be used to perform DOS attacks
In Solidity, `revert` statements are used to undo changes and throw an exception when certain conditions are not met. However, in public and external functions, improper use of `revert` can be exploited for Denial of Service (DoS) attacks. An attacker can intentionally trigger these `revert' conditions, causing legitimate transactions to consistently fail. For example, if a function relies on specific conditions from user input or contract state, an attacker could manipulate these to continually force `revert`s, blocking the function's execution. Therefore, it's crucial to design contract logic to handle exceptions properly and avoid scenarios where `revert` can be predictably triggered by malicious actors. This includes careful input validation and considering alternative design patterns that are less susceptible to such abuses.

```solidity
Path: ./src/SlashingHandler.sol

53:        if (amount == 0) revert ZeroAmount();	// @audit-issue

54:        if (!_config().supportedAssets[token]) revert UnsupportedAsset();	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L53-L53), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L54-L54), 


```solidity
Path: ./src/Core.sol

104:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

264:        if (!address(dss).isSmartContract()) revert NotSmartContract();	// @audit-issue
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L104-L104), [264](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L264-L264), 


```solidity
Path: ./src/NativeVault.sol

57:        if (_depositToken != Constants.DEAD_BEEF) revert DepositTokenNotAccepted();	// @audit-issue

62:        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue

148:            if (validatorDetails.status != NativeVaultLib.ValidatorStatus.ACTIVE) revert InactiveValidator();	// @audit-issue

150:                revert ValidatorAlreadyProved();	// @audit-issue

182:            revert BeaconTimestampIsCurrent();	// @audit-issue

187:        ) revert BeaconTimestampTooOld();	// @audit-issue

219:            revert SnapshotNotExpired();	// @audit-issue

239:            revert WithdrawMoreThanMax();	// @audit-issue

244:            revert SnapshotExpired();	// @audit-issue

271:        if (startedWithdrawal.start == 0) revert WithdrawalNotFound();	// @audit-issue

273:            revert MinWithdrawDelayNotPassed();	// @audit-issue
```
[57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L57-L57), [62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L62-L62), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L148-L148), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L150-L150), [182](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L182-L182), [187](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L187-L187), [219](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L219-L219), [239](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L239-L239), [244](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L244-L244), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L271-L271), [273](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L273-L273), 


```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue

100:        if (assets == 0) revert ZeroAmount();	// @audit-issue

102:        if (shares < minSharesOut) revert NotEnoughShares();	// @audit-issue

117:        if (shares == 0) revert ZeroShares();	// @audit-issue

131:        if (shares == 0) revert ZeroShares();	// @audit-issue

132:        if (beneficiary == address(0)) revert ZeroAddress();	// @audit-issue

167:        if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L100-L100), [102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L102-L102), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), [131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L131-L131), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L132-L132), [167](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L167-L167), 


```solidity
Path: ./src/entities/Operator.sol

157:        if (isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorAlreadyRegisteredToDSS();	// @audit-issue

158:        if (operatorState.dssMap.length() == Constants.MAX_DSS_PER_OPERATOR) revert MaxDSSCapacityReached();	// @audit-issue

190:        if (vaults.length != 0) revert AllVaultsNotUnstakedFromDSS();	// @audit-issue

191:        if (!isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorNotValidatingForDSS();	// @audit-issue
```
[157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L157-L157), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L158-L158), [190](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L190-L190), [191](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L191-L191), 


```solidity
Path: ./src/entities/CoreLib.sol

70:        if (assets.length != slashingHandlers.length) revert LengthsDontMatch();	// @audit-issue

72:            if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress();	// @audit-issue

82:            revert VaultImplNotAllowlisted();	// @audit-issue

85:            if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();	// @audit-issue
```
[70](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L70-L70), [72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L72-L72), [82](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L82-L82), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L85-L85), 


```solidity
Path: ./src/entities/SlasherLib.sol

128:        if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();	// @audit-issue

130:            revert MinSlashingDelayNotPassed();	// @audit-issue

155:        if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();	// @audit-issue

180:        if (currentSlashablePercentageWad != 0) revert DSSAlreadyRegistered();	// @audit-issue

181:        if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();	// @audit-issue

182:        if (dssMaxSlashablePercentageWad > Constants.MAX_SLASHING_PERCENT_WAD) revert MaxSlashPercentageWadBreached();	// @audit-issue
```
[128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L128-L128), [130](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L130-L130), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L155-L155), [180](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L180-L180), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L181-L181), [182](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L182-L182), 


#### Recommendation

Design your Solidity contract's public and external functions with care to mitigate the risk of DoS attacks via `revert` statements. Implement robust input validation to ensure inputs are within expected bounds and conditions. Consider alternative logic or design patterns that reduce the reliance on `revert` for critical operations, particularly those that can be influenced externally. Evaluate the use of modifiers, try-catch blocks, or state checks that allow for safer handling of conditions and exceptions. Ensure that your contract's critical functionality remains accessible and resilient against potential abuse of `revert` behavior by malicious actors.

### Use `string.concat()` on strings instead of `abi.encodePacked()` for clearer semantic meaning
From Solidity 0.8.12 onwards, developers can utilize `string.concat()` to concatenate strings without additional padding. Opting for `string.concat()` over `abi.encodePacked()` offers clearer semantic interpretation of the code's intent, enhancing readability. This shift minimizes ambiguity, reducing the potential for misinterpretation by reviewers or future developers. Thus, for string concatenation tasks, it's recommended to transition to `string.concat()` for transparent, straightforward code that communicates its purpose distinctly.

```solidity
Path: ./src/entities/CoreLib.sol

99:        bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));	// @audit-issue
```
[99](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L99-L99), 


```solidity
Path: ./src/entities/MerkleProofs.sol

148:            layer[i] = sha256(abi.encodePacked(leaves[2 * i], leaves[2 * i + 1]));	// @audit-issue

156:                layer[i] = sha256(abi.encodePacked(layer[2 * i], layer[2 * i + 1]));	// @audit-issue
```
[148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L148-L148), [156](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L156-L156), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

97:        bytes32 salt = keccak256(abi.encodePacked(config.operator, owner));	// @audit-issue

164:                != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))	// @audit-issue
```
[97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L97-L97), [164](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L164-L164), 


#### Recommendation

Consider using `bytes.concat()` instead of `abi.encodePacked()` for concatenating `bytes` for clearer semantic meaning, especially in Solidity versions 0.8.4 and later.

### Consider adding emergency-stop functionality
In the event of a security breach or any unforeseen emergency, swiftly suspending all protocol operations becomes crucial. Having a mechanism in place to halt all functions collectively, instead of pausing individual contracts separately, substantially enhances the efficiency of mitigating ongoing attacks or vulnerabilities. This not only quickens the response time to potential threats but also reduces operational stress during these critical periods. Therefore, consider integrating a 'circuit breaker' or 'emergency stop' function into the smart contract system architecture. Such a feature would provide the capability to suspend the entire protocol instantly, which could prove invaluable during a time-sensitive crisis management situation.

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
Path: ./src/entities/MerkleProofs.sol

20:library Merkle {	// @audit-issue
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L20-L20), 


```solidity
Path: ./src/entities/VaultLib.sol

8:library VaultLib {	// @audit-issue
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L8-L8), 


```solidity
Path: ./src/entities/HookLib.sol

9:library HookLib {	// @audit-issue
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L9-L9), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

14:library NativeVaultLib {	// @audit-issue
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L14-L14), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Implement an emergency-stop feature in your Solidity contract system to enhance security and crisis response capabilities. This can be achieved through a 'circuit breaker' pattern, where a central switch or set of conditions can instantly suspend critical operations across the contract ecosystem. Ensure that this mechanism is accessible to authorized parties only, such as contract administrators or a decentralized governance system. Design the emergency-stop functionality to be transparent and auditable, with clear conditions and processes for activation and deactivation. Regularly test and audit this feature to ensure its reliability and effectiveness in potential emergency situations.

### Assembly block creates dirty bits
Manipulating data directly at the free memory pointer location without subsequently adjusting the pointer can lead to unwanted data remnants, or "dirty bits", in that memory spot. This can cause challenges for the Solidity optimizer, making it difficult to determine if memory cleaning is required before reuse, potentially resulting in less efficient optimization. To mitigate this issue, it's advised to always update the free memory pointer following any data write operation. Furthermore, using the `assembly ("memory-safe") { ... }` annotation will clearly indicate to the optimizer the sections of your code that are memory-safe, improving code efficiency and reducing the potential for errors.

```solidity
Path: ./src/SlashingHandler.sol

62:        assembly {	// @audit-issue
63:            $.slot := CONFIG_SLOT
64:        }
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L62-L64), 


```solidity
Path: ./src/Core.sol

386:        assembly {	// @audit-issue
387:            $.slot := STORAGE_SLOT
388:        }
```
[386](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L386-L388), 


```solidity
Path: ./src/NativeVault.sol

404:        assembly {	// @audit-issue
405:            $.slot := STATE_SLOT
406:        }

410:        assembly {	// @audit-issue
411:            $.slot := CONFIG_SLOT
412:        }
```
[404](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L404-L406), [410](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L410-L412), 


```solidity
Path: ./src/Vault.sol

298:        assembly {	// @audit-issue
299:            $.slot := STATE_SLOT
300:        }

304:        assembly {	// @audit-issue
305:            $.slot := CONFIG_SLOT
306:        }

310:        assembly {	// @audit-issue
311:            $.slot := STATE_SLOT
312:            $$.slot := CONFIG_SLOT
313:        }
```
[298](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L298-L300), [304](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L304-L306), [310](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L310-L313), 


```solidity
Path: ./src/entities/MerkleProofs.sol

58:                assembly {	// @audit-issue
59:                    mstore(0x00, computedHash)
60:                    mstore(0x20, mload(add(proof, i)))
61:                    computedHash := keccak256(0x00, 0x40)
62:                    index := div(index, 2)
63:                }

66:                assembly {	// @audit-issue
67:                    mstore(0x00, mload(add(proof, i)))
68:                    mstore(0x20, computedHash)
69:                    computedHash := keccak256(0x00, 0x40)
70:                    index := div(index, 2)
71:                }

116:                assembly {	// @audit-issue
117:                    mstore(0x00, mload(computedHash))
118:                    mstore(0x20, mload(add(proof, i)))
119:                    if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) }
120:                    index := div(index, 2)
121:                }

124:                assembly {	// @audit-issue
125:                    mstore(0x00, mload(add(proof, i)))
126:                    mstore(0x20, mload(computedHash))
127:                    if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) }
128:                    index := div(index, 2)
129:                }
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L58-L63), [66](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L66-L71), [116](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L116-L121), [124](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L124-L129), 


```solidity
Path: ./src/entities/HookLib.sol

22:        assembly {	// @audit-issue
23:            // pointer(data) + 0x20 is where actual data is available
24:            // pointer(data) contains the size of the data in bytes
25:            // returnData is where the return value is written to
26:            // we limit size of return value to 32 bytes (same as the size of `returnData` above)
27:            success :=
28:                call(
29:                    gasLimit, // gas available to the inner call
30:                    target, // address of contract being called
31:                    0, // ETH (denominated in WEI) being transferred in this call
32:                    add(data, 0x20), // Pointer to actual data (i.e. 32 bytes offset from `data`)
33:                    mload(data), // Size of actual data (i.e. the value stored in the first 32 bytes at `data`)
34:                    returnData, // Free pointer as a buffer for the inner call to write the return value
35:                    32 // 32 bytes size limit for the return value
36:                )
37:        }
```
[22](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L22-L37), 


```solidity
Path: ./src/entities/Pauser.sol

19:        assembly {	// @audit-issue
20:            $.slot := PAUSER_STORAGE_SLOT
21:        }
```
[19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L19-L21), 


```solidity
Path: ./src/utils/ExtSloads.sol

17:            assembly ("memory-safe") {	// @audit-issue
18:                mstore(add(res, mul(i, 32)), sload(slot))
19:            }
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L17-L19), 


```solidity
Path: ./src/utils/CommonUtils.sol

50:        assembly {	// @audit-issue
51:            size := extcodesize(addr)
52:        }
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L50-L52), 


#### Recommendation

Always update the free memory pointer after writing data in Solidity assembly blocks to ensure memory cleanliness. This practice prevents the creation of 'dirty bits' and aids the Solidity optimizer in performing efficient memory management. Additionally, consider using the `assembly ("memory-safe") { ... }` annotation for sections of your code that are memory-safe. This annotation clearly communicates to the optimizer which parts of your assembly code are handling memory correctly, leading to better optimization and reduced risk of memory-related errors. Regularly review and audit your assembly blocks for proper memory handling to maintain the efficiency and reliability of your Solidity contracts.

### For extended 'using-for' usage, use the latest pragma version
Solidity versions of 0.8.13 or above can make use of enhanced using-for notation within contracts.

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
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


#### Recommendation

Update your Solidity contracts to use the latest pragma version, ideally 0.8.13 or higher, to leverage the enhanced 'using-for' notation. This upgrade will enable you to apply library functions to user-defined types more effectively, enhancing the functionality and readability of your contracts. Make sure to thoroughly test your contracts after upgrading to ensure compatibility and to take full advantage of the latest Solidity features and improvements. Regularly keep your contracts updated with the latest Solidity versions to stay aligned with the evolving capabilities and best practices of the language.

### Consider only defining one library/interface/contract per sol file
Combining multiple libraries, interfaces, or contracts in a single .sol file can lead to clutter, reduced readability, and versioning issues. Resolution: Adopt the best practice of defining only one library, interface, or contract per Solidity file. This modular approach enhances clarity, simplifies unit testing, and streamlines code review. Furthermore, segregating components makes version management easier, as updates to one component won't necessitate changes to a file housing multiple unrelated components. Structured file management can further assist in avoiding naming collisions and ensure smoother integration into larger systems or DApps.

```solidity
Path: ./src/NativeNode.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";
6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
7:
8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
9:
10:import {Pauser} from "./entities/Pauser.sol";
11:import {INativeNode} from "./interfaces/INativeNode.sol";
12:
13:import "./interfaces/Errors.sol";
14:import "./interfaces/Events.sol";
15:import "./interfaces/Constants.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L4-L15), 


```solidity
Path: ./src/SlashStore.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
5:import {Address} from "@openzeppelin/contracts/utils/Address.sol";
6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
7:
8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
9:
10:import "./interfaces/Events.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L4-L10), 


```solidity
Path: ./src/Querier.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
5:
6:import "./entities/CoreStorageSlots.sol";
7:import "./Core.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L4-L7), 


```solidity
Path: ./src/SlashingHandler.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
5:import {SafeTransferLib} from "solady/src/utils/SafeTransferLib.sol";
6:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
7:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
8:
9:import "./interfaces/ISlashingHandler.sol";
10:import "./interfaces/Errors.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L4-L10), 


```solidity
Path: ./src/Core.sol

4:import {OwnableRoles} from "solady/src/auth/OwnableRoles.sol";	// @audit-issue
5:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
6:
7:import {IBeacon} from "@openzeppelin/contracts/proxy/beacon/IBeacon.sol";
8:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
9:
10:import {Pauser} from "./entities/Pauser.sol";
11:import {CoreLib} from "./entities/CoreLib.sol";
12:import {VaultLib} from "./entities/VaultLib.sol";
13:import {Operator} from "./entities/Operator.sol";
14:import {ExtSloads} from "./utils/ExtSloads.sol";
15:import {CommonUtils} from "./utils/CommonUtils.sol";
16:
17:import {ICore, SlasherLib} from "./interfaces/ICore.sol";
18:import {Constants} from "./interfaces/Constants.sol";
19:import {IKarakBaseVault} from "./interfaces/IKarakBaseVault.sol";
20:import {IDSS} from "./interfaces/IDSS.sol";
21:
22:import "./interfaces/Errors.sol";
23:import "./interfaces/Events.sol";
24:import "./interfaces/Constants.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L4-L24), 


```solidity
Path: ./src/NativeVault.sol

4:import {ERC4626, ERC20} from "solady/src/tokens/ERC4626.sol";	// @audit-issue
5:import {OwnableRoles} from "solady/src/auth/OwnableRoles.sol";
6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
7:import {SafeTransferLib} from "solady/src/utils/SafeTransferLib.sol";
8:
9:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
10:import {IBeacon} from "@openzeppelin/contracts/proxy/beacon/IBeacon.sol";
11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
12:
13:import {Pauser} from "./entities/Pauser.sol";
14:import {VaultLib} from "./entities/VaultLib.sol";
15:import {INativeNode} from "./interfaces/INativeNode.sol";
16:import {INativeVault} from "./interfaces/INativeVault.sol";
17:import {BeaconProofs} from "./entities/BeaconProofsLib.sol";
18:import {NativeVaultLib} from "./entities/NativeVaultLib.sol";
19:import {IKarakBaseVault} from "./interfaces/IKarakBaseVault.sol";
20:
21:import "./interfaces/Errors.sol";
22:import "./interfaces/Events.sol";
23:import "./interfaces/Constants.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L4-L23), 


```solidity
Path: ./src/Vault.sol

4:import {Ownable} from "solady/src/auth/Ownable.sol";	// @audit-issue
5:import {ERC4626, ERC20} from "solady/src/tokens/ERC4626.sol";
6:import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
7:import {SafeTransferLib} from "solady/src/utils/SafeTransferLib.sol";
8:
9:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
10:import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
11:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
12:
13:import {Pauser} from "./entities/Pauser.sol";
14:import {VaultLib} from "./entities/VaultLib.sol";
15:import {WithdrawLib} from "./entities/Withdraw.sol";
16:
17:import {ExtSloads} from "./utils/ExtSloads.sol";
18:
19:import {Constants} from "./interfaces/Constants.sol";
20:import {IVault} from "./interfaces/IVault.sol";
21:import {IKarakBaseVault} from "./interfaces/IKarakBaseVault.sol";
22:import {ISlashingHandler} from "./interfaces/ISlashingHandler.sol";
23:import "./interfaces/Errors.sol";
24:import "./interfaces/Events.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L4-L24), 


```solidity
Path: ./src/entities/Operator.sol

4:import {EnumerableSet} from "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";	// @audit-issue
5:
6:import {CoreLib} from "./CoreLib.sol";
7:import {IKarakBaseVault} from "../interfaces/IKarakBaseVault.sol";
8:import {HookLib} from "./HookLib.sol";
9:
10:import "../interfaces/Errors.sol";
11:import "../interfaces/Constants.sol";
12:import "../interfaces/IDSS.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L4-L12), 


```solidity
Path: ./src/entities/CoreLib.sol

4:import {Create2} from "@openzeppelin/contracts/utils/Create2.sol";	// @audit-issue
5:import {LibClone} from "solady/src/utils/LibClone.sol";
6:
7:import {Operator} from "./Operator.sol";
8:import {VaultLib} from "./VaultLib.sol";
9:
10:import {IKarakBaseVault} from "../interfaces/IKarakBaseVault.sol";
11:import {IDSS} from "../interfaces/IDSS.sol";
12:import "../interfaces/Constants.sol";
13:import "../interfaces/Errors.sol";
14:import "../interfaces/Events.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L4-L14), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

4:/* SLOTS */	// @audit-issue
5:uint256 constant CORE_STORAGE_SLOT = 0x13c729cff436dc8ac22d145f2c778f6a709d225083f39538cc5e2674f2f10700;
6:
7:/* CORE_STORAGE_OFFSETS */
8:uint256 constant OPERATOR_STATE_MAPPING_OFFSET = 0;
9:
10:/* OPERATOR_STORAGE_OFFSETS */
11:uint256 constant PENDING_STAKE_UPDATE_MAPPING_OFFSET = 6;
12:
13:library CoreStorageSlots {
14:    /* GETTERS */
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L4-L14), 


```solidity
Path: ./src/entities/SlasherLib.sol

4:import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";	// @audit-issue
5:import "@openzeppelin/contracts/utils/structs/EnumerableMap.sol";
6:
7:import {CoreLib} from "./CoreLib.sol";
8:import {HookLib} from "./HookLib.sol";
9:import {Operator} from "./Operator.sol";
10:import {CommonUtils} from "../utils/CommonUtils.sol";
11:
12:import "../interfaces/Errors.sol";
13:import "../interfaces/Constants.sol";
14:import "../interfaces/IDSS.sol";
15:import "../interfaces/IKarakBaseVault.sol";
16:import "../interfaces/Events.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L4-L16), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

4:import "../interfaces/Errors.sol";	// @audit-issue
5:import {Merkle} from "./MerkleProofs.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L4-L5), 


```solidity
Path: ./src/entities/MerkleProofs.sol

4:pragma solidity ^0.8.0;	// @audit-issue
5:
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L4-L5), 


```solidity
Path: ./src/entities/VaultLib.sol

4:import {Constants} from "../interfaces/Constants.sol";	// @audit-issue
5:import "./Withdraw.sol";
6:import "../interfaces/Errors.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L4-L6), 


```solidity
Path: ./src/entities/HookLib.sol

4:import {Constants} from "../interfaces/Constants.sol";	// @audit-issue
5:import "@openzeppelin/contracts/interfaces/IERC165.sol";
6:import "../interfaces/Errors.sol";
7:import "../interfaces/Events.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L4-L7), 


```solidity
Path: ./src/entities/Pauser.sol

4:	// @audit-issue
5:import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
6:import {ContextUpgradeable} from "@openzeppelin-upgradeable/utils/ContextUpgradeable.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L4-L6), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

4:import {LibClone} from "solady/src/utils/LibClone.sol";	// @audit-issue
5:
6:import "./VaultLib.sol";
7:import "../interfaces/Errors.sol";
8:import "../interfaces/Events.sol";
9:import "../interfaces/Constants.sol";
10:import "../interfaces/INativeNode.sol";
11:
12:import "../entities/BeaconProofsLib.sol";
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L4-L12), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue
5:    struct QueuedWithdrawal {
6:        address staker;
7:        uint96 start;
8:        uint256 shares;
9:        address beneficiary;
10:    }
11:
12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L12), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue
5:    /// @notice Allows reading of arbitrary storage slots. Useful for reading inside embedded structs
6:    /// @dev Originally from Morpho Blue: https://github.com/morpho-org/morpho-blue/blob/d36719dcd2f37068478889782deac96e296719f0/src/Morpho.sol#L544-L557
7:    /// @param slots The storage slots to read
8:    /// @return res The values stored in the given storage slots
9:    function extSloads(bytes32[] calldata slots) public view virtual returns (bytes32[] memory res) {
10:        uint256 nSlots = slots.length;
11:
12:        res = new bytes32[](nSlots);
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue
5:    /// Sorts the array using quick sort inplace
6:    /// @param arr Array to sort
7:    function sortArr(address[] memory arr) private pure {
8:        if (arr.length == 0) return;
9:        sort(arr, 0, arr.length - 1);
10:    }
11:
12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L12), 


#### Recommendation

Adopt a modular file structure in your Solidity projects by defining only one library, interface, or contract per file. This approach significantly enhances the clarity and readability of your code, making it easier to manage, test, and review. It also simplifies version control, as updates to individual components are isolated to their respective files, reducing the risk of unintended side effects. Organize your project directory to reflect this structure, with a clear naming convention that matches file names to their contained contracts, libraries, or interfaces. This organization not only prevents naming collisions but also facilitates smoother integration into larger systems or decentralized applications (DApps).

### Reduce deployment costs by tweaking contracts' metadata
When solidity generates the bytecode for the smart contract to be deployed, it appends metadata about the compilation at the end of the bytecode.
By default, the solidity compiler appends metadata at the end of the “actual” initcode, which gets stored to the blockchain when the constructor finishes executing.
Consider tweaking the metadata to avoid this unnecessary allocation. A full guide can be found [here](https://www.rareskills.io/post/solidity-metadata).
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

See [this](https://www.rareskills.io/post/solidity-metadata) link, at its bottom, for full details

### All verbatim blocks are considered identical by deduplicator and can incorrectly be unified
The Solidity Team reported a bug on October 24, 2023, affecting Yul code using the verbatim builtin, specifically in the Block Deduplicator optimizer step. This bug, present since Solidity version 0.8.5, caused incorrect deduplication of verbatim assembly items surrounded by identical opcodes, considering them identical regardless of their data. The bug was confined to pure Yul compilation with optimization enabled and was unlikely to be exploited as an attack vector. The conditions triggering the bug were very specific, and its occurrence was deemed to have a low likelihood. The bug was rated with an overall low score due to these factors.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Review and assess any Solidity contracts, especially those involving Yul code, that may be impacted by this deduplication bug. If your contracts rely on the Block Deduplicator optimizer and use verbatim blocks in a way that could be affected by this issue, consider updating your Solidity version to one where this bug is fixed, or adjust your contract to avoid this specific scenario. Stay informed about updates from the Solidity Team regarding this and similar issues, and regularly update your Solidity compiler to the latest version to benefit from bug fixes and optimizations. Given the specific and limited nature of this bug, its impact may be minimal, but caution is advised for contracts with complex assembly code or those heavily reliant on optimizer behaviors.

### Consider adding formal verification proofs
Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Consider integrating formal verification into your Solidity contract development process. This can be done by defining formal specifications and properties that your contract should adhere to and using mathematical methods to verify these aspects. Tools and platforms like Certora Prover, Scribble, or OpenZeppelin's test environment can assist in this process. Formal verification should complement traditional testing and auditing methods, offering an additional layer of security assurance. Keep in mind that formal verification requires a thorough understanding of mathematical logic and contract specifications, so it may necessitate additional resources or expertise. Nevertheless, the investment in formal verification can significantly enhance the trustworthiness and robustness of your smart contracts.

### Contracts should have full test coverage
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Consider writing test cases.

### Large or complicated code bases should implement invariant tests
This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts. Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Consider writing invariant test cases.

### Consider adding formal verification proofs
Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)
```solidity
/// @audit Global finding.
```
[1](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L1), 


#### Recommendation

Consider using formal verification.

### NatSpec: Whitespace in Expressions
See the [Whitespace in Expressions](https://docs.soliditylang.org/en/latest/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide.


```solidity
Path: ./src/NativeVault.sol

145:            NativeVaultLib.ValidatorDetails memory validatorDetails =	// @audit-issue: Variable declaration should be like `uint256 x = 3`
```
[145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L145-L145), 


```solidity
Path: ./src/entities/CoreLib.sol

101:        address expectedNewVaultAddr =	// @audit-issue: Variable declaration should be like `uint256 x = 3`
```
[101](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L101-L101), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

154:        NativeVaultLib.ValidatorDetails memory validatorDetails =	// @audit-issue: Variable declaration should be like `uint256 x = 3`
```
[154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L154-L154), 


#### Recommendation

Review and align your Solidity code with the whitespace guidelines provided in the Solidity Style Guide, particularly for expressions. Ensure consistent spacing around operators and commas, and adopt a uniform style for indentation and line breaks in complex expressions. This alignment not only enhances the readability of your code but also promotes a standardized coding style that aligns with community best practices. Utilize linters or automated code formatting tools, where possible, to enforce these whitespace guidelines consistently across your codebase.

### Assembly blocks should have extensive comments
Assembly blocks take a lot more time to audit than normal Solidity code, and often have gotchas and side-effects that the Solidity versions of the same code do not. Consider adding more comments explaining what is being done in every step of the assembly code, and describe why assembly is being used instead of Solidity.


```solidity
Path: ./src/SlashingHandler.sol

62:        assembly {	// @audit-issue
63:            $.slot := CONFIG_SLOT
64:        }
```
[62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L62-L64), 


```solidity
Path: ./src/Core.sol

386:        assembly {	// @audit-issue
387:            $.slot := STORAGE_SLOT
388:        }
```
[386](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L386-L388), 


```solidity
Path: ./src/NativeVault.sol

404:        assembly {	// @audit-issue
405:            $.slot := STATE_SLOT
406:        }

410:        assembly {	// @audit-issue
411:            $.slot := CONFIG_SLOT
412:        }
```
[404](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L404-L406), [410](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L410-L412), 


```solidity
Path: ./src/Vault.sol

298:        assembly {	// @audit-issue
299:            $.slot := STATE_SLOT
300:        }

304:        assembly {	// @audit-issue
305:            $.slot := CONFIG_SLOT
306:        }

310:        assembly {	// @audit-issue
311:            $.slot := STATE_SLOT
312:            $$.slot := CONFIG_SLOT
313:        }
```
[298](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L298-L300), [304](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L304-L306), [310](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L310-L313), 


```solidity
Path: ./src/entities/MerkleProofs.sol

58:                assembly {	// @audit-issue
59:                    mstore(0x00, computedHash)
60:                    mstore(0x20, mload(add(proof, i)))
61:                    computedHash := keccak256(0x00, 0x40)
62:                    index := div(index, 2)
63:                }

66:                assembly {	// @audit-issue
67:                    mstore(0x00, mload(add(proof, i)))
68:                    mstore(0x20, computedHash)
69:                    computedHash := keccak256(0x00, 0x40)
70:                    index := div(index, 2)
71:                }

116:                assembly {	// @audit-issue
117:                    mstore(0x00, mload(computedHash))
118:                    mstore(0x20, mload(add(proof, i)))
119:                    if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) }
120:                    index := div(index, 2)
121:                }

124:                assembly {	// @audit-issue
125:                    mstore(0x00, mload(add(proof, i)))
126:                    mstore(0x20, mload(computedHash))
127:                    if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) }
128:                    index := div(index, 2)
129:                }
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L58-L63), [66](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L66-L71), [116](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L116-L121), [124](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L124-L129), 


```solidity
Path: ./src/entities/Pauser.sol

19:        assembly {	// @audit-issue
20:            $.slot := PAUSER_STORAGE_SLOT
21:        }
```
[19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L19-L21), 


```solidity
Path: ./src/utils/ExtSloads.sol

17:            assembly ("memory-safe") {	// @audit-issue
18:                mstore(add(res, mul(i, 32)), sload(slot))
19:            }
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L17-L19), 


```solidity
Path: ./src/utils/CommonUtils.sol

50:        assembly {	// @audit-issue
51:            size := extcodesize(addr)
52:        }
```
[50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L50-L52), 


#### Recommendation

Thoroughly comment assembly blocks in Solidity to aid in understanding and auditing. Explain each step of the assembly code and justify the use of assembly over Solidity, highlighting any side effects or nuances not present in high-level code.

### Inconsistent spacing in comments
Some lines use `// x` and some use `//x`. The instances below point out the usages that don't follow the majority, within each file

```solidity
Path: ./src/entities/Operator.sol

23:        mapping(address vault => bytes32 updateHash) pendingStakeUpdates; //Supporting only 1 update per vault at a time	// @audit-issue
```
[23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L23-L23), 


```solidity
Path: ./src/entities/MerkleProofs.sol

142:        //there are half as many nodes in the layer above the leaves	// @audit-issue

144:        //create a layer to store the internal nodes	// @audit-issue

146:        //fill the layer with the pairwise hashes of the leaves	// @audit-issue

150:        //the next layer above has half as many nodes	// @audit-issue

152:        //while we haven't computed the root	// @audit-issue

154:            //overwrite the first numNodesInLayer nodes in layer with the pairwise hashes of their children	// @audit-issue

158:            //the next layer above has half as many nodes	// @audit-issue

161:        //the first node in the layer is the root	// @audit-issue
```
[142](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L142-L142), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L144-L144), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L146-L146), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L150-L150), [152](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L152-L152), [154](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L154-L154), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L158-L158), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L161-L161), 


#### Recommendation

Adopt a consistent style for spacing in comments throughout your Solidity code. Choose either `// comment` or `//comment` and apply it uniformly across the entire codebase. This standardization aids in enhancing the overall readability and professionalism of the code. If working in a team, establish and adhere to a shared style guide to maintain consistency in collaborative projects.

### TODO Left in the code
`TODO` comments are mark areas of code that need attention or completion. These comments serve as reminders for unfinished tasks and can be helpful during the development phase. However, if left untouched in production code, these `TODO` statements can introduce security vulnerabilities and impact the overall security of a smart contract.

```solidity
Path: ./src/NativeVault.sol

235:        // TODO: make more recent snapshot compulsory	// @audit-issue
```
[235](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L235-L235), 


#### Recommendation

It's important to remove `TODO` comments from production code to avoid potential security vulnerabilities. These comments should be addressed and resolved during the development phase.

### NatSpec: Body of `if` statement should be placed on a new line
According to the [Solidity style guide](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures), `if` statements whose body contains a single line should look like this: solidity `if (x < 10)     x += 1; `

```solidity
Path: ./src/Querier.sol

35:            if (results[i] != bytes32(0)) count++;	// @audit-issue

40:            if (results[i] != bytes32(0)) vaults[latestIndex++] = stakedVaults[i];	// @audit-issue
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L35-L35), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L40-L40), 


```solidity
Path: ./src/SlashingHandler.sol

53:        if (amount == 0) revert ZeroAmount();	// @audit-issue

54:        if (!_config().supportedAssets[token]) revert UnsupportedAsset();	// @audit-issue
```
[53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L53-L53), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L54-L54), 


```solidity
Path: ./src/Core.sol

104:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

174:        if (newVaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

175:        if (newVaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();	// @audit-issue

185:        if (!self.isVaultImplAllowlisted(newVaultImpl)) revert VaultImplNotAllowlisted();	// @audit-issue

188:        if (self.vaultToImplMap[vault] == address(0)) revert VaultNotAChildVault();	// @audit-issue

212:        if (vaultImpl == address(0)) revert ZeroAddress();	// @audit-issue

213:        if (vaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();	// @audit-issue

264:        if (!address(dss).isSmartContract()) revert NotSmartContract();	// @audit-issue
```
[104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L104-L104), [174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L174-L174), [175](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L175-L175), [185](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L185-L185), [188](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L188-L188), [212](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L212-L212), [213](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L213-L213), [264](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L264-L264), 


```solidity
Path: ./src/NativeVault.sol

57:        if (_depositToken != Constants.DEAD_BEEF) revert DepositTokenNotAccepted();	// @audit-issue

62:        if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

88:        if (newNodeImplementation == address(0)) revert ZeroAddress();	// @audit-issue

140:        if (node.currentSnapshotTimestamp == 0) revert NoActiveSnapshot();	// @audit-issue

148:            if (validatorDetails.status != NativeVaultLib.ValidatorStatus.ACTIVE) revert InactiveValidator();	// @audit-issue

184:        if (	// @audit-issue

271:        if (startedWithdrawal.start == 0) revert WithdrawalNotFound();	// @audit-issue

308:        if (slashingHandler != self.slashStore) revert NotSlashStore();	// @audit-issue

451:        if (node.currentSnapshotTimestamp != 0) revert PendingIncompleteSnapshot();	// @audit-issue

461:        if (revertIfNoBalanceChange && nodeBalanceWei == 0) revert NoBalanceUpdateToSnapshot();	// @audit-issue

499:        if (assets + self.totalAssets > maxDeposit(_of)) revert DepositMoreThanMax();	// @audit-issue

530:        if (_state().ownerToNode[owner].nodeAddress == address(0)) revert NotNodeOwner();	// @audit-issue
```
[57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L57-L57), [62](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L62-L62), [88](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L88-L88), [140](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L140-L140), [148](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L148-L148), [184](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L184-L184), [271](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L271-L271), [308](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L308-L308), [451](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L451-L451), [461](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L461-L461), [499](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L499-L499), [530](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L530-L530), 


```solidity
Path: ./src/Vault.sol

85:        if (assets == 0) revert ZeroAmount();	// @audit-issue

100:        if (assets == 0) revert ZeroAmount();	// @audit-issue

102:        if (shares < minSharesOut) revert NotEnoughShares();	// @audit-issue

117:        if (shares == 0) revert ZeroShares();	// @audit-issue

131:        if (shares == 0) revert ZeroShares();	// @audit-issue

132:        if (beneficiary == address(0)) revert ZeroAddress();	// @audit-issue

167:        if (shares > maxRedeem(address(this))) revert RedeemMoreThanMax();	// @audit-issue
```
[85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L85-L85), [100](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L100-L100), [102](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L102-L102), [117](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L117-L117), [131](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L131-L131), [132](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L132-L132), [167](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L167-L167), 


```solidity
Path: ./src/entities/Operator.sol

44:        if (vault == IKarakBaseVault(address(0))) revert ZeroAddress();	// @audit-issue

45:        if (operatorState.vaults.length() == Constants.MAX_VAULTS_PER_OPERATOR) revert MaxVaultCapacityReached();	// @audit-issue

57:        if (operatorState.pendingStakeUpdates[stakeUpdate.vault] != bytes32(0)) revert PendingStakeUpdateRequest();	// @audit-issue

58:        if (!operatorState.vaults.contains(stakeUpdate.vault)) revert VaultNotAChildVault();	// @audit-issue

144:        if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();	// @audit-issue

157:        if (isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorAlreadyRegisteredToDSS();	// @audit-issue

158:        if (operatorState.dssMap.length() == Constants.MAX_DSS_PER_OPERATOR) revert MaxDSSCapacityReached();	// @audit-issue

190:        if (vaults.length != 0) revert AllVaultsNotUnstakedFromDSS();	// @audit-issue

191:        if (!isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorNotValidatingForDSS();	// @audit-issue

233:            if (isVaultStakeToDSS(operatorState, IDSS(dssAddresses[i]), address(vault))) count++;	// @audit-issue
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L44-L44), [45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L45-L45), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L57-L57), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L58-L58), [144](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L144-L144), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L157-L157), [158](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L158-L158), [190](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L190-L190), [191](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L191-L191), [233](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L233-L233), 


```solidity
Path: ./src/entities/CoreLib.sol

70:        if (assets.length != slashingHandlers.length) revert LengthsDontMatch();	// @audit-issue

72:            if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress();	// @audit-issue

85:            if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();	// @audit-issue
```
[70](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L70-L70), [72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L72-L72), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L85-L85), 


```solidity
Path: ./src/entities/SlasherLib.sol

47:        if (slashingRequest.vaults.hasDuplicates()) revert DuplicateSlashingVaults();	// @audit-issue

54:            if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad();	// @audit-issue

55:            if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached();	// @audit-issue

68:        if (slashingRequest.slashPercentagesWad.length != slashingRequest.vaults.length) revert LengthsDontMatch();	// @audit-issue

74:        if (slashingRequest.vaults.length == 0) revert EmptyArray();	// @audit-issue

128:        if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();	// @audit-issue

155:        if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();	// @audit-issue

180:        if (currentSlashablePercentageWad != 0) revert DSSAlreadyRegistered();	// @audit-issue

181:        if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();	// @audit-issue

182:        if (dssMaxSlashablePercentageWad > Constants.MAX_SLASHING_PERCENT_WAD) revert MaxSlashPercentageWadBreached();	// @audit-issue
```
[47](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L47-L47), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L54-L54), [55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L55-L55), [68](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L68-L68), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L74-L74), [128](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L128-L128), [155](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L155-L155), [180](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L180-L180), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L181-L181), [182](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L182-L182), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

65:        if (beaconStateRootProof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT)) revert InvalidBeaconStateProof();	// @audit-issue

66:        if (	// @audit-issue

79:        if (validatorFields.length != NUM_FIELDS) revert InvalidValidatorFieldsLength();	// @audit-issue

104:        if (	// @audit-issue

119:        if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();	// @audit-issue

123:        if (	// @audit-issue
```
[65](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L65-L65), [66](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L66-L66), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L79-L79), [104](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L104-L104), [119](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L119-L119), [123](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L123-L123), 


```solidity
Path: ./src/entities/HookLib.sol

55:        if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas();	// @audit-issue

59:        if (!ignoreFailure && !success) revert DSSHookCallReverted(returnData);	// @audit-issue

61:        if (success) emit HookCallSucceeded(returnData);	// @audit-issue
```
[55](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L55-L55), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L59-L59), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L61-L61), 


```solidity
Path: ./src/entities/Pauser.sol

45:        if (paused()) revert EnforcedPause();	// @audit-issue

50:        if (paused(index)) revert EnforcedPauseFunction(index);	// @audit-issue

69:        if ((self._paused & map) != self._paused) revert AttemptedUnpauseWhilePausing();	// @audit-issue

76:        if (self._paused & map != map) revert AttemptedPauseWhileUnpausing();	// @audit-issue
```
[45](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L45-L45), [50](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L50-L50), [69](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L69-L69), [76](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L76-L76), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

157:        if (validatorDetails.status != NativeVaultLib.ValidatorStatus.INACTIVE) revert ValidatorAlreadyActive();	// @audit-issue
```
[157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L157-L157), 


```solidity
Path: ./src/utils/CommonUtils.sol

8:        if (arr.length == 0) return;	// @audit-issue

13:        if (left >= right) return;	// @audit-issue

18:                if (i != lastUnsortedInd) swap(arr, i, lastUnsortedInd);	// @audit-issue

41:        if (arr.length == 0) return false;	// @audit-issue

43:            if (arr[i] == arr[i + 1]) return true;	// @audit-issue
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L8-L8), [13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L13-L13), [18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L18-L18), [41](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L41-L41), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L43-L43), 


#### Recommendation

Adhere to the Solidity style guide by formatting single-line `if` statements with the body on the same line as the condition. For example, use `if (x < 10) x += 1;` for concise and clear code. This style of formatting enhances readability and maintains consistency with Solidity's recommended best practices. It's particularly effective for simple and short conditional operations within the contract's code.

### NatSpec: Contract declarations should have `@author` tag
In the world of decentralized code, giving credit is key. NatSpec's `@author` tag acknowledges the minds behind the code. It appears this Solidity contract omits the `@author` directive in its NatSpec annotations. Properly attributing code to its contributors not only recognizes effort but also aids in establishing trust and credibility. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue missing `@author` tag
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue missing `@author` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


```solidity
Path: ./src/Querier.sol

9:contract Querier {	// @audit-issue missing `@author` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L9-L9), 


```solidity
Path: ./src/SlashingHandler.sol

16:contract SlashingHandler is Initializable, Ownable, ISlashingHandler {	// @audit-issue missing `@author` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L16-L16), 


```solidity
Path: ./src/Core.sol

26:contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {	// @audit-issue missing `@author` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L26-L26), 


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue missing `@author` tag
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue missing `@author` tag
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


```solidity
Path: ./src/entities/Operator.sol

14:library Operator {	// @audit-issue missing `@author` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L14-L14), 


```solidity
Path: ./src/entities/CoreLib.sol

16:library CoreLib {	// @audit-issue missing `@author` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L16-L16), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

13:library CoreStorageSlots {	// @audit-issue missing `@author` tag
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L13-L13), 


```solidity
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue missing `@author` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

7:library BeaconProofs {	// @audit-issue missing `@author` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L7-L7), 


```solidity
Path: ./src/entities/MerkleProofs.sol

20:library Merkle {	// @audit-issue missing `@author` tag
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L20-L20), 


```solidity
Path: ./src/entities/VaultLib.sol

8:library VaultLib {	// @audit-issue missing `@author` tag
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L8-L8), 


```solidity
Path: ./src/entities/HookLib.sol

9:library HookLib {	// @audit-issue missing `@author` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L9-L9), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue missing `@author` tag
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

14:library NativeVaultLib {	// @audit-issue missing `@author` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L14-L14), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue missing `@author` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L4), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue missing `@author` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue missing `@author` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@dev` tag
NatSpec comments are a critical part of Solidity's documentation system, designed to help developers and others understand the behavior and purpose of a contract. The `@dev` tag, in particular, provides context and insight into the contract's development considerations. A missing `@dev` comment can lead to misunderstandings about the contract, making it harder for others to contribute to or use the contract effectively. Therefore, it's highly recommended to include `@dev` comments in the documentation to enhance code readability and maintainability. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue missing `@dev` tag
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue missing `@dev` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


```solidity
Path: ./src/Querier.sol

9:contract Querier {	// @audit-issue missing `@dev` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L9-L9), 


```solidity
Path: ./src/Core.sol

26:contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {	// @audit-issue missing `@dev` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L26-L26), 


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue missing `@dev` tag
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/entities/Operator.sol

14:library Operator {	// @audit-issue missing `@dev` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L14-L14), 


```solidity
Path: ./src/entities/CoreLib.sol

16:library CoreLib {	// @audit-issue missing `@dev` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L16-L16), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

13:library CoreStorageSlots {	// @audit-issue missing `@dev` tag
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L13-L13), 


```solidity
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue missing `@dev` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

7:library BeaconProofs {	// @audit-issue missing `@dev` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L7-L7), 


```solidity
Path: ./src/entities/VaultLib.sol

8:library VaultLib {	// @audit-issue missing `@dev` tag
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L8-L8), 


```solidity
Path: ./src/entities/HookLib.sol

9:library HookLib {	// @audit-issue missing `@dev` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L9-L9), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

14:library NativeVaultLib {	// @audit-issue missing `@dev` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L14-L14), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue missing `@dev` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L4), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue missing `@dev` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue missing `@dev` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@notice` tag
The `@notice` is used to explain to users what the contract does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue missing `@notice` tag
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue missing `@notice` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


```solidity
Path: ./src/Querier.sol

9:contract Querier {	// @audit-issue missing `@notice` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L9-L9), 


```solidity
Path: ./src/Core.sol

26:contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {	// @audit-issue missing `@notice` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L26-L26), 


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue missing `@notice` tag
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/Vault.sol

29:contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault {	// @audit-issue missing `@notice` tag
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L29-L29), 


```solidity
Path: ./src/entities/Operator.sol

14:library Operator {	// @audit-issue missing `@notice` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L14-L14), 


```solidity
Path: ./src/entities/CoreLib.sol

16:library CoreLib {	// @audit-issue missing `@notice` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L16-L16), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

13:library CoreStorageSlots {	// @audit-issue missing `@notice` tag
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L13-L13), 


```solidity
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue missing `@notice` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

7:library BeaconProofs {	// @audit-issue missing `@notice` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L7-L7), 


```solidity
Path: ./src/entities/MerkleProofs.sol

20:library Merkle {	// @audit-issue missing `@notice` tag
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L20-L20), 


```solidity
Path: ./src/entities/VaultLib.sol

8:library VaultLib {	// @audit-issue missing `@notice` tag
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L8-L8), 


```solidity
Path: ./src/entities/HookLib.sol

9:library HookLib {	// @audit-issue missing `@notice` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L9-L9), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue missing `@notice` tag
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

14:library NativeVaultLib {	// @audit-issue missing `@notice` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L14-L14), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue missing `@notice` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L4), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue missing `@notice` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue missing `@notice` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Contract declarations should have `@title` tag
The `@title` is used to explain to users what the contract does. The compiler interprets `///` or `/**` comments [as this tag](https://docs.soliditylang.org/en/latest/natspec-format.html#tags) if one wasn't explicitly provided.

```solidity
Path: ./src/NativeNode.sol

17:contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard {	// @audit-issue missing `@title` tag
```
[17](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L17-L17), 


```solidity
Path: ./src/SlashStore.sol

12:contract SlashStore is Initializable, Ownable, ReentrancyGuard {	// @audit-issue missing `@title` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L12-L12), 


```solidity
Path: ./src/Querier.sol

9:contract Querier {	// @audit-issue missing `@title` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L9-L9), 


```solidity
Path: ./src/Core.sol

26:contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {	// @audit-issue missing `@title` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L26-L26), 


```solidity
Path: ./src/NativeVault.sol

25:contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard {	// @audit-issue missing `@title` tag
```
[25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L25-L25), 


```solidity
Path: ./src/entities/Operator.sol

14:library Operator {	// @audit-issue missing `@title` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L14-L14), 


```solidity
Path: ./src/entities/CoreLib.sol

16:library CoreLib {	// @audit-issue missing `@title` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L16-L16), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

13:library CoreStorageSlots {	// @audit-issue missing `@title` tag
```
[13](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L13-L13), 


```solidity
Path: ./src/entities/SlasherLib.sol

18:library SlasherLib {	// @audit-issue missing `@title` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L18-L18), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

7:library BeaconProofs {	// @audit-issue missing `@title` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L7-L7), 


```solidity
Path: ./src/entities/MerkleProofs.sol

20:library Merkle {	// @audit-issue missing `@title` tag
```
[20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L20-L20), 


```solidity
Path: ./src/entities/VaultLib.sol

8:library VaultLib {	// @audit-issue missing `@title` tag
```
[8](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L8-L8), 


```solidity
Path: ./src/entities/HookLib.sol

9:library HookLib {	// @audit-issue missing `@title` tag
```
[9](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L9-L9), 


```solidity
Path: ./src/entities/Pauser.sol

10:contract Pauser is Initializable, ContextUpgradeable {	// @audit-issue missing `@title` tag
```
[10](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L10-L10), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

14:library NativeVaultLib {	// @audit-issue missing `@title` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L14-L14), 


```solidity
Path: ./src/entities/Withdraw.sol

4:library WithdrawLib {	// @audit-issue missing `@title` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L4-L4), 


```solidity
Path: ./src/utils/ExtSloads.sol

4:abstract contract ExtSloads {	// @audit-issue missing `@title` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/ExtSloads.sol#L4-L4), 


```solidity
Path: ./src/utils/CommonUtils.sol

4:library CommonUtils {	// @audit-issue missing `@title` tag
```
[4](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L4-L4), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Use `@inheritdoc` for overriden functions.
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/Core.sol

308:    function implementation() external view override returns (address) {	// @audit-issue missing `@inheritdoc` tag

373:    function extSloads(bytes32[] calldata slots)	// @audit-issue missing `@inheritdoc` tag
```
[308](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L308-L308), [373](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L373-L373), 


```solidity
Path: ./src/NativeVault.sol

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@inheritdoc` tag

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@inheritdoc` tag

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue missing `@inheritdoc` tag

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue missing `@inheritdoc` tag

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue missing `@inheritdoc` tag

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue missing `@inheritdoc` tag

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue missing `@inheritdoc` tag

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue missing `@inheritdoc` tag

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@inheritdoc` tag

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@inheritdoc` tag

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@inheritdoc` tag

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@inheritdoc` tag

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@inheritdoc` tag

627:    function implementation() external view override returns (address) {	// @audit-issue missing `@inheritdoc` tag
```
[536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)	// @audit-issue missing `@inheritdoc` tag

110:    function mint(uint256 shares, address to)	// @audit-issue missing `@inheritdoc` tag

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@inheritdoc` tag

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@inheritdoc` tag

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@inheritdoc` tag

267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@inheritdoc` tag

272:    function owner() public view override(Ownable, IVault) returns (address) {	// @audit-issue missing `@inheritdoc` tag

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@inheritdoc` tag

285:    function extSloads(bytes32[] calldata slots)	// @audit-issue missing `@inheritdoc` tag

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue missing `@inheritdoc` tag

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue missing `@inheritdoc` tag

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue missing `@inheritdoc` tag
```
[78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L78), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L110-L110), [222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [267](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L267-L267), [272](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L272-L272), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [285](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L285-L285), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function `@return` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including `@return` tag will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/SlashingHandler.sol

61:    function _config() internal pure returns (Config storage $) {	// @audit-issue missing `@return` tag
```
[61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L61-L61), 


```solidity
Path: ./src/Core.sol

130:    function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)	// @audit-issue missing `@return` tag

220:    function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)	// @audit-issue missing `@return` tag

294:    function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {	// @audit-issue missing `@return` tag

385:    function _self() internal pure returns (CoreLib.Storage storage $) {	// @audit-issue missing `@return` tag
```
[130](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L130-L130), [220](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L220-L220), [294](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L294-L294), [385](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L385-L385), 


```solidity
Path: ./src/NativeVault.sol

95:    function createNode()	// @audit-issue missing `@return` tag

228:    function startWithdrawal(address to, uint256 weiAmount)	// @audit-issue missing `@return` tag

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue missing `@return` tag

346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@return` tag

351:    function activeValidatorCount(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@return` tag

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue missing `@return` tag

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue missing `@return` tag

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)	// @audit-issue missing `@return` tag

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue missing `@return` tag

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)	// @audit-issue missing `@return` tag

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@return` tag

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@return` tag

392:    function currentSnapshot(address nodeOwner)	// @audit-issue missing `@return` tag

403:    function _state() internal pure returns (NativeVaultLib.Storage storage $) {	// @audit-issue missing `@return` tag

409:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@return` tag

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue missing `@return` tag

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@return` tag

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@return` tag

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue missing `@return` tag

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue missing `@return` tag

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue missing `@return` tag

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue missing `@return` tag

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue missing `@return` tag

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue missing `@return` tag

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@return` tag

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@return` tag

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@return` tag

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@return` tag

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@return` tag

627:    function implementation() external view override returns (address) {	// @audit-issue missing `@return` tag

631:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue missing `@return` tag
```
[95](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L95-L95), [228](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L228-L228), [299](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L299), [346](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L346-L346), [351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L351-L351), [355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [363](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L363), [371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), [375](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L375), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [392](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L392), [403](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L403-L403), [409](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L409-L409), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), [631](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L631-L631), 


```solidity
Path: ./src/Vault.sol

78:    function deposit(uint256 assets, address to)	// @audit-issue missing `@return` tag

94:    function deposit(uint256 assets, address to, uint256 minSharesOut)	// @audit-issue missing `@return` tag

193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue missing `@return` tag

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@return` tag

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@return` tag

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@return` tag

237:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue missing `@return` tag

243:    function getNextWithdrawNonce(address staker) public view returns (uint256) {	// @audit-issue missing `@return` tag

250:    function isWithdrawalPending(address staker, uint256 _withdrawNonce) public view returns (bool) {	// @audit-issue missing `@return` tag

267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@return` tag

272:    function owner() public view override(Ownable, IVault) returns (address) {	// @audit-issue missing `@return` tag

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@return` tag

297:    function _state() internal pure returns (VaultLib.State storage $) {	// @audit-issue missing `@return` tag

303:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@return` tag

309:    function _storage() internal pure returns (VaultLib.State storage $, VaultLib.Config storage $$) {	// @audit-issue missing `@return` tag

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue missing `@return` tag

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue missing `@return` tag

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue missing `@return` tag
```
[78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L78-L78), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L94-L94), [193](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L193-L193), [222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L237-L237), [243](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L243-L243), [250](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L250-L250), [267](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L267-L267), [272](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L272-L272), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [297](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L297-L297), [303](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L303-L303), [309](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L309-L309), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue missing `@return` tag

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue missing `@return` tag

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)	// @audit-issue missing `@return` tag

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)	// @audit-issue missing `@return` tag

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue missing `@return` tag
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L135), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L173), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), 


```solidity
Path: ./src/entities/CoreLib.sol

89:    function createVault(	// @audit-issue missing `@return` tag

118:    function deployVaults(	// @audit-issue missing `@return` tag

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue missing `@return` tag

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue missing `@return` tag

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue missing `@return` tag
```
[89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L89), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L118), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue missing `@return` tag

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue missing `@return` tag
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue missing `@return` tag

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue missing `@return` tag

94:    function requestSlashing(	// @audit-issue missing `@return` tag

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue missing `@return` tag
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), [170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue missing `@return` tag

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue missing `@return` tag

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue missing `@return` tag

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue missing `@return` tag

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue missing `@return` tag

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@return` tag

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@return` tag

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@return` tag

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@return` tag
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L48), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L85), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L103), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue missing `@return` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/Pauser.sol

18:    function _getPauserStorage() private pure returns (PauserStorage storage $) {	// @audit-issue missing `@return` tag

54:    function paused() public view virtual returns (bool) {	// @audit-issue missing `@return` tag

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue missing `@return` tag

63:    function pausedMap() public view virtual returns (uint256) {	// @audit-issue missing `@return` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L18-L18), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L54-L54), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), [63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L63-L63), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue missing `@return` tag

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag

110:    function validateSnapshotProof(	// @audit-issue missing `@return` tag

146:    function validateWithdrawalCredentials(	// @audit-issue missing `@return` tag
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L110), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L146), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@return` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue missing `@return` tag
```
[48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function declarations should have `@notice` tag
The `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a function does. It appears that this contract's function declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a function's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/NativeNode.sol

21:    constructor() {	// @audit-issue missing `@notice` tag
```
[21](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L21-L21), 


```solidity
Path: ./src/SlashStore.sol

14:    constructor() {	// @audit-issue missing `@notice` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L14-L14), 


```solidity
Path: ./src/Querier.sol

14:    constructor(address coreAddress) {	// @audit-issue missing `@notice` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L14-L14), 


```solidity
Path: ./src/SlashingHandler.sol

26:    constructor() {	// @audit-issue missing `@notice` tag

61:    function _config() internal pure returns (Config storage $) {	// @audit-issue missing `@notice` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L26-L26), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L61-L61), 


```solidity
Path: ./src/Core.sol

42:    constructor() {	// @audit-issue missing `@notice` tag

385:    function _self() internal pure returns (CoreLib.Storage storage $) {	// @audit-issue missing `@notice` tag
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L42-L42), [385](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L385-L385), 


```solidity
Path: ./src/NativeVault.sol

35:    constructor() {	// @audit-issue missing `@notice` tag

346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@notice` tag

351:    function activeValidatorCount(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@notice` tag

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue missing `@notice` tag

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue missing `@notice` tag

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)	// @audit-issue missing `@notice` tag

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue missing `@notice` tag

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)	// @audit-issue missing `@notice` tag

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@notice` tag

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@notice` tag

392:    function currentSnapshot(address nodeOwner)	// @audit-issue missing `@notice` tag

403:    function _state() internal pure returns (NativeVaultLib.Storage storage $) {	// @audit-issue missing `@notice` tag

409:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@notice` tag

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue missing `@notice` tag

425:    function _transferToSlashStore(address nodeOwner) internal {	// @audit-issue missing `@notice` tag

448:    function _startSnapshot(NativeVaultLib.NativeNode storage node, bool revertIfNoBalanceChange, address nodeOwner)	// @audit-issue missing `@notice` tag

476:    function _updateSnapshot(	// @audit-issue missing `@notice` tag

497:    function _increaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@notice` tag

507:    function _decreaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@notice` tag

517:    function _updateBalance(address _of, int256 assets) internal {	// @audit-issue missing `@notice` tag

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@notice` tag

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@notice` tag

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue missing `@notice` tag

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue missing `@notice` tag

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue missing `@notice` tag

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue missing `@notice` tag

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue missing `@notice` tag

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue missing `@notice` tag

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@notice` tag

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@notice` tag

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@notice` tag

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@notice` tag

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@notice` tag

627:    function implementation() external view override returns (address) {	// @audit-issue missing `@notice` tag

631:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue missing `@notice` tag
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L35-L35), [346](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L346-L346), [351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L351-L351), [355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [363](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L363), [371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), [375](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L375), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [392](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L392), [403](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L403-L403), [409](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L409-L409), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [425](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L425-L425), [448](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L448-L448), [476](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L476-L476), [497](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L497-L497), [507](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L507-L507), [517](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L517-L517), [536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), [631](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L631-L631), 


```solidity
Path: ./src/Vault.sol

40:    constructor() {	// @audit-issue missing `@notice` tag

297:    function _state() internal pure returns (VaultLib.State storage $) {	// @audit-issue missing `@notice` tag

303:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@notice` tag

309:    function _storage() internal pure returns (VaultLib.State storage $, VaultLib.Config storage $$) {	// @audit-issue missing `@notice` tag

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue missing `@notice` tag
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L40-L40), [297](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L297-L297), [303](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L303-L303), [309](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L309-L309), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), 


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue missing `@notice` tag

43:    function addVault(State storage operatorState, IKarakBaseVault vault) internal {	// @audit-issue missing `@notice` tag

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue missing `@notice` tag

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue missing `@notice` tag

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@notice` tag

103:    function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {	// @audit-issue missing `@notice` tag

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@notice` tag

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)	// @audit-issue missing `@notice` tag

143:    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {	// @audit-issue missing `@notice` tag

150:    function registerOperatorToDSS(	// @audit-issue missing `@notice` tag

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)	// @audit-issue missing `@notice` tag

181:    function unregisterOperatorFromDSS(	// @audit-issue missing `@notice` tag

209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)	// @audit-issue missing `@notice` tag

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue missing `@notice` tag

224:    function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)	// @audit-issue missing `@notice` tag
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L43-L43), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L103-L103), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L135), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L143-L143), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L150-L150), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L173), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L181-L181), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L209-L209), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), [224](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L224-L224), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue missing `@notice` tag

56:    function updateGasValues(	// @audit-issue missing `@notice` tag

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue missing `@notice` tag

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue missing `@notice` tag

89:    function createVault(	// @audit-issue missing `@notice` tag

118:    function deployVaults(	// @audit-issue missing `@notice` tag

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue missing `@notice` tag

153:    function allowlistVaultImpl(Storage storage self, address implementation) internal {	// @audit-issue missing `@notice` tag

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue missing `@notice` tag

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue missing `@notice` tag
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L40), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L56-L56), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L89), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L118), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L153-L153), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue missing `@notice` tag
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue missing `@notice` tag

42:    function validateVaultsAndSlashPercentages(	// @audit-issue missing `@notice` tag

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue missing `@notice` tag

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue missing `@notice` tag

94:    function requestSlashing(	// @audit-issue missing `@notice` tag

126:    function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@notice` tag

153:    function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@notice` tag

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue missing `@notice` tag

174:    function setDSSMaxSlashablePercentageWad(	// @audit-issue missing `@notice` tag
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L42), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L126-L126), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L153-L153), [170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), [174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L174-L174), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue missing `@notice` tag

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue missing `@notice` tag

73:    function validateValidatorProof(	// @audit-issue missing `@notice` tag

97:    function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {	// @audit-issue missing `@notice` tag

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue missing `@notice` tag

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue missing `@notice` tag

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue missing `@notice` tag

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue missing `@notice` tag

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L73-L73), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L97-L97), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@notice` tag

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@notice` tag

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@notice` tag

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@notice` tag
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L48), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L85), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L103), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue missing `@notice` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/Pauser.sol

18:    function _getPauserStorage() private pure returns (PauserStorage storage $) {	// @audit-issue missing `@notice` tag

36:    function __Pauser_init() internal onlyInitializing {	// @audit-issue missing `@notice` tag

40:    function __Pauser_init_unchained() internal onlyInitializing {	// @audit-issue missing `@notice` tag

54:    function paused() public view virtual returns (bool) {	// @audit-issue missing `@notice` tag

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue missing `@notice` tag

63:    function pausedMap() public view virtual returns (uint256) {	// @audit-issue missing `@notice` tag

67:    function _pause(uint256 map) internal virtual {	// @audit-issue missing `@notice` tag

74:    function _unpause(uint256 map) internal virtual {	// @audit-issue missing `@notice` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L18-L18), [36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L36-L36), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L40-L40), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L54-L54), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), [63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L63-L63), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L67-L67), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L74-L74), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue missing `@notice` tag

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag

110:    function validateSnapshotProof(	// @audit-issue missing `@notice` tag

146:    function validateWithdrawalCredentials(	// @audit-issue missing `@notice` tag
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L110), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L146), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@notice` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue missing `@notice` tag

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@notice` tag

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@notice` tag

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue missing `@notice` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function declarations should have `@dev` tag
Some functions have an incomplete NatSpec: add a `@dev` notation to describe the function to improve the code documentation.

```solidity
Path: ./src/NativeNode.sol

21:    constructor() {	// @audit-issue missing `@dev` tag

28:    function initialize(address _owner, address _nodeOwner) external initializer {	// @audit-issue missing `@dev` tag

39:    function withdraw(address to, uint256 weiAmount)	// @audit-issue missing `@dev` tag

51:    function pause(uint256 map) external onlyOwner {	// @audit-issue missing `@dev` tag

57:    function unpause(uint256 map) external onlyOwner {	// @audit-issue missing `@dev` tag
```
[21](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L21-L21), [28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L28-L28), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L39-L39), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L51-L51), [57](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeNode.sol#L57-L57), 


```solidity
Path: ./src/SlashStore.sol

14:    constructor() {	// @audit-issue missing `@dev` tag

20:    function initialize(address _owner) external initializer {	// @audit-issue missing `@dev` tag

25:    receive() external payable {	// @audit-issue missing `@dev` tag

32:    function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {	// @audit-issue missing `@dev` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L14-L14), [20](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L20-L20), [25](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L25-L25), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashStore.sol#L32-L32), 


```solidity
Path: ./src/Querier.sol

14:    constructor(address coreAddress) {	// @audit-issue missing `@dev` tag

26:    function fetchVaultsQueuedForExit(address operator, IDSS dss) external view returns (address[] memory vaults) {	// @audit-issue missing `@dev` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L14-L14), [26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L26-L26), 


```solidity
Path: ./src/SlashingHandler.sol

26:    constructor() {	// @audit-issue missing `@dev` tag

33:    function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer {	// @audit-issue missing `@dev` tag

43:    function addSlashableToken(IERC20 token) external onlyOwner {	// @audit-issue missing `@dev` tag

52:    function handleSlashing(IERC20 token, uint256 amount) external {	// @audit-issue missing `@dev` tag

61:    function _config() internal pure returns (Config storage $) {	// @audit-issue missing `@dev` tag
```
[26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L26-L26), [33](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L33-L33), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L43-L43), [52](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L52-L52), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/SlashingHandler.sol#L61-L61), 


```solidity
Path: ./src/Core.sol

42:    constructor() {	// @audit-issue missing `@dev` tag

53:    function initialize(	// @audit-issue missing `@dev` tag

72:    function pause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

78:    function unpause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

97:    function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)	// @audit-issue missing `@dev` tag

173:    function changeStandardImplementation(address newVaultImpl) external onlyOwner {	// @audit-issue missing `@dev` tag

183:    function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner {	// @audit-issue missing `@dev` tag

197:    function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

204:    function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

211:    function allowlistVaultImpl(address vaultImpl) external onlyOwner {	// @audit-issue missing `@dev` tag

220:    function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)	// @audit-issue missing `@dev` tag

235:    function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue missing `@dev` tag

248:    function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)	// @audit-issue missing `@dev` tag

294:    function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {	// @audit-issue missing `@dev` tag

302:    function isOperatorRegisteredToDSS(address operator, IDSS dss) public view returns (bool) {	// @audit-issue missing `@dev` tag

308:    function implementation() external view override returns (address) {	// @audit-issue missing `@dev` tag

331:    function getOperatorVaults(address operator) external view returns (address[] memory vaults) {	// @audit-issue missing `@dev` tag

339:    function fetchVaultsStakedInDSS(address operator, IDSS dss) external view returns (address[] memory vaults) {	// @audit-issue missing `@dev` tag

365:    function isDSSRegistered(IDSS dss) public view returns (bool) {	// @audit-issue missing `@dev` tag

385:    function _self() internal pure returns (CoreLib.Storage storage $) {	// @audit-issue missing `@dev` tag
```
[42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L42-L42), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L53-L53), [72](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L72-L72), [78](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L78-L78), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L97-L97), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L173-L173), [183](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L183-L183), [197](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L197-L197), [204](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L204-L204), [211](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L211-L211), [220](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L220-L220), [235](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L235-L235), [248](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L248-L248), [294](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L294-L294), [302](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L302-L302), [308](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L308-L308), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L331-L331), [339](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L339-L339), [365](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L365-L365), [385](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L385-L385), 


```solidity
Path: ./src/NativeVault.sol

35:    constructor() {	// @audit-issue missing `@dev` tag

46:    function initialize(	// @audit-issue missing `@dev` tag

83:    function changeNodeImplementation(address newNodeImplementation)	// @audit-issue missing `@dev` tag

95:    function createNode()	// @audit-issue missing `@dev` tag

112:    function startSnapshot(bool revertIfNoBalanceChange)	// @audit-issue missing `@dev` tag

126:    function validateSnapshotProofs(	// @audit-issue missing `@dev` tag

168:    function validateWithdrawalCredentials(	// @audit-issue missing `@dev` tag

210:    function validateExpiredSnapshot(address nodeOwner)	// @audit-issue missing `@dev` tag

228:    function startWithdrawal(address to, uint256 weiAmount)	// @audit-issue missing `@dev` tag

262:    function finishWithdrawal(bytes32 withdrawalKey)	// @audit-issue missing `@dev` tag

299:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue missing `@dev` tag

322:    function pause(uint256 map) external onlyOwner {	// @audit-issue missing `@dev` tag

328:    function unpause(uint256 map) external onlyOwner {	// @audit-issue missing `@dev` tag

334:    function pauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

340:    function unpauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {	// @audit-issue missing `@dev` tag

346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@dev` tag

351:    function activeValidatorCount(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@dev` tag

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue missing `@dev` tag

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue missing `@dev` tag

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)	// @audit-issue missing `@dev` tag

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue missing `@dev` tag

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)	// @audit-issue missing `@dev` tag

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@dev` tag

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@dev` tag

392:    function currentSnapshot(address nodeOwner)	// @audit-issue missing `@dev` tag

403:    function _state() internal pure returns (NativeVaultLib.Storage storage $) {	// @audit-issue missing `@dev` tag

409:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@dev` tag

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue missing `@dev` tag

425:    function _transferToSlashStore(address nodeOwner) internal {	// @audit-issue missing `@dev` tag

448:    function _startSnapshot(NativeVaultLib.NativeNode storage node, bool revertIfNoBalanceChange, address nodeOwner)	// @audit-issue missing `@dev` tag

476:    function _updateSnapshot(	// @audit-issue missing `@dev` tag

497:    function _increaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@dev` tag

507:    function _decreaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@dev` tag

517:    function _updateBalance(address _of, int256 assets) internal {	// @audit-issue missing `@dev` tag

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@dev` tag

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@dev` tag

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue missing `@dev` tag

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue missing `@dev` tag

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue missing `@dev` tag

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue missing `@dev` tag

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue missing `@dev` tag

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue missing `@dev` tag

607:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@dev` tag

611:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@dev` tag

615:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@dev` tag

619:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@dev` tag

623:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@dev` tag

627:    function implementation() external view override returns (address) {	// @audit-issue missing `@dev` tag

631:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue missing `@dev` tag
```
[35](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L35-L35), [46](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L46-L46), [83](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L83-L83), [95](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L95-L95), [112](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L112-L112), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L126-L126), [168](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L168-L168), [210](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L210-L210), [228](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L228-L228), [262](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L262-L262), [299](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L299-L299), [322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L322-L322), [328](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L328-L328), [334](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L334-L334), [340](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L340-L340), [346](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L346-L346), [351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L351-L351), [355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [363](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L363), [371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), [375](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L375), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [392](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L392), [403](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L403-L403), [409](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L409-L409), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [425](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L425-L425), [448](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L448-L448), [476](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L476-L476), [497](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L497-L497), [507](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L507-L507), [517](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L517-L517), [536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), [607](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L607-L607), [611](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L611-L611), [615](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L615-L615), [619](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L619-L619), [623](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L623-L623), [627](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L627-L627), [631](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L631-L631), 


```solidity
Path: ./src/Vault.sol

40:    constructor() {	// @audit-issue missing `@dev` tag

51:    function initialize(	// @audit-issue missing `@dev` tag

125:    function startRedeem(uint256 shares, address beneficiary)	// @audit-issue missing `@dev` tag

193:    function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)	// @audit-issue missing `@dev` tag

209:    function pause(uint256 map) external onlyCore {	// @audit-issue missing `@dev` tag

215:    function unpause(uint256 map) external onlyCore {	// @audit-issue missing `@dev` tag

222:    function name() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@dev` tag

227:    function symbol() public view override(ERC20, IKarakBaseVault) returns (string memory) {	// @audit-issue missing `@dev` tag

232:    function asset() public view override(ERC4626, IKarakBaseVault) returns (address) {	// @audit-issue missing `@dev` tag

237:    function vaultConfig() public pure returns (VaultLib.Config memory) {	// @audit-issue missing `@dev` tag

243:    function getNextWithdrawNonce(address staker) public view returns (uint256) {	// @audit-issue missing `@dev` tag

250:    function isWithdrawalPending(address staker, uint256 _withdrawNonce) public view returns (bool) {	// @audit-issue missing `@dev` tag

258:    function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)	// @audit-issue missing `@dev` tag

267:    function totalAssets() public view override(ERC4626, IKarakBaseVault) returns (uint256) {	// @audit-issue missing `@dev` tag

272:    function owner() public view override(Ownable, IVault) returns (address) {	// @audit-issue missing `@dev` tag

277:    function decimals() public view override(ERC4626, IKarakBaseVault) returns (uint8) {	// @audit-issue missing `@dev` tag

297:    function _state() internal pure returns (VaultLib.State storage $) {	// @audit-issue missing `@dev` tag

303:    function _config() internal pure returns (VaultLib.Config storage $) {	// @audit-issue missing `@dev` tag

309:    function _storage() internal pure returns (VaultLib.State storage $, VaultLib.Config storage $$) {	// @audit-issue missing `@dev` tag

316:    function _underlyingDecimals() internal view override returns (uint8) {	// @audit-issue missing `@dev` tag

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue missing `@dev` tag

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue missing `@dev` tag
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L40-L40), [51](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L51-L51), [125](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L125-L125), [193](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L193-L193), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L209-L209), [215](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L215-L215), [222](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L222-L222), [227](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L227-L227), [232](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L232-L232), [237](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L237-L237), [243](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L243-L243), [250](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L250-L250), [258](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L258-L258), [267](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L267-L267), [272](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L272-L272), [277](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L277-L277), [297](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L297-L297), [303](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L303-L303), [309](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L309-L309), [316](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L316-L316), [331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue missing `@dev` tag

43:    function addVault(State storage operatorState, IKarakBaseVault vault) internal {	// @audit-issue missing `@dev` tag

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue missing `@dev` tag

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue missing `@dev` tag

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@dev` tag

103:    function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {	// @audit-issue missing `@dev` tag

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@dev` tag

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)	// @audit-issue missing `@dev` tag

143:    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {	// @audit-issue missing `@dev` tag

150:    function registerOperatorToDSS(	// @audit-issue missing `@dev` tag

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)	// @audit-issue missing `@dev` tag

181:    function unregisterOperatorFromDSS(	// @audit-issue missing `@dev` tag

209:    function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)	// @audit-issue missing `@dev` tag

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue missing `@dev` tag

224:    function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)	// @audit-issue missing `@dev` tag
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L43-L43), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L103-L103), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L135), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L143-L143), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L150-L150), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L173), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L181-L181), [209](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L209-L209), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), [224](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L224-L224), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue missing `@dev` tag

56:    function updateGasValues(	// @audit-issue missing `@dev` tag

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue missing `@dev` tag

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue missing `@dev` tag

89:    function createVault(	// @audit-issue missing `@dev` tag

118:    function deployVaults(	// @audit-issue missing `@dev` tag

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue missing `@dev` tag

153:    function allowlistVaultImpl(Storage storage self, address implementation) internal {	// @audit-issue missing `@dev` tag

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue missing `@dev` tag

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue missing `@dev` tag
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L40), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L56-L56), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L89), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L118), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L153-L153), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

15:    function operatorStateMappingSlot() internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue missing `@dev` tag
```
[15](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L15-L15), [19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue missing `@dev` tag

42:    function validateVaultsAndSlashPercentages(	// @audit-issue missing `@dev` tag

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue missing `@dev` tag

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue missing `@dev` tag

94:    function requestSlashing(	// @audit-issue missing `@dev` tag

126:    function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@dev` tag

153:    function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@dev` tag

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue missing `@dev` tag

174:    function setDSSMaxSlashablePercentageWad(	// @audit-issue missing `@dev` tag
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L42), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L126-L126), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L153-L153), [170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), [174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L174-L174), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue missing `@dev` tag

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue missing `@dev` tag

73:    function validateValidatorProof(	// @audit-issue missing `@dev` tag

97:    function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {	// @audit-issue missing `@dev` tag

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue missing `@dev` tag

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue missing `@dev` tag

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue missing `@dev` tag

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue missing `@dev` tag

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L73-L73), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L97-L97), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue missing `@dev` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/HookLib.sol

16:    function performLowLevelCallAndLimitReturnData(address target, bytes memory data, uint256 gasLimit)	// @audit-issue missing `@dev` tag

48:    function callHook(	// @audit-issue missing `@dev` tag
```
[16](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L16-L16), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/HookLib.sol#L48-L48), 


```solidity
Path: ./src/entities/Pauser.sol

18:    function _getPauserStorage() private pure returns (PauserStorage storage $) {	// @audit-issue missing `@dev` tag

36:    function __Pauser_init() internal onlyInitializing {	// @audit-issue missing `@dev` tag

40:    function __Pauser_init_unchained() internal onlyInitializing {	// @audit-issue missing `@dev` tag

54:    function paused() public view virtual returns (bool) {	// @audit-issue missing `@dev` tag

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue missing `@dev` tag

63:    function pausedMap() public view virtual returns (uint256) {	// @audit-issue missing `@dev` tag

67:    function _pause(uint256 map) internal virtual {	// @audit-issue missing `@dev` tag

74:    function _unpause(uint256 map) internal virtual {	// @audit-issue missing `@dev` tag
```
[18](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L18-L18), [36](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L36-L36), [40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L40-L40), [54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L54-L54), [58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), [63](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L63-L63), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L67-L67), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L74-L74), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue missing `@dev` tag

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag

110:    function validateSnapshotProof(	// @audit-issue missing `@dev` tag

146:    function validateWithdrawalCredentials(	// @audit-issue missing `@dev` tag
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L110), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L146), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@dev` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

7:    function sortArr(address[] memory arr) private pure {	// @audit-issue missing `@dev` tag

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@dev` tag

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@dev` tag

39:    function hasDuplicates(address[] memory arr) external pure returns (bool) {	// @audit-issue missing `@dev` tag

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue missing `@dev` tag
```
[7](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L7-L7), [12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), [39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L39-L39), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Function/Constructor `@param` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/Querier.sol

14:    constructor(address coreAddress) {	// @audit-issue missing `@param` tag
```
[14](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Querier.sol#L14-L14), 


```solidity
Path: ./src/Core.sol

146:    function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake)	// @audit-issue missing `@param` tag
```
[146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Core.sol#L146-L146), 


```solidity
Path: ./src/NativeVault.sol

112:    function startSnapshot(bool revertIfNoBalanceChange)	// @audit-issue missing `@param` tag

346:    function withdrawableWei(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@param` tag

351:    function activeValidatorCount(address nodeOwner) public view nodeExists(nodeOwner) returns (uint256) {	// @audit-issue missing `@param` tag

355:    function getNextWithdrawNonce(address nodeOwner) public view returns (uint256) {	// @audit-issue missing `@param` tag

359:    function isWithdrawalPending(address nodeOwner, uint256 withdrawNonce) public view returns (bool) {	// @audit-issue missing `@param` tag

363:    function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)	// @audit-issue missing `@param` tag

371:    function getNodeOwner(address node) external view returns (address) {	// @audit-issue missing `@param` tag

375:    function getValidatorDetails(bytes32 pubKey, address nodeOwner)	// @audit-issue missing `@param` tag

384:    function lastSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@param` tag

388:    function currentSnapshotTimestamp(address nodeOwner) external view nodeExists(nodeOwner) returns (uint64) {	// @audit-issue missing `@param` tag

392:    function currentSnapshot(address nodeOwner)	// @audit-issue missing `@param` tag

415:    function _getParentBlockRoot(uint64 timestamp) internal view returns (bytes32) {	// @audit-issue missing `@param` tag

425:    function _transferToSlashStore(address nodeOwner) internal {	// @audit-issue missing `@param` tag

448:    function _startSnapshot(NativeVaultLib.NativeNode storage node, bool revertIfNoBalanceChange, address nodeOwner)	// @audit-issue missing `@param` tag

476:    function _updateSnapshot(	// @audit-issue missing `@param` tag

497:    function _increaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@param` tag

507:    function _decreaseBalance(address _of, uint256 assets) internal {	// @audit-issue missing `@param` tag

517:    function _updateBalance(address _of, int256 assets) internal {	// @audit-issue missing `@param` tag

536:    function transfer(address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@param` tag

544:    function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) {	// @audit-issue missing `@param` tag

553:    function deposit(uint256 assets, address to) public pure override returns (uint256 shares) {	// @audit-issue missing `@param` tag

562:    function mint(uint256 shares, address to) public pure override returns (uint256 assets) {	// @audit-issue missing `@param` tag

571:    function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {	// @audit-issue missing `@param` tag

581:    function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {	// @audit-issue missing `@param` tag

591:    function previewDeposit(uint256 assets) public pure override returns (uint256 shares) {	// @audit-issue missing `@param` tag

599:    function previewRedeem(uint256 shares) public pure override returns (uint256 assets) {	// @audit-issue missing `@param` tag
```
[112](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L112-L112), [346](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L346-L346), [351](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L351-L351), [355](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L355-L355), [359](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L359-L359), [363](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L363-L363), [371](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L371-L371), [375](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L375-L375), [384](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L384-L384), [388](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L388-L388), [392](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L392-L392), [415](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L415-L415), [425](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L425-L425), [448](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L448-L448), [476](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L476-L476), [497](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L497-L497), [507](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L507-L507), [517](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L517-L517), [536](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L536-L536), [544](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L544-L544), [553](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L553-L553), [562](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L562-L562), [571](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L571-L571), [581](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L581-L581), [591](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L591-L591), [599](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L599-L599), 


```solidity
Path: ./src/Vault.sol

331:    function withdraw(uint256 assets, address to, address owner)	// @audit-issue missing `@param` tag

348:    function redeem(uint256 shares, address to, address owner)	// @audit-issue missing `@param` tag
```
[331](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L331-L331), [348](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L348-L348), 


```solidity
Path: ./src/entities/Operator.sol

39:    function getVaults(State storage operatorState) internal view returns (address[] memory) {	// @audit-issue missing `@param` tag

43:    function addVault(State storage operatorState, IKarakBaseVault vault) internal {	// @audit-issue missing `@param` tag

49:    function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag

53:    function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)	// @audit-issue missing `@param` tag

61:    function requestUpdateVaultStakeInDSS(	// @audit-issue missing `@param` tag

89:    function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@param` tag

103:    function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {	// @audit-issue missing `@param` tag

111:    function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate)	// @audit-issue missing `@param` tag

135:    function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)	// @audit-issue missing `@param` tag

143:    function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {	// @audit-issue missing `@param` tag

150:    function registerOperatorToDSS(	// @audit-issue missing `@param` tag

173:    function getVaultsStakedToDSS(State storage operatorState, IDSS dss)	// @audit-issue missing `@param` tag

181:    function unregisterOperatorFromDSS(	// @audit-issue missing `@param` tag

217:    function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {	// @audit-issue missing `@param` tag
```
[39](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L39-L39), [43](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L43-L43), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L49-L49), [53](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L53-L53), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L61-L61), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L89-L89), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L103-L103), [111](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L111-L111), [135](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L135-L135), [143](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L143-L143), [150](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L150-L150), [173](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L173-L173), [181](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L181-L181), [217](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Operator.sol#L217-L217), 


```solidity
Path: ./src/entities/CoreLib.sol

40:    function init(	// @audit-issue missing `@param` tag

56:    function updateGasValues(	// @audit-issue missing `@param` tag

67:    function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers)	// @audit-issue missing `@param` tag

77:    function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation)	// @audit-issue missing `@param` tag

89:    function createVault(	// @audit-issue missing `@param` tag

118:    function deployVaults(	// @audit-issue missing `@param` tag

149:    function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {	// @audit-issue missing `@param` tag

153:    function allowlistVaultImpl(Storage storage self, address implementation) internal {	// @audit-issue missing `@param` tag

157:    function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {	// @audit-issue missing `@param` tag

161:    function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {	// @audit-issue missing `@param` tag
```
[40](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L40-L40), [56](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L56-L56), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L67-L67), [77](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L77-L77), [89](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L89-L89), [118](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L118-L118), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L149-L149), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L153-L153), [157](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L157-L157), [161](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreLib.sol#L161-L161), 


```solidity
Path: ./src/entities/CoreStorageSlots.sol

19:    function operatorStateSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag

23:    function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag

27:    function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) {	// @audit-issue missing `@param` tag
```
[19](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L19-L19), [23](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L23-L23), [27](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/CoreStorageSlots.sol#L27-L27), 


```solidity
Path: ./src/entities/SlasherLib.sol

38:    function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {	// @audit-issue missing `@param` tag

42:    function validateVaultsAndSlashPercentages(	// @audit-issue missing `@param` tag

59:    function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)	// @audit-issue missing `@param` tag

79:    function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)	// @audit-issue missing `@param` tag

94:    function requestSlashing(	// @audit-issue missing `@param` tag

126:    function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@param` tag

153:    function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external {	// @audit-issue missing `@param` tag

170:    function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) {	// @audit-issue missing `@param` tag

174:    function setDSSMaxSlashablePercentageWad(	// @audit-issue missing `@param` tag
```
[38](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L38-L38), [42](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L42-L42), [59](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L59-L59), [79](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L79-L79), [94](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L94-L94), [126](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L126-L126), [153](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L153-L153), [170](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L170-L170), [174](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/SlasherLib.sol#L174-L174), 


```solidity
Path: ./src/entities/BeaconProofsLib.sol

54:    function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {	// @audit-issue missing `@param` tag

61:    function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)	// @audit-issue missing `@param` tag

73:    function validateValidatorProof(	// @audit-issue missing `@param` tag

97:    function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {	// @audit-issue missing `@param` tag

114:    function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)	// @audit-issue missing `@param` tag

137:    function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {	// @audit-issue missing `@param` tag

141:    function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) {	// @audit-issue missing `@param` tag

145:    function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {	// @audit-issue missing `@param` tag

149:    function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag
```
[54](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L54-L54), [61](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L61-L61), [73](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L73-L73), [97](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L97-L97), [114](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L114-L114), [137](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L137-L137), [141](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L141-L141), [145](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L145-L145), [149](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/BeaconProofsLib.sol#L149-L149), 


```solidity
Path: ./src/entities/MerkleProofs.sol

29:    function verifyInclusionKeccak(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@param` tag

48:    function processInclusionProofKeccak(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@param` tag

85:    function verifyInclusionSha256(bytes memory proof, bytes32 root, bytes32 leaf, uint256 index)	// @audit-issue missing `@param` tag

103:    function processInclusionProofSha256(bytes memory proof, bytes32 leaf, uint256 index)	// @audit-issue missing `@param` tag
```
[29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L48-L48), [85](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L85-L85), [103](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/MerkleProofs.sol#L103-L103), 


```solidity
Path: ./src/entities/VaultLib.sol

24:    function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)	// @audit-issue missing `@param` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/VaultLib.sol#L24-L24), 


```solidity
Path: ./src/entities/Pauser.sol

58:    function paused(uint8 index) public view virtual returns (bool) {	// @audit-issue missing `@param` tag

67:    function _pause(uint256 map) internal virtual {	// @audit-issue missing `@param` tag

74:    function _unpause(uint256 map) internal virtual {	// @audit-issue missing `@param` tag
```
[58](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L58-L58), [67](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L67-L67), [74](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L74-L74), 


```solidity
Path: ./src/entities/NativeVaultLib.sol

93:    function deployNode(Storage storage self, VaultLib.Config storage config, address owner)	// @audit-issue missing `@param` tag

106:    function calculateWithdrawKey(address nodeOwner, uint256 nodeOwnerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag

110:    function validateSnapshotProof(	// @audit-issue missing `@param` tag

146:    function validateWithdrawalCredentials(	// @audit-issue missing `@param` tag
```
[93](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L93-L93), [106](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L106-L106), [110](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L110-L110), [146](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/NativeVaultLib.sol#L146-L146), 


```solidity
Path: ./src/entities/Withdraw.sol

12:    function calculateWithdrawKey(address staker, uint256 stakerNonce) internal pure returns (bytes32) {	// @audit-issue missing `@param` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Withdraw.sol#L12-L12), 


```solidity
Path: ./src/utils/CommonUtils.sol

12:    function sort(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@param` tag

29:    function swap(address[] memory arr, uint256 left, uint256 right) private pure {	// @audit-issue missing `@param` tag

48:    function isSmartContract(address addr) external view returns (bool) {	// @audit-issue missing `@param` tag
```
[12](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L12-L12), [29](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L29-L29), [48](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/utils/CommonUtils.sol#L48-L48), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifier declarations should have `@notice` tag
In Solidity, the `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a modifier does. It appears that this contract's modifier declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a modifier's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/NativeVault.sol

529:    modifier nodeExists(address owner) {	// @audit-issue missing `@notice` tag
```
[529](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L529-L529), 


```solidity
Path: ./src/Vault.sol

322:    modifier onlyCore() {	// @audit-issue missing `@notice` tag
```
[322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L322-L322), 


```solidity
Path: ./src/entities/Pauser.sol

44:    modifier whenNotPaused() {	// @audit-issue missing `@notice` tag

49:    modifier whenFunctionNotPaused(uint8 index) {	// @audit-issue missing `@notice` tag
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L44-L44), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L49-L49), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifier declarations should have `@dev` tag
Some modifiers have an incomplete NatSpec: add a `@dev` notation to describe the modifier to improve the code documentation.

```solidity
Path: ./src/NativeVault.sol

529:    modifier nodeExists(address owner) {	// @audit-issue missing `@dev` tag
```
[529](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L529-L529), 


```solidity
Path: ./src/Vault.sol

322:    modifier onlyCore() {	// @audit-issue missing `@dev` tag
```
[322](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/Vault.sol#L322-L322), 


```solidity
Path: ./src/entities/Pauser.sol

44:    modifier whenNotPaused() {	// @audit-issue missing `@dev` tag

49:    modifier whenFunctionNotPaused(uint8 index) {	// @audit-issue missing `@dev` tag
```
[44](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L44-L44), [49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L49-L49), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Modifiers `@param` tag is missing
Function modifiers should include NatSpec comments with @param tags describing each input parameter. This promotes better code readability and documentation. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/NativeVault.sol

529:    modifier nodeExists(address owner) {	// @audit-issue missing `@param` tag
```
[529](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/NativeVault.sol#L529-L529), 


```solidity
Path: ./src/entities/Pauser.sol

49:    modifier whenFunctionNotPaused(uint8 index) {	// @audit-issue missing `@param` tag
```
[49](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L49-L49), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Event declarations should have `@notice` tag
The `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a event does. It appears that this contract's modifier declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a events's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/entities/Pauser.sol

24:    event Paused(address account, uint256 map);	// @audit-issue missing `@notice` tag

26:    event Unpaused(address account, uint256 map);	// @audit-issue missing `@notice` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L24-L24), [26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L26-L26), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Event declarations should have `@dev` tag
Some events have an incomplete NatSpec: add a `@dev` notation to describe the event to improve the code documentation.

```solidity
Path: ./src/entities/Pauser.sol

24:    event Paused(address account, uint256 map);	// @audit-issue missing `@dev` tag

26:    event Unpaused(address account, uint256 map);	// @audit-issue missing `@dev` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L24-L24), [26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L26-L26), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Event `@param` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of event arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/entities/Pauser.sol

24:    event Paused(address account, uint256 map);	// @audit-issue missing `@param` tag

26:    event Unpaused(address account, uint256 map);	// @audit-issue missing `@param` tag
```
[24](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L24-L24), [26](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L26-L26), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error declarations should have `@notice` tag
The `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a error does. It appears that this contract's modifier declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a error's purpose and behavior.  [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/entities/Pauser.sol

28:    error EnforcedPause();	// @audit-issue missing `@notice` tag

30:    error EnforcedPauseFunction(uint8 functionIndex);	// @audit-issue missing `@notice` tag

32:    error AttemptedUnpauseWhilePausing();	// @audit-issue missing `@notice` tag

34:    error AttemptedPauseWhileUnpausing();	// @audit-issue missing `@notice` tag
```
[28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L28-L28), [30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L30-L30), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L32-L32), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L34-L34), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error declarations should have `@dev` tag
Some errors have an incomplete NatSpec: add a `@dev` notation to describe the error to improve the code documentation.

```solidity
Path: ./src/entities/Pauser.sol

28:    error EnforcedPause();	// @audit-issue missing `@dev` tag

30:    error EnforcedPauseFunction(uint8 functionIndex);	// @audit-issue missing `@dev` tag

32:    error AttemptedUnpauseWhilePausing();	// @audit-issue missing `@dev` tag

34:    error AttemptedPauseWhileUnpausing();	// @audit-issue missing `@dev` tag
```
[28](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L28-L28), [30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L30-L30), [32](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L32-L32), [34](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L34-L34), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).

### NatSpec: Error `@param` tag is missing
Natural Specification (NatSpec) comments are crucial for understanding the role of error arguments in your Solidity code. Including @param tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose. [Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

```solidity
Path: ./src/entities/Pauser.sol

30:    error EnforcedPauseFunction(uint8 functionIndex);	// @audit-issue missing `@param` tag
```
[30](https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/./src/entities/Pauser.sol#L30-L30), 


#### Recommendation

Follow the official [Solidity guidelines](https://docs.soliditylang.org/en/v0.8.17/style-guide.html).
