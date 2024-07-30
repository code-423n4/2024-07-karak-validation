## Summary

### Total Low findings: 38

### Total NonCritical findings: 31

# Summary for Low findings

| Number | Details | Instances |
|----------|----------|----------|
| [Low-1] | Solidity version 0.8.23 won't work on all chains due to MCOPY  | 3 |
| [Low-2] | Two or more functions contain the exact same code  | 4 |
| [Low-3] | Contracts do not use their OZ upgradable counterparts  | 3 |
| [Low-4] | deposit/redeem functions found which implement accounting arithmetic vulnerable to the donation attack | 1 |
| [Low-5] | Unsafe use of transfer()/transferFrom() with IERC20 | 1 |
| [Low-6] | Large transfers may not work with some ERC20 tokens | 2 |
| [Low-7] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 2 |
| [Low-8] | Solidity version 0.8.20 won't work on all chains due to PUSH0 | 3 |
| [Low-9] | Double imports in solidity file | 1 |
| [Low-10] | Missing events in functions that are either setters, privileged or voting related | 17 |
| [Low-11] | Unsafe use of transfer()/transferFrom() with IERC20 | 1 |
| [Low-12] | Avoid floating pragma in non interface/library files | 9 |
| [Low-13] | Solidity version 0.8.20 won't work on all chains due to PUSH0 | 3 |
| [Low-14] | Low level calls in solidity versions preceding 0.8.14 can result in an optimiser bug | 2 |
| [Low-15] | Ownable2Step should be used in place of Ownable | 4 |
| [Low-16] | The call abi.encodeWithSelector is not type safe | 16 |
| [Low-17] | Upgradable contracts should have a __gap variable | 5 |
| [Low-18] | Contracts are vulnerable to fee-on-transfer accounting-related issues | 1 |
| [Low-19] | Upgradable contracts should have an initialization function | 1 |
| [Low-20] | The nonReentrant modifier should be first in a function declaration | 9 |
| [Low-21] | Initializer function can be front run | 6 |
| [Low-22] | Use _disableInitializers() to ensure initialization occurs once | 1 |
| [Low-23] | Minting to the zero address should be avoided | 1 |
| [Low-24] | Missing zero address check in constructor | 1 |
| [Low-25] | Return values of transfer()/transferFrom() not checked | 1 |
| [Low-26] | Use of onlyOwner functions can be lost | 3 |
| [Low-27] | Off-by-one timestamp error | 1 |
| [Low-28] | Events may be emitted out of order due to code not follow the best practice of check-effects-interaction | 1 |
| [Low-29] | Missing zero address check in initializer | 5 |
| [Low-30] | Critical functions should have a timelock | 1 |
| [Low-31] | Consider implementing two-step procedure for updating protocol addresses | 3 |
| [Low-32] | SafeTransferLib does not ensure that the token contract exists | 1 |
| [Low-33] | Avoid mutating function parameters | 2 |
| [Low-34] | Prefer skip over revert model in iteration | 5 |
| [Low-35] | Nonce variables should be uint256 | 2 |
| [Low-36] | Division in comparison | 2 |
| [Low-37] | Library has public/external functions | 6 |
| [Low-38] | Constructor doesn't set initial owner | 4 |


# Summary for NonCritical findings

| Number | Details | Instances |
|----------|----------|----------|
| [NonCritical-1] | ERC777 tokens can introduce reentrancy risks | 2 |
| [NonCritical-2] | Floating pragma should be avoided | 3 |
| [NonCritical-3] | Open TODO in comments | 1 |
| [NonCritical-4] | Not all event definitions are utilizing indexed variables. | 2 |
| [NonCritical-5] | Explicitly define visibility of state variables to prevent misconceptions on what can access the variable | 1 |
| [NonCritical-6] | Functions within contracts are not ordered according to the solidity style guide | 3 |
| [NonCritical-7] | Double type casts create complexity within the code | 3 |
| [NonCritical-8] | Emits without msg.sender parameter | 1 |
| [NonCritical-9] | Unused modifiers present | 1 |
| [NonCritical-10] | Defined named returns not used within function  | 3 |
| [NonCritical-11] | Initialize functions do not emit an event | 5 |
| [NonCritical-12] | Event emit should emit a parameter | 1 |
| [NonCritical-13] | No equate comparison checks between to and from address parameters | 1 |
| [NonCritical-14] | Assembly block creates dirty bits | 2 |
| [NonCritical-15] | Unused import | 1 |
| [NonCritical-16] | Missing events in sensitive functions | 5 |
| [NonCritical-17] | Ensure block.timestamp is only used in long time intervals | 1 |
| [NonCritical-18] | A event should be emitted if a non immutable state variable is set in a constructor | 1 |
| [NonCritical-19] | gasLimit should be uint64 | 1 |
| [NonCritical-20] | Pure function storage pointer bug | 8 |
| [NonCritical-21] | Use 'using' keyword when using specific imports rather than calling the specific import directly | 106 |
| [NonCritical-22] | Inconsistent checks of address params against address(0) | 1 |
| [NonCritical-23] | Avoid declaring variables with the names of defined functions within the project | 5 |
| [NonCritical-24] | Contract and Abstract files should have a fixed compiler version | 2 |
| [NonCritical-25] | Function call in event emit | 1 |
| [NonCritical-26] | For loop iterates on arrays not indexed | 3 |
| [NonCritical-27] | Avoid using 'owner' or '_owner' as a parameter name | 5 |
| [NonCritical-28] | Avoid arithmetic directly within array indices | 1 |
| [NonCritical-29] | Memory-safe annotation missing | 1 |
| [NonCritical-30] | Constant state variables defined more than once | 1 |
| [NonCritical-31] | Unnecessary struct attribute prefix | 6 |


## [Low-1] Solidity version 0.8.23 won't work on all chains due to MCOPY 

### Resolution 
Solidity version 0.8.23 introduces the MCOPY opcode, this may not be implemented on all chains and L2 thus reducing the portability and compatibility of the code. Consider using a earlier solidity version.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L2-L2)']
```solidity
2: pragma solidity ^0.8.25; // <= FOUND
```
['[3](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L3-L3)']
```solidity
3: pragma solidity ^0.8.21; // <= FOUND
```
['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L4-L4)']
```solidity
4: pragma solidity ^0.8.0; // <= FOUND
```


</details>

## [Low-2] Two or more functions contain the exact same code 

### Resolution 
In Solidity programming, duplicate code in multiple functions introduces potential security risks and maintainability issues. It magnifies the impact of any bugs or vulnerabilities, since developers must fix these in every location where the code is replicated. Overlooking any instance of replicated code could leave vulnerabilities intact. Furthermore, code duplication leads to contract bloating, diminishing the readability and manageability of the code. Future logic changes would need to be applied in every location where the code is replicated, increasing the complexity of updates. To resolve this, it is recommended to consolidate duplicate code into a single internal function, and replace the duplicate instances with calls to this new function. This approach streamlines the code, reducing the attack surface and making it easier to maintain and update.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[331](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L331-L339)']
```solidity
331:     function withdraw(uint256 assets, address to, address owner)
332:         public
333:         override
334:         whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:         nonReentrant
336:         returns (uint256 shares)
337:     {
338:         
339:         owner = owner; // <= FOUND
340:         assets = assets;
341:         to = to;
342:         shares = shares;
343: 
344:         revert NotImplemented();
345:     }
```
['[571](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L571-L573)']
```solidity
571:     function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares) {
572:         
573:         owner = owner; // <= FOUND
574:         assets = assets;
575:         to = to;
576:         shares = shares;
577: 
578:         revert NotImplemented();
579:     }
```
['[348](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L348-L356)']
```solidity
348:     function redeem(uint256 shares, address to, address owner)
349:         public
350:         override
351:         whenFunctionNotPaused(Constants.PAUSE_VAULT_REDEEM)
352:         nonReentrant
353:         returns (uint256 assets)
354:     {
355:         
356:         owner = owner; // <= FOUND
357:         to = to;
358:         shares = shares;
359:         assets = assets;
360: 
361:         revert NotImplemented();
362:     }
```
['[581](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L581-L583)']
```solidity
581:     function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets) {
582:         
583:         owner = owner; // <= FOUND
584:         to = to;
585:         shares = shares;
586:         assets = assets;
587: 
588:         revert NotImplemented();
589:     }
```


</details>

## [Low-3] Contracts do not use their OZ upgradable counterparts 

### Resolution 
Using the upgradeable counterpart of the OpenZeppelin (OZ) library in Solidity is beneficial for creating contracts that can be updated in the future. OpenZeppelin's upgradeable contracts library is designed with proxy patterns in mind, which allow the logic of contracts to be upgraded while preserving the contract's state and address. This can be crucial for long-lived contracts where future requirements or improvements may not be fully known at the time of deployment. The upgradeable OZ contracts also include protection against a class of vulnerabilities related to initialization of storage variables in upgradeable contracts. Hence, it's a good idea to use them when developing contracts that may need to be upgraded in the future, as they provide a solid foundation for secure and upgradeable smart contracts.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[29](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L29-L29)']
```solidity
29: contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault  // <= FOUND ' ERC4626,'
```
['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L16-L16)']
```solidity
16: contract SlashingHandler is Initializable, Ownable, ISlashingHandler  // <= FOUND ' Ownable,'
```
['[12](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L12-L12)']
```solidity
12: contract SlashStore is Initializable, Ownable, ReentrancyGuard  // <= FOUND ' Ownable,'
```


</details>

## [Low-4] deposit/redeem functions found which implement accounting arithmetic vulnerable to the donation attack

### Resolution 
Calculations using non-internal accounting, such as balanceOf or totalSupply, can introduce potential donation attack vectors. For instance, consider a scenario where a reward calculation uses totalSupply during a deposit. An attacker could exploit this by donating a large amount of tokens to the vault before the user tries to redeem their withdrawal. This manipulation causes the totalSupply to change significantly, altering the reward calculations and potentially leading to unexpected or unfair outcomes for users.

Let's say a smart contract calculates user rewards based on their share of the total token supply:

```solidity
uint256 reward = (userDeposit * totalRewards) / totalSupply;
```

If an attacker donates a large number of tokens to the vault before users withdraw, totalSupply increases, thereby diluting each user's share of the rewards. This discrepancy between expected and actual rewards can undermine user trust and contract integrity.

The risks associated with this attack include reward manipulation, where attackers can alter totalSupply to reduce the share of honest users, and economic attacks, where significant token donations destabilize the contract's economic assumptions, leading to unfair advantages or financial losses. Additionally, users may find their rewards significantly lower than expected, causing confusion and dissatisfaction.

To prevent such vulnerabilities, it's essential to use internal variables to track deposits, withdrawals, and rewards instead of relying on balanceOf or totalSupply. This approach isolates contract logic from external token movements. Implementing a snapshot mechanism to capture totalSupply at specific points in time ensures consistent reward calculations. Introducing limits on the number of tokens that can be deposited or donated in a single transaction can also prevent significant manipulation. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[425](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L425-L425)']
```solidity
425:     function _transferToSlashStore(address nodeOwner) internal { // <= FOUND
426:         NativeVaultLib.Storage storage self = _state();
427:         NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner];
428: 
429:         
430:         uint256 slashedAssets = node.totalRestakedETH - convertToAssets(balanceOf(nodeOwner));
431: 
432:         
433:         uint256 slashedWithdrawable = Math.min(node.nodeAddress.balance, slashedAssets);
434: 
435:         
436:         INativeNode(node.nodeAddress).withdraw(self.slashStore, slashedWithdrawable);
437: 
438:         
439:         node.totalRestakedETH -= slashedWithdrawable;
440: 
441:         
442:         
443:         if (node.nodeAddress.balance < node.withdrawableCreditedNodeETH) {
444:             node.withdrawableCreditedNodeETH = node.nodeAddress.balance;
445:         }
446:     }
```


</details>

## [Low-5] Unsafe use of transfer()/transferFrom() with IERC20

### Resolution 
SafeTransfer should be used in place of Transfer for Solidity contracts to ensure robust security and error handling. Unlike the basic Transfer function, SafeTransfer incorporates safeguards against potential smart contract vulnerabilities, such as reentrancy attacks and unexpected token loss. By automatically validating the recipient's ability to receive tokens and reverting transactions in case of failures, 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[125](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L125-L146)']
```solidity
125:     function startRedeem(uint256 shares, address beneficiary)
126:         external
127:         whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:         nonReentrant
129:         returns (bytes32 withdrawalKey)
130:     {
131:         if (shares == 0) revert ZeroShares();
132:         if (beneficiary == address(0)) revert ZeroAddress();
133: 
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
135:         address staker = msg.sender;
136: 
137:         uint256 assets = convertToAssets(shares);
138: 
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);
140: 
141:         state.withdrawalMap[withdrawalKey].staker = staker;
142:         state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
143:         state.withdrawalMap[withdrawalKey].shares = shares;
144:         state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;
145: 
146:         this.transferFrom(msg.sender, address(this), shares); // <= FOUND
147: 
148:         emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
149:     }
```


</details>

## [Low-6] Large transfers may not work with some ERC20 tokens

### Resolution 
Large transfers with some ERC20 tokens may not work due to various reasons. Some tokens may have transfer restrictions built into the contract, such as daily transfer limits or maximum transfer sizes per transaction, to comply with regulatory requirements or to mitigate risks. Others may face issues with rounding errors when dealing with large quantities, especially if they have a high number of decimal places. Resolution involves carefully reading the token's contract to understand its constraints and behaviors and performing transfers accordingly. It may also be necessary to split large transfers into smaller increments if the token enforces specific transfer limits.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[52](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L52-L56)']
```solidity
52:     function handleSlashing(IERC20 token, uint256 amount) external { // <= FOUND
53:         if (amount == 0) revert ZeroAmount();
54:         if (!_config().supportedAssets[token]) revert UnsupportedAsset();
55: 
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount); // <= FOUND
57:         
58:         SafeTransferLib.safeTransfer(address(token), address(0), amount); // <= FOUND
59:     }
```
['[125](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L125-L146)']
```solidity
125:     function startRedeem(uint256 shares, address beneficiary)
126:         external
127:         whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:         nonReentrant
129:         returns (bytes32 withdrawalKey)
130:     {
131:         if (shares == 0) revert ZeroShares();
132:         if (beneficiary == address(0)) revert ZeroAddress();
133: 
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
135:         address staker = msg.sender;
136: 
137:         uint256 assets = convertToAssets(shares);
138: 
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);
140: 
141:         state.withdrawalMap[withdrawalKey].staker = staker;
142:         state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
143:         state.withdrawalMap[withdrawalKey].shares = shares;
144:         state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;
145: 
146:         this.transferFrom(msg.sender, address(this), shares); // <= FOUND
147: 
148:         emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
149:     }
```


</details>

## [Low-7] Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

### Resolution 
While adherence to the check-effects-interaction pattern is commendable, the absence of a reentrancy guard in functions, especially where transfer hooks might be present, can expose the protocol users to risks of read-only reentrancies. Such reentrancy vulnerabilities can be exploited to execute malicious actions even without altering the contract state. Without a reentrancy guard, the only potential mitigation would be to blocklist the entire protocol - an extreme and disruptive measure. Therefore, incorporating a reentrancy guard into these functions is vital to bolster security, as it helps protect against both traditional reentrancy attacks and read-only reentrancies, ensuring robust and safe protocol operations.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[52](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L52-L58)']
```solidity
52:     function handleSlashing(IERC20 token, uint256 amount) external { // <= FOUND
53:         if (amount == 0) revert ZeroAmount();
54:         if (!_config().supportedAssets[token]) revert UnsupportedAsset();
55: 
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount);
57:         
58:         SafeTransferLib.safeTransfer(address(token), address(0), amount); // <= FOUND
59:     }
```
['[52](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L52-L58)']
```solidity
52:     function handleSlashing(IERC20 token, uint256 amount) external {
53:         if (amount == 0) revert ZeroAmount();
54:         if (!_config().supportedAssets[token]) revert UnsupportedAsset();
55: 
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount);
57:         
58:         SafeTransferLib.safeTransfer(address(token), address(0), amount); // <= FOUND
59:     }
```


</details>

## [Low-8] Solidity version 0.8.20 won't work on all chains due to PUSH0

### Resolution 
Solidity version 0.8.20 uses the new Shanghai EVM which introduces the PUSH0 opcode, this may not be implemented on all chains and L2 thus reducing the portability and compatability of the code. Consider using a earlier solidity version.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L2-L2)']
```solidity
2: pragma solidity ^0.8.25; // <= FOUND
```
['[3](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L3-L3)']
```solidity
3: pragma solidity ^0.8.21; // <= FOUND
```
['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L4-L4)']
```solidity
4: pragma solidity ^0.8.0; // <= FOUND
```


</details>

## [Low-9] Double imports in solidity file

### Resolution 
The same library was imported twice, as such one instance should be safely removed

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L2-L25)']
```solidity
2: 
3: pragma solidity ^0.8.25;
4: 
5: import {OwnableRoles} from "solady/src/auth/OwnableRoles.sol";
6: import {ReentrancyGuard} from "solady/src/utils/ReentrancyGuard.sol";
7: 
8: import {IBeacon} from "@openzeppelin/contracts/proxy/beacon/IBeacon.sol";
9: import {Initializable} from "@openzeppelin-upgradeable/proxy/utils/Initializable.sol";
10: 
11: import {Pauser} from "./entities/Pauser.sol";
12: import {CoreLib} from "./entities/CoreLib.sol";
13: import {VaultLib} from "./entities/VaultLib.sol";
14: import {Operator} from "./entities/Operator.sol";
15: import {ExtSloads} from "./utils/ExtSloads.sol";
16: import {CommonUtils} from "./utils/CommonUtils.sol";
17: 
18: import {ICore, SlasherLib} from "./interfaces/ICore.sol";
19: import {Constants} from "./interfaces/Constants.sol"; // <= FOUND
20: import {IKarakBaseVault} from "./interfaces/IKarakBaseVault.sol";
21: import {IDSS} from "./interfaces/IDSS.sol";
22: 
23: import "./interfaces/Errors.sol";
24: import "./interfaces/Events.sol";
25: import "./interfaces/Constants.sol"; // <= FOUND
26: 
27: contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads {
28:     using CoreLib for CoreLib.Storage;
29:     using Operator for CoreLib.Storage;
30:     using Operator for Operator.State;
31:     using SlasherLib for SlasherLib.QueuedSlashing;
32:     using SlasherLib for SlasherLib.SlashRequest;
33:     using SlasherLib for CoreLib.Storage;
34:     using VaultLib for VaultLib.Config;
35:     using CommonUtils for address;
36: 
37:     string public constant VERSION = "2.0.0";
38: 
40:     bytes32 internal constant STORAGE_SLOT = 0x13c729cff436dc8ac22d145f2c778f6a709d225083f39538cc5e2674f2f10700;
41: 
43:     constructor() {
44:         _disableInitializers();
45:     }
46: 
54:     function initialize(
55:         address _vaultImpl,
56:         address _manager,
57:         address _vetoCommittee,
58:         uint32 _hookCallGasLimit,
59:         uint32 _supportsInterfaceGasLimit,
60:         uint32 _hookGasBuffer
61:     ) external initializer {
62:         _initializeOwner(msg.sender);
63:         __Pauser_init();
64: 
65:         _grantRoles(_manager, Constants.MANAGER_ROLE);
66:         _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);
67: 
68:         _self().init(_vaultImpl, _vetoCommittee, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
69:     }
70: 
73:     function pause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {
74:         _pause(map);
75:     }
76: 
79:     function unpause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {
80:         _unpause(map);
81:     }
82: 
86:     function allowlistAssets(address[] memory assets, address[] memory slashingHandlers)
87:         external
88:         onlyRolesOrOwner(Constants.MANAGER_ROLE)
89:     {
90:         _self().allowlistAssets(assets, slashingHandlers);
91:         emit AllowlistedAssets(assets);
92:     }
93: 
98:     function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)
99:         external
100:         whenFunctionNotPaused(Constants.PAUSE_CORE_REGISTER_TO_DSS)
101:         nonReentrant
102:     {
103:         address operator = msg.sender;
104:         CoreLib.Storage storage self = _self();
105:         if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();
106:         self.registerOperatorToDSS(dss, operator, registrationHookData);
107:         emit RegisteredOperatorToDSS(operator, address(dss));
108:     }
109: 
114:     function unregisterOperatorFromDSS(IDSS dss, bytes memory unregistrationHookData)
115:         external
116:         nonReentrant
117:         whenFunctionNotPaused(Constants.PAUSE_CORE_UNREGISTER_FROM_DSS)
118:     {
119:         address operator = msg.sender;
120:         CoreLib.Storage storage self = _self();
121:         self.checkIfOperatorIsRegInRegDSS(operator, dss);
122:         self.unregisterOperatorFromDSS(dss, operator, unregistrationHookData);
123: 
124:         emit UnregisteredOperatorToDSS(operator, address(dss));
125:     }
126: 
131:     function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest)
132:         external
133:         nonReentrant
134:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_STAKE_UPDATE)
135:         returns (Operator.QueuedStakeUpdate memory updatedStake)
136:     {
137:         address operator = msg.sender;
138:         CoreLib.Storage storage self = _self();
139:         self.checkIfOperatorIsRegInRegDSS(operator, vaultStakeUpdateRequest.dss);
140:         updatedStake = self.requestUpdateVaultStakeInDSS(vaultStakeUpdateRequest, self.nonce++, operator);
141:         emit RequestedStakeUpdate(updatedStake);
142:     }
143: 
147:     function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake)
148:         external
149:         nonReentrant
150:         whenFunctionNotPaused(Constants.PAUSE_CORE_FINALIZE_STAKE_UPDATE)
151:     {
152:         _self().validateAndUpdateVaultStakeInDSS(queuedStake);
153:         emit FinishedStakeUpdate(queuedStake);
154:     }
155: 
162:     function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)
163:         external
164:         whenFunctionNotPaused(Constants.PAUSE_CORE_DEPLOY_VAULTS)
165:         nonReentrant
166:         returns (IKarakBaseVault[] memory vaults)
167:     {
168:         vaults = _self().deployVaults(msg.sender, vaultImpl, vaultConfigs);
169:     }
170: 
174:     function changeStandardImplementation(address newVaultImpl) external onlyOwner {
175:         if (newVaultImpl == address(0)) revert ZeroAddress();
176:         if (newVaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();
177:         _self().vaultImpl = newVaultImpl;
178:         emit UpgradedAllVaults(newVaultImpl);
179:     }
180: 
184:     function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner {
185:         CoreLib.Storage storage self = _self();
186:         if (!self.isVaultImplAllowlisted(newVaultImpl)) revert VaultImplNotAllowlisted();
187:         
188:         
189:         if (self.vaultToImplMap[vault] == address(0)) revert VaultNotAChildVault();
190: 
191:         self.vaultToImplMap[vault] = newVaultImpl;
192:         emit UpgradedVault(newVaultImpl, vault);
193:     }
194: 
198:     function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {
199:         vault.pause(map);
200:     }
201: 
205:     function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) {
206:         vault.unpause(map);
207:     }
208: 
212:     function allowlistVaultImpl(address vaultImpl) external onlyOwner {
213:         if (vaultImpl == address(0)) revert ZeroAddress();
214:         if (vaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();
215: 
216:         _self().allowlistVaultImpl(vaultImpl);
217:     }
218: 
221:     function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)
222:         external
223:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
224:         nonReentrant
225:         returns (SlasherLib.QueuedSlashing memory queuedSlashing)
226:     {
227:         IDSS dss = IDSS(msg.sender);
228:         CoreLib.Storage storage self = _self();
229:         self.checkIfOperatorIsRegInRegDSS(slashingRequest.operator, dss);
230:         queuedSlashing = self.requestSlashing(dss, slashingRequest, self.nonce++);
231:         emit RequestedSlashing(address(dss), slashingRequest);
232:     }
233: 
236:     function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)
237:         external
238:         whenFunctionNotPaused(Constants.PAUSE_CORE_CANCEL_SLASHING)
239:         nonReentrant
240:         onlyRoles(Constants.VETO_COMMITTEE_ROLE)
241:     {
242:         _self().cancelSlashing(queuedSlashing);
243:         emit CancelledSlashing(msg.sender, queuedSlashing);
244:     }
245: 
249:     function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)
250:         external
251:         nonReentrant
252:         whenFunctionNotPaused(Constants.PAUSE_CORE_FINALIZE_SLASHING)
253:     {
254:         _self().finalizeSlashing(queuedSlashing);
255: 
256:         emit FinalizedSlashing(msg.sender, queuedSlashing);
257:     }
258: 
263:     function registerDSS(uint256 maxSlashablePercentageWad) external {
264:         IDSS dss = IDSS(msg.sender);
265:         if (!address(dss).isSmartContract()) revert NotSmartContract();
266:         _self().setDSSMaxSlashablePercentageWad(dss, maxSlashablePercentageWad);
267:         emit DSSRegistered(msg.sender, maxSlashablePercentageWad);
268:     }
269: 
275:     function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)
276:         external
277:         onlyRolesOrOwner(Constants.MANAGER_ROLE)
278:     {
279:         _self().updateGasValues(_hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
280:     }
281: 
289:     function isAssetAllowlisted(address asset) public view returns (bool) {
290:         return _self().assetSlashingHandlers[asset] != address(0);
291:     }
292: 
295:     function isVaultImplAllowListed(address vaultImpl) public view returns (bool) {
296:         return _self().isVaultImplAllowlisted(vaultImpl);
297:     }
298: 
303:     function isOperatorRegisteredToDSS(address operator, IDSS dss) public view returns (bool) {
304:         return _self().isOperatorRegisteredToDSS(operator, dss);
305:     }
306: 
309:     function implementation() external view override returns (address) {
310:         return implementation(msg.sender);
311:     }
312: 
319:     function implementation(address vault) public view returns (address) {
320:         CoreLib.Storage storage self = _self();
321:         address vaultImplOverride = self.vaultToImplMap[vault];
322: 
323:         if (vaultImplOverride == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) {
324:             return self.vaultImpl;
325:         }
326:         return vaultImplOverride;
327:     }
328: 
332:     function getOperatorVaults(address operator) external view returns (address[] memory vaults) {
333:         return _self().operatorState[operator].getVaults();
334:     }
335: 
340:     function fetchVaultsStakedInDSS(address operator, IDSS dss) external view returns (address[] memory vaults) {
341:         vaults = _self().operatorState[operator].getVaultsStakedToDSS(dss);
342:     }
343: 
350:     function getLeverage(address vault) external view returns (uint256 leverage) {
351:         leverage = _self().getDSSCountVaultStakedTo(IKarakBaseVault(vault));
352:         leverage *= Constants.HUNDRED_PERCENT_WAD;
353:     }
354: 
359:     function getDssMaxSlashablePercentageWad(IDSS dss) public view returns (uint256 slashablePercentageWad) {
360:         slashablePercentageWad = _self().getDSSMaxSlashablePercentageWad(dss);
361:     }
362: 
366:     function isDSSRegistered(IDSS dss) public view returns (bool) {
367:         return _self().isDSSRegistered(dss);
368:     }
369: 
374:     function extSloads(bytes32[] calldata slots)
375:         public
376:         view
377:         override(ExtSloads, ICore)
378:         returns (bytes32[] memory res)
379:     {
380:         res = super.extSloads(slots);
381:     }
382: 
386:     function _self() internal pure returns (CoreLib.Storage storage $) {
387:         assembly {
388:             $.slot := STORAGE_SLOT
389:         }
390:     }
391:     
392: }
393: 
```


</details>

## [Low-10] Missing events in functions that are either setters, privileged or voting related

### Resolution 
Sensitive setter functions in smart contracts often alter critical state variables. Without events emitted in these functions, external observers or dApps cannot easily track or react to these state changes. Missing events can obscure contract activity, hampering transparency and making integration more challenging. To resolve this, incorporate appropriate event emissions within these functions. Events offer an efficient way to log crucial changes, aiding in real-time tracking and post-transaction verification.

Num of instances: 17

### Findings 


<details><summary>Click to show findings</summary>

['[274](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L274-L274)']
```solidity
274:     function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit)
275:         external
276:         onlyRolesOrOwner(Constants.MANAGER_ROLE)
277:     
```
['[174](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L174-L174)']
```solidity
174:     function setDSSMaxSlashablePercentageWad(
175:         CoreLib.Storage storage self,
176:         IDSS dss,
177:         uint256 dssMaxSlashablePercentageWad
178:     ) public 
```
['[103](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L103-L103)']
```solidity
103:     function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal 
```
['[56](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L56-L56)']
```solidity
56:     function updateGasValues(
57:         Storage storage self,
58:         uint32 _hookCallGasLimit,
59:         uint32 _supportsInterfaceGasLimit,
60:         uint32 _hookGasBuffer
61:     ) internal 
```
['[517](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L517-L517)']
```solidity
517:     function _updateBalance(address _of, int256 assets) internal 
```
['[43](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L43-L43)']
```solidity
43:     function addSlashableToken(IERC20 token) external onlyOwner 
```
['[211](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L211-L211)']
```solidity
211:     function allowlistVaultImpl(address vaultImpl) external onlyOwner 
```
['[322](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L322-L322)']
```solidity
322:     function pause(uint256 map) external onlyOwner 
```
['[328](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L328-L328)']
```solidity
328:     function unpause(uint256 map) external onlyOwner 
```
['[322](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L322-L322)']
```solidity
322:     function pause(uint256 map) external onlyOwner 
```
['[328](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L328-L328)']
```solidity
328:     function unpause(uint256 map) external onlyOwner 
```
['[72](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L72-L72)']
```solidity
72:     function pause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```
['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L78-L78)']
```solidity
78:     function unpause(uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```
['[197](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L197-L197)']
```solidity
197:     function pauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```
['[204](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L204-L204)']
```solidity
204:     function unpauseVault(IKarakBaseVault vault, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```
['[334](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L334-L334)']
```solidity
334:     function pauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```
['[340](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L340-L340)']
```solidity
340:     function unpauseNode(INativeNode node, uint256 map) external onlyRolesOrOwner(Constants.MANAGER_ROLE) 
```


</details>

## [Low-11] Unsafe use of transfer()/transferFrom() with IERC20

### Resolution 
SafeTransfer should be used in place of Transfer for Solidity contracts to ensure robust security and error handling. Unlike the basic Transfer function, SafeTransfer incorporates safeguards against potential smart contract vulnerabilities, such as reentrancy attacks and unexpected token loss. By automatically validating the recipient's ability to receive tokens and reverting transactions in case of failures, 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[125](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L125-L146)']
```solidity
125:     function startRedeem(uint256 shares, address beneficiary)
126:         external
127:         whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:         nonReentrant
129:         returns (bytes32 withdrawalKey)
130:     {
131:         if (shares == 0) revert ZeroShares();
132:         if (beneficiary == address(0)) revert ZeroAddress();
133: 
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
135:         address staker = msg.sender;
136: 
137:         uint256 assets = convertToAssets(shares);
138: 
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);
140: 
141:         state.withdrawalMap[withdrawalKey].staker = staker;
142:         state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
143:         state.withdrawalMap[withdrawalKey].shares = shares;
144:         state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;
145: 
146:         this.transferFrom(msg.sender, address(this), shares); // <= FOUND
147: 
148:         emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
149:     }
```


</details>

## [Low-12] Avoid floating pragma in non interface/library files

### Resolution 
Avoid using floating pragmas in non-interface and non-library files to ensure contract compatibility and security. Floating pragmas like `pragma solidity ^0.8.0;` allow any compiler version that matches the specified range. While this can provide flexibility, it risks introducing unexpected behavior or vulnerabilities from future compiler versions. Instead, specify a fixed pragma version, such as `pragma solidity 0.8.0;`, to guarantee consistent behavior and security across deployments. This practice ensures that your contracts are tested and verified against a specific compiler version, reducing the risk of unforeseen issues and maintaining code reliability.

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

[]
```solidity
16: contract SlashingHandler is Initializable, Ownable, ISlashingHandler 
```
[]
```solidity
12: contract SlashStore is Initializable, Ownable, ReentrancyGuard 
```
[]
```solidity
29: contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault 
```
[]
```solidity
26: contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads 
```
[]
```solidity
9: contract Querier 
```
[]
```solidity
25: contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard 
```
[]
```solidity
17: contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard 
```
[]
```solidity
10: contract Pauser is Initializable, ContextUpgradeable 
```
[]
```solidity
4: abstract contract ExtSloads 
```


</details>

## [Low-13] Solidity version 0.8.20 won't work on all chains due to PUSH0

### Resolution 
Solidity version 0.8.20 uses the new Shanghai EVM which introduces the PUSH0 opcode, this may not be implemented on all chains and L2 thus reducing the portability and compatability of the code. Consider using a earlier solidity version.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L2-L2)']
```solidity
2: pragma solidity ^0.8.25; // <= FOUND
```
['[3](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L3-L3)']
```solidity
3: pragma solidity ^0.8.21; // <= FOUND
```
['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L4-L4)']
```solidity
4: pragma solidity ^0.8.0; // <= FOUND
```


</details>

## [Low-14] Low level calls in solidity versions preceding 0.8.14 can result in an optimiser bug

### Resolution 
In Solidity versions 0.8.13 and 0.8.14, a known optimizer bug presents potential risks when a variable is used in a separate assembly block from the one in which it was stored. Specifically, the 'mstore' operation could be optimized out due to this bug, leading to the use of uninitialized memory. Although the current code does not exhibit this risky pattern of execution, it does utilize 'mstore' within assembly blocks, which introduces a vulnerability risk for future code modifications. As a preventative measure, it is advisable to avoid the usage of the afflicted Solidity versions, 0.8.13 and 0.8.14. Instead, consider utilizing a version that is not impacted by this optimizer bug to prevent potential memory initialization issues in your smart contract.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[58](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L58-L58)']
```solidity
58:                 assembly { // <= FOUND
59:                     mstore(0x00, computedHash)
60:                     mstore(0x20, mload(add(proof, i)))
61:                     computedHash := keccak256(0x00, 0x40)
62:                     index := div(index, 2)
63:                 }
```
['[116](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L116-L116)']
```solidity
116:                 assembly { // <= FOUND
117:                     mstore(0x00, mload(computedHash))
118:                     mstore(0x20, mload(add(proof, i)))
119:                     if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) }
120:                     index := div(index, 2)
121:                 }
```


</details>

## [Low-15] Ownable2Step should be used in place of Ownable

### Resolution 
Ownable2Step further prevents risks posed by centralised privileges as there is a smaller likelihood of the owner being wrongfully changed

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L16-L16)']
```solidity
16: contract SlashingHandler is Initializable, Ownable, ISlashingHandler  // <= FOUND
```
['[12](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L12-L12)']
```solidity
12: contract SlashStore is Initializable, Ownable, ReentrancyGuard  // <= FOUND
```
['[29](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L29-L29)']
```solidity
29: contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault  // <= FOUND
```
['[17](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeNode.sol#L17-L17)']
```solidity
17: contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard  // <= FOUND
```


</details>

## [Low-16] The call abi.encodeWithSelector is not type safe

### Resolution 
In Solidity, `abi.encodeWithSelector` is a function used for encoding data along with a function selector, but it is not type-safe. This means it does not enforce type checking at compile time, potentially leading to errors if arguments do not match the expected types. Starting from version 0.8.13, Solidity introduced `abi.encodeCall`, which offers a safer alternative. `abi.encodeCall` ensures type safety by performing a full type check, aligning the types of the arguments with the function signature. This reduces the risk of bugs caused by typographical errors or mismatched types. Using `abi.encodeCall` enhances the reliability and security of the code by ensuring that the encoded data strictly conforms to the specified types, making it a preferable choice in Solidity versions 0.8.13 and above.

Num of instances: 16

### Findings 


<details><summary>Click to show findings</summary>

['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L78-L80)']
```solidity
78:         HookLib.callHookIfInterfaceImplemented({
79:             dss: dss,
80:             data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate), // <= FOUND
81:             interfaceId: dss.requestUpdateStakeHook.selector,
82:             ignoreFailure: !requestStakeUpdate.toStake,
83:             hookCallGasLimit: self.hookCallGasLimit,
84:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
85:             hookGasBuffer: self.hookGasBuffer
86:         });
```
['[124](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L124-L126)']
```solidity
124:         HookLib.callHookIfInterfaceImplemented({
125:             dss: dss,
126:             data: abi.encodeWithSelector(dss.finishUpdateStakeHook.selector, msg.sender), // <= FOUND
127:             interfaceId: dss.finishUpdateStakeHook.selector,
128:             ignoreFailure: true,
129:             hookCallGasLimit: self.hookCallGasLimit,
130:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
131:             hookGasBuffer: self.hookGasBuffer
132:         });
```
['[162](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L162-L164)']
```solidity
162:         HookLib.callHookIfInterfaceImplemented({
163:             dss: dss,
164:             data: abi.encodeWithSelector(dss.registrationHook.selector, operator, registrationHookData), // <= FOUND
165:             interfaceId: dss.registrationHook.selector,
166:             ignoreFailure: false,
167:             hookCallGasLimit: self.hookCallGasLimit,
168:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
169:             hookGasBuffer: self.hookGasBuffer
170:         });
```
['[194](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L194-L196)']
```solidity
194:         HookLib.callHookIfInterfaceImplemented({
195:             dss: dss,
196:             data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData), // <= FOUND
197:             interfaceId: dss.unregistrationHook.selector,
198:             ignoreFailure: true, 
199:             hookCallGasLimit: self.hookCallGasLimit,
200:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
201:             hookGasBuffer: self.hookGasBuffer
202:         });
```
['[91](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L91-L93)']
```solidity
91:         (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(
92:             address(dss),
93:             abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId), // <= FOUND
94:             supportsInterfaceGasLimit
95:         );
```
['[113](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L113-L115)']
```solidity
113:         HookLib.callHookIfInterfaceImplemented({
114:             dss: dss,
115:             data: abi.encodeWithSelector( // <= FOUND
116:                 dss.requestSlashingHook.selector, slashingMetadata.operator, slashingMetadata.slashPercentagesWad
117:             ),
118:             interfaceId: dss.requestSlashingHook.selector,
119:             ignoreFailure: true,
120:             hookCallGasLimit: self.hookCallGasLimit,
121:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
122:             hookGasBuffer: self.hookGasBuffer
123:         });
```
['[142](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L142-L144)']
```solidity
142:         HookLib.callHookIfInterfaceImplemented({
143:             dss: dss,
144:             data: abi.encodeWithSelector(dss.finishSlashingHook.selector, queuedSlashing.operator), // <= FOUND
145:             interfaceId: dss.finishSlashingHook.selector,
146:             ignoreFailure: true,
147:             hookCallGasLimit: self.hookCallGasLimit,
148:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
149:             hookGasBuffer: self.hookGasBuffer
150:         });
```
['[159](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L159-L161)']
```solidity
159:         HookLib.callHookIfInterfaceImplemented({
160:             dss: dss,
161:             data: abi.encodeWithSelector(dss.cancelSlashingHook.selector, queuedSlashing.operator), // <= FOUND
162:             interfaceId: dss.cancelSlashingHook.selector,
163:             ignoreFailure: true,
164:             hookCallGasLimit: self.hookCallGasLimit,
165:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
166:             hookGasBuffer: self.hookGasBuffer
167:         });
```
['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L78-L80)']
```solidity
78:         HookLib.callHookIfInterfaceImplemented({
79:             dss: dss,
80:             data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate), // <= FOUND
81:             interfaceId: dss.requestUpdateStakeHook.selector,
82:             ignoreFailure: !requestStakeUpdate.toStake,
83:             hookCallGasLimit: self.hookCallGasLimit,
84:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
85:             hookGasBuffer: self.hookGasBuffer
86:         });
```
['[124](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L124-L126)']
```solidity
124:         HookLib.callHookIfInterfaceImplemented({
125:             dss: dss,
126:             data: abi.encodeWithSelector(dss.finishUpdateStakeHook.selector, msg.sender), // <= FOUND
127:             interfaceId: dss.finishUpdateStakeHook.selector,
128:             ignoreFailure: true,
129:             hookCallGasLimit: self.hookCallGasLimit,
130:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
131:             hookGasBuffer: self.hookGasBuffer
132:         });
```
['[162](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L162-L164)']
```solidity
162:         HookLib.callHookIfInterfaceImplemented({
163:             dss: dss,
164:             data: abi.encodeWithSelector(dss.registrationHook.selector, operator, registrationHookData), // <= FOUND
165:             interfaceId: dss.registrationHook.selector,
166:             ignoreFailure: false,
167:             hookCallGasLimit: self.hookCallGasLimit,
168:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
169:             hookGasBuffer: self.hookGasBuffer
170:         });
```
['[194](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L194-L196)']
```solidity
194:         HookLib.callHookIfInterfaceImplemented({
195:             dss: dss,
196:             data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData), // <= FOUND
197:             interfaceId: dss.unregistrationHook.selector,
198:             ignoreFailure: true, 
199:             hookCallGasLimit: self.hookCallGasLimit,
200:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
201:             hookGasBuffer: self.hookGasBuffer
202:         });
```
['[91](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L91-L93)']
```solidity
91:         (bool success, bytes32 result) = performLowLevelCallAndLimitReturnData(
92:             address(dss),
93:             abi.encodeWithSelector(IERC165.supportsInterface.selector, interfaceId), // <= FOUND
94:             supportsInterfaceGasLimit
95:         );
```
['[113](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L113-L115)']
```solidity
113:         HookLib.callHookIfInterfaceImplemented({
114:             dss: dss,
115:             data: abi.encodeWithSelector( // <= FOUND
116:                 dss.requestSlashingHook.selector, slashingMetadata.operator, slashingMetadata.slashPercentagesWad
117:             ),
118:             interfaceId: dss.requestSlashingHook.selector,
119:             ignoreFailure: true,
120:             hookCallGasLimit: self.hookCallGasLimit,
121:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
122:             hookGasBuffer: self.hookGasBuffer
123:         });
```
['[142](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L142-L144)']
```solidity
142:         HookLib.callHookIfInterfaceImplemented({
143:             dss: dss,
144:             data: abi.encodeWithSelector(dss.finishSlashingHook.selector, queuedSlashing.operator), // <= FOUND
145:             interfaceId: dss.finishSlashingHook.selector,
146:             ignoreFailure: true,
147:             hookCallGasLimit: self.hookCallGasLimit,
148:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
149:             hookGasBuffer: self.hookGasBuffer
150:         });
```
['[159](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L159-L161)']
```solidity
159:         HookLib.callHookIfInterfaceImplemented({
160:             dss: dss,
161:             data: abi.encodeWithSelector(dss.cancelSlashingHook.selector, queuedSlashing.operator), // <= FOUND
162:             interfaceId: dss.cancelSlashingHook.selector,
163:             ignoreFailure: true,
164:             hookCallGasLimit: self.hookCallGasLimit,
165:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
166:             hookGasBuffer: self.hookGasBuffer
167:         });
```


</details>

## [Low-17] Upgradable contracts should have a __gap variable

### Resolution 
This is to ensure the team can add new state variables without compromising compatability.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L16-L16)']
```solidity
16: contract SlashingHandler is Initializable, Ownable, ISlashingHandler 
```
['[12](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L12-L12)']
```solidity
12: contract SlashStore is Initializable, Ownable, ReentrancyGuard 
```
['[29](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L29-L29)']
```solidity
29: contract Vault is ERC4626, Initializable, Ownable, Pauser, ReentrancyGuard, ExtSloads, IVault 
```
['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L26-L26)']
```solidity
26: contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads 
```
['[10](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L10-L10)']
```solidity
10: contract Pauser is Initializable, ContextUpgradeable 
```


</details>

## [Low-18] Contracts are vulnerable to fee-on-transfer accounting-related issues

### Resolution 
The below-listed functions use `transferFrom()` to move funds from the sender to the recipient but fail to verify if the received token amount matches the transferred amount. This could pose an issue with fee-on-transfer tokens, where the post-transfer balance might be less than anticipated, leading to balance inconsistencies. There might be subsequent checks for a second transfer, but an attacker might exploit leftover funds (such as those accidentally sent by another user) to gain unjustified credit. A practical solution is to gauge the balance prior and post-transfer, and consider the differential as the transferred amount, instead of the predefined amount.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[52](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L52-L56)']
```solidity
52:     function handleSlashing(IERC20 token, uint256 amount) external {
53:         if (amount == 0) revert ZeroAmount();
54:         if (!_config().supportedAssets[token]) revert UnsupportedAsset();
55: 
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount); // <= FOUND
57:         
58:         SafeTransferLib.safeTransfer(address(token), address(0), amount);
59:     }
```


</details>

## [Low-19] Upgradable contracts should have an initialization function

### Resolution 
Upgradable contracts in Solidity should have an initialization function to ensure proper setup, maintain state consistency, and enhance security. Unlike regular contracts, upgradable contracts use a proxy pattern that separates the contract's logic from its data storage, enabling seamless updates to the logic without affecting the stored data. However, this approach requires careful initialization of the contract state to avoid inconsistencies or vulnerabilities.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[10](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L10-L10)']
```solidity
10: contract Pauser is Initializable, ContextUpgradeable { // <= FOUND
11:     struct PauserStorage {
12:         uint256 _paused;
13:     }
14: 
16:     bytes32 private constant PAUSER_STORAGE_SLOT = 0x271441cddf42198c20456f920f5dac04f245854c82f280f2e59e7095958d0b00;
17: 
18:     function _getPauserStorage() private pure returns (PauserStorage storage $) {
19:         assembly {
20:             $.slot := PAUSER_STORAGE_SLOT
21:         }
22:     }
23: 
24:     event Paused(address account, uint256 map);
25: 
26:     event Unpaused(address account, uint256 map);
27: 
28:     error EnforcedPause();
29: 
30:     error EnforcedPauseFunction(uint8 functionIndex);
31: 
32:     error AttemptedUnpauseWhilePausing();
33: 
34:     error AttemptedPauseWhileUnpausing();
35: 
36:     function __Pauser_init() internal onlyInitializing {
37:         __Pauser_init_unchained();
38:     }
39: 
40:     function __Pauser_init_unchained() internal onlyInitializing {
41:         _getPauserStorage()._paused = 0;
42:     }
43: 
44:     modifier whenNotPaused() {
45:         if (paused()) revert EnforcedPause();
46:         _;
47:     }
48: 
49:     modifier whenFunctionNotPaused(uint8 index) {
50:         if (paused(index)) revert EnforcedPauseFunction(index);
51:         _;
52:     }
53: 
54:     function paused() public view virtual returns (bool) {
55:         return (_getPauserStorage()._paused != 0);
56:     }
57: 
58:     function paused(uint8 index) public view virtual returns (bool) {
59:         uint256 mask = 1 << index;
60:         return ((_getPauserStorage()._paused & mask) != 0);
61:     }
62: 
63:     function pausedMap() public view virtual returns (uint256) {
64:         return _getPauserStorage()._paused;
65:     }
66: 
67:     function _pause(uint256 map) internal virtual {
68:         PauserStorage storage self = _getPauserStorage();
69:         if ((self._paused & map) != self._paused) revert AttemptedUnpauseWhilePausing();
70:         self._paused = map;
71:         emit Paused(_msgSender(), map);
72:     }
73: 
74:     function _unpause(uint256 map) internal virtual {
75:         PauserStorage storage self = _getPauserStorage();
76:         if (self._paused & map != map) revert AttemptedPauseWhileUnpausing();
77:         self._paused = map;
78:         emit Unpaused(_msgSender(), map);
79:     }
80: }
```


</details>

## [Low-20] The nonReentrant modifier should be first in a function declaration

### Resolution 
In Solidity, the `nonReentrant` modifier is essential for securing smart contracts against reentrancy attacks. It should be positioned first in a function declaration. This placement is critical because it ensures that the modifier's protection is applied before any other code or modifiers in the function. If placed later, other modifiers could potentially be executed in a reentrant manner before `nonReentrant` has a chance to lock the function, leaving the contract vulnerable. Thus, prioritizing `nonReentrant` as the first modifier is a best practice for robust smart contract security, effectively guarding against unintended reentries and related exploits.

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L78-L82)']
```solidity
78:     function deposit(uint256 assets, address to)
79:         public
80:         override(ERC4626, IVault)
81:         whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
82:         nonReentrant // <= FOUND
83:         returns (uint256 shares)
84:     {
85:         if (assets == 0) revert ZeroAmount();
86:         return super.deposit(assets, to);
87:     }
```
['[110](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L110-L114)']
```solidity
110:     function mint(uint256 shares, address to)
111:         public
112:         override(ERC4626, IVault)
113:         whenFunctionNotPaused(Constants.PAUSE_VAULT_MINT)
114:         nonReentrant // <= FOUND
115:         returns (uint256 assets)
116:     {
117:         if (shares == 0) revert ZeroShares();
118:         assets = super.mint(shares, to);
119:     }
```
['[125](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L125-L128)']
```solidity
125:     function startRedeem(uint256 shares, address beneficiary)
126:         external
127:         whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:         nonReentrant // <= FOUND
129:         returns (bytes32 withdrawalKey)
130:     {
131:         if (shares == 0) revert ZeroShares();
132:         if (beneficiary == address(0)) revert ZeroAddress();
133: 
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
135:         address staker = msg.sender;
136: 
137:         uint256 assets = convertToAssets(shares);
138: 
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);
140: 
141:         state.withdrawalMap[withdrawalKey].staker = staker;
142:         state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
143:         state.withdrawalMap[withdrawalKey].shares = shares;
144:         state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;
145: 
146:         this.transferFrom(msg.sender, address(this), shares);
147: 
148:         emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
149:     }
```
['[331](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L331-L335)']
```solidity
331:     function withdraw(uint256 assets, address to, address owner)
332:         public
333:         override
334:         whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:         nonReentrant // <= FOUND
336:         returns (uint256 shares)
337:     {
338:         
339:         owner = owner;
340:         assets = assets;
341:         to = to;
342:         shares = shares;
343: 
344:         revert NotImplemented();
345:     }
```
['[348](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L348-L352)']
```solidity
348:     function redeem(uint256 shares, address to, address owner)
349:         public
350:         override
351:         whenFunctionNotPaused(Constants.PAUSE_VAULT_REDEEM)
352:         nonReentrant // <= FOUND
353:         returns (uint256 assets)
354:     {
355:         
356:         owner = owner;
357:         to = to;
358:         shares = shares;
359:         assets = assets;
360: 
361:         revert NotImplemented();
362:     }
```
['[97](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L97-L100)']
```solidity
97:     function registerOperatorToDSS(IDSS dss, bytes memory registrationHookData)
98:         external
99:         whenFunctionNotPaused(Constants.PAUSE_CORE_REGISTER_TO_DSS)
100:         nonReentrant // <= FOUND
101:     {
102:         address operator = msg.sender;
103:         CoreLib.Storage storage self = _self();
104:         if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();
105:         self.registerOperatorToDSS(dss, operator, registrationHookData);
106:         emit RegisteredOperatorToDSS(operator, address(dss));
107:     }
```
['[161](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L161-L164)']
```solidity
161:     function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl)
162:         external
163:         whenFunctionNotPaused(Constants.PAUSE_CORE_DEPLOY_VAULTS)
164:         nonReentrant // <= FOUND
165:         returns (IKarakBaseVault[] memory vaults)
166:     {
167:         vaults = _self().deployVaults(msg.sender, vaultImpl, vaultConfigs);
168:     }
```
['[220](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L220-L223)']
```solidity
220:     function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)
221:         external
222:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
223:         nonReentrant // <= FOUND
224:         returns (SlasherLib.QueuedSlashing memory queuedSlashing)
225:     {
226:         IDSS dss = IDSS(msg.sender);
227:         CoreLib.Storage storage self = _self();
228:         self.checkIfOperatorIsRegInRegDSS(slashingRequest.operator, dss);
229:         queuedSlashing = self.requestSlashing(dss, slashingRequest, self.nonce++);
230:         emit RequestedSlashing(address(dss), slashingRequest);
231:     }
```
['[235](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L235-L238)']
```solidity
235:     function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing)
236:         external
237:         whenFunctionNotPaused(Constants.PAUSE_CORE_CANCEL_SLASHING)
238:         nonReentrant // <= FOUND
239:         onlyRoles(Constants.VETO_COMMITTEE_ROLE)
240:     {
241:         _self().cancelSlashing(queuedSlashing);
242:         emit CancelledSlashing(msg.sender, queuedSlashing);
243:     }
```


</details>

## [Low-21] Initializer function can be front run

### Resolution 
In Solidity contract deployment, not making the initialize() function call atomic with the contract creation can leave a vulnerability window. A malicious actor could exploit this time gap and call initialize() before the intended initialization. This action could disrupt the contract's setup, potentially necessitating a full contract re-deployment to ensure proper initialization. To mitigate such risks, it's advised to use a factory contract. This factory contract can be programmed to deploy and initialize a new contract in a single atomic transaction, closing the window of vulnerability and ensuring correct and secure contract initialization.

Num of instances: 6

### Findings 


<details><summary>Click to show findings</summary>

['[33](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L33-L33)']
```solidity
33:     function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer  // <= FOUND
```
['[20](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L20-L20)']
```solidity
20:     function initialize(address _owner) external initializer  // <= FOUND
```
['[46](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L46-L53)']
```solidity
46:     function initialize(
47:         address _owner,
48:         address _operator,
49:         address _depositToken,
50:         string memory _name,
51:         string memory _symbol,
52:         bytes memory _extraData
53:     ) external initializer  // <= FOUND
```
['[53](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L53-L60)']
```solidity
53:     function initialize(
54:         address _vaultImpl,
55:         address _manager,
56:         address _vetoCommittee,
57:         uint32 _hookCallGasLimit,
58:         uint32 _supportsInterfaceGasLimit,
59:         uint32 _hookGasBuffer
60:     ) external initializer  // <= FOUND
```
['[46](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L46-L53)']
```solidity
46:     function initialize(
47:         address _owner,
48:         address _operator,
49:         address _depositToken,
50:         string memory _name,
51:         string memory _symbol,
52:         bytes memory _extraData
53:     ) external initializer  // <= FOUND
```
['[28](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeNode.sol#L28-L28)']
```solidity
28:     function initialize(address _owner, address _nodeOwner) external initializer  // <= FOUND
```


</details>

## [Low-22] Use _disableInitializers() to ensure initialization occurs once

### Resolution 
`disableInitializers()` should be used in upgradeable contracts to ensure the initializer functions can't be called more than once. In upgradeable contracts, initializer functions set initial state and values, but if they can be invoked multiple times, it could lead to unexpected behavior or vulnerabilities. By calling `disableInitializers()` after the initial setup, you essentially lock the initializer functions, ensuring they can only be called once during the contract's lifecycle. This prevents repeated initializations, helping to maintain the integrity and security of the contract, and providing a safeguard against potential manipulation or misuse of the initialization functions.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[10](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L10-L10)']
```solidity
10: contract Pauser is Initializable, ContextUpgradeable  // <= FOUND
```


</details>

## [Low-23] Minting to the zero address should be avoided

### Resolution 
Minting tokens to the zero address in Solidity is a potential pitfall that should be carefully guarded against. The zero address (0x0) is generally used as a default value and represents an uninitialized or null address. Minting tokens to this address effectively burns them, making them inaccessible and permanently removing them from the total supply. This could lead to unintended token loss if performed accidentally. To prevent this, it's important to include a check in the minting function to ensure that the target address is not the zero address. Using a library like OpenZeppelin's `Address` can provide utility functions like `requireNonZero`, which simplifies this check and enhances the security of the minting function.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[110](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L110-L118)']
```solidity
110:     function mint(uint256 shares, address to)
111:         public
112:         override(ERC4626, IVault)
113:         whenFunctionNotPaused(Constants.PAUSE_VAULT_MINT)
114:         nonReentrant
115:         returns (uint256 assets)
116:     {
117:         if (shares == 0) revert ZeroShares(); // <= FOUND
118:         assets = super.mint(shares, to); // <= FOUND
119:     }
```


</details>

## [Low-24] Missing zero address check in constructor

### Resolution 
In Solidity, constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a check, there's a risk that an address parameter could be mistakenly set to the zero address (0x0). This could occur due to a mistake or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it are irretrievable. Therefore, it's crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[14](https://github.com/code-423n4/2024-07-karak/tree/main/src/Querier.sol#L14-L14)']
```solidity
14:     constructor(address coreAddress) { // <= FOUND
15:         core = ICore(coreAddress);
16:     }
```


</details>

## [Low-25] Return values of transfer()/transferFrom() not checked

### Resolution 
In Solidity, it's crucial to check the return value of `.transfer` and `.transferFrom` methods because not all ERC20 and ERC721 token implementations revert on failure. Notably, If these methods fail silently and the contract doesn't verify their return value, the contract might continue execution as if the tokens were transferred successfully, leading to incorrect balances, loss of funds, or other unexpected behaviors. Therefore, the return values of these methods should always be checked, ensuring a failed token transfer operation correctly halts the execution of the contract.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[125](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L125-L146)']
```solidity
125:     function startRedeem(uint256 shares, address beneficiary)
126:         external
127:         whenFunctionNotPaused(Constants.PAUSE_VAULT_START_REDEEM)
128:         nonReentrant
129:         returns (bytes32 withdrawalKey)
130:     {
131:         if (shares == 0) revert ZeroShares();
132:         if (beneficiary == address(0)) revert ZeroAddress();
133: 
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage();
135:         address staker = msg.sender;
136: 
137:         uint256 assets = convertToAssets(shares);
138: 
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++);
140: 
141:         state.withdrawalMap[withdrawalKey].staker = staker;
142:         state.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
143:         state.withdrawalMap[withdrawalKey].shares = shares;
144:         state.withdrawalMap[withdrawalKey].beneficiary = beneficiary;
145: 
146:         this.transferFrom(msg.sender, address(this), shares); // <= FOUND
147: 
148:         emit StartedRedeem(staker, config.operator, shares, withdrawalKey, assets);
149:     }
```


</details>

## [Low-26] Use of onlyOwner functions can be lost

### Resolution 
In Solidity, renouncing ownership of a contract essentially transfers ownership to the zero address. This is an irreversible operation and has considerable security implications. If the renounceOwnership function is used, the contract will lose the ability to perform any operations that are limited to the owner. This can be problematic if there are any bugs, flaws, or unexpected events that require owner intervention to resolve. Therefore, in some instances, it is better to disable or omit the renounceOwnership function, and instead implement a secure transferOwnership function. This way, if necessary, ownership can be transferred to a new, trusted party without losing the potential for administrative intervention.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L16-L16)']
```solidity
16: contract SlashingHandler is Initializable, Ownable, ISlashingHandler  // <= FOUND
```
['[12](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L12-L12)']
```solidity
12: contract SlashStore is Initializable, Ownable, ReentrancyGuard  // <= FOUND
```
['[17](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeNode.sol#L17-L17)']
```solidity
17: contract NativeNode is Pauser, Ownable, INativeNode, ReentrancyGuard  // <= FOUND
```


</details>

## [Low-27] Off-by-one timestamp error

### Resolution 
In Solidity, using `>=` or `<=` to compare against `block.timestamp` (alias `now`) may introduce off-by-one errors due to the fact that `block.timestamp` is only updated once per block and its value remains constant throughout the block's execution. If an operation happens at the exact second when `block.timestamp` changes, it could result in unexpected behavior. To avoid this, it's safer to use strict inequality operators (`>` or `<`). For instance, if a condition should only be met after a certain time, use `block.timestamp > time` rather than `block.timestamp >= time`. This way, potential off-by-one errors due to the exact timing of block mining are mitigated, leading to safer, more predictable contract behavior.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[228](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L228-L243)']
```solidity
228:     function startWithdrawal(address to, uint256 weiAmount)
229:         external
230:         nonReentrant
231:         nodeExists(msg.sender)
232:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_START_WITHDRAWAL)
233:         returns (bytes32 withdrawalKey)
234:     {
235:         
236:         NativeVaultLib.Storage storage self = _state();
237:         NativeVaultLib.NativeNode storage node = self.ownerToNode[msg.sender];
238:         if (weiAmount > withdrawableWei(msg.sender) - self.nodeOwnerToWithdrawAmount[msg.sender]) {
239:             revert WithdrawMoreThanMax();
240:         }
241:         self.nodeOwnerToWithdrawAmount[msg.sender] += weiAmount;
242: 
243:         if (block.timestamp >= node.lastSnapshotTimestamp + Constants.SNAPSHOT_EXPIRY) { // <= FOUND
244:             revert SnapshotExpired();
245:         }
246: 
247:         withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++);
248:         address nodeOwner = msg.sender;
249: 
250:         self.withdrawalMap[withdrawalKey].to = to;
251:         self.withdrawalMap[withdrawalKey].assets = weiAmount;
252:         self.withdrawalMap[withdrawalKey].nodeOwner = nodeOwner;
253:         self.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
254: 
255:         emit StartedWithdraw(nodeOwner, _config().operator, withdrawalKey, weiAmount, to);
256: 
257:         return withdrawalKey;
258:     }
```


</details>

## [Low-28] Events may be emitted out of order due to code not follow the best practice of check-effects-interaction

### Resolution 
The "check-effects-interaction" pattern also impacts event ordering. When a contract doesn't adhere to this pattern, events might be emitted in a sequence that doesn't reflect the actual logical flow of operations. This can cause confusion during event tracking, potentially leading to erroneous off-chain interpretations. To rectify this, always ensure that checks are performed first, state modifications come next, and interactions with external contracts or addresses are done last. This will ensure events are emitted in a logical, consistent manner, providing a clear and accurate chronological record of on-chain actions for off-chain systems and observers.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[193](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L193-L204)']
```solidity
193:     function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
194:         external
195:         onlyCore
196:         returns (uint256 transferAmount)
197:     {
198:         transferAmount = Math.min(totalAssets(), totalAssetsToSlash);
199: 
200:         
201:         SafeTransferLib.safeApproveWithRetry(asset(), slashingHandler, transferAmount);
202:         ISlashingHandler(slashingHandler).handleSlashing(IERC20(asset()), transferAmount); // <= FOUND
203: 
204:         emit Slashed(transferAmount); // <= FOUND
205:     }
```


</details>

## [Low-29] Missing zero address check in initializer

### Resolution 
Initializer functions in contracts often set important parameters or addresses. Failing to check for the zero address (0x0000000000000000000000000000000000000000) in initializers can lead to unintended behavior, as this address typically signifies an unset or default value. Transfers to or interactions with the zero address can result in permanent loss of assets or broken functionality. It's crucial to add checks using `require(targetAddress != address(0), "Address cannot be zero")` in initializers to prevent accidentally setting important state variables or parameters to this address, ensuring the system's integrity and user asset safety.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[33](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L33-L33)']
```solidity
33:     function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer {
34:         _initializeOwner(owner);
35:         Config storage config = _config();
36:         for (uint256 i = 0; i < _supportedAssets.length; i++) {
37:             config.supportedAssets[_supportedAssets[i]] = true;
38:         }
39:     }
```
['[20](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L20-L20)']
```solidity
20:     function initialize(address _owner) external initializer {
21:         _initializeOwner(_owner);
22:     }
```
['[51](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L51-L51)']
```solidity
51:     function initialize(
52:         address _owner,
53:         address _operator,
54:         address _depositToken,
55:         string memory _name,
56:         string memory _symbol,
57:         bytes memory _extraData
58:     ) external initializer {
59:         _initializeOwner(_owner);
60:         __Pauser_init();
61: 
62:         (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));
63:         VaultLib.Config storage config = _config();
64: 
65:         config.asset = _depositToken;
66:         config.name = _name;
67:         config.symbol = _symbol;
68:         config.decimals = decimalsSuccess ? result : _DEFAULT_UNDERLYING_DECIMALS;
69:         config.operator = _operator;
70:         config.extraData = _extraData;
71:     }
```
['[53](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L53-L53)']
```solidity
53:     function initialize(
54:         address _vaultImpl,
55:         address _manager,
56:         address _vetoCommittee,
57:         uint32 _hookCallGasLimit,
58:         uint32 _supportsInterfaceGasLimit,
59:         uint32 _hookGasBuffer
60:     ) external initializer {
61:         _initializeOwner(msg.sender);
62:         __Pauser_init();
63: 
64:         _grantRoles(_manager, Constants.MANAGER_ROLE);
65:         _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);
66: 
67:         _self().init(_vaultImpl, _vetoCommittee, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
68:     }
```
['[28](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeNode.sol#L28-L28)']
```solidity
28:     function initialize(address _owner, address _nodeOwner) external initializer {
29:         _initializeOwner(_owner);
30:         __Pauser_init();
31: 
32:         nodeOwner = _nodeOwner;
33:     }
```


</details>

## [Low-30] Critical functions should have a timelock

### Resolution 
Critical functions, especially those affecting protocol parameters or user funds, are potential points of failure or exploitation. To mitigate risks, incorporating a timelock on such functions can be beneficial. A timelock requires a waiting period between the time an action is initiated and when it's executed, giving stakeholders time to react, potentially vetoing malicious or erroneous changes. To implement, integrate a smart contract like OpenZeppelin's `TimelockController` or build a custom mechanism. This ensures governance decisions or administrative changes are transparent and allows for community or multi-signature interventions, enhancing protocol security and trustworthiness.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[274](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L274-L274)']
```solidity
274:     function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit) // <= FOUND
275:         external
276:         onlyRolesOrOwner(Constants.MANAGER_ROLE)
277:     
```


</details>

## [Low-31] Consider implementing two-step procedure for updating protocol addresses

### Resolution 
Implementing a two-step procedure for updating protocol addresses adds an extra layer of security. In such a system, the first step initiates the change, and the second step, after a predefined delay, confirms and finalizes it. This delay allows stakeholders or monitoring tools to observe and react to unintended or malicious changes. If an unauthorized change is detected, corrective actions can be taken before the change is finalized. To achieve this, introduce a "proposed address" state variable and a "delay period". Upon an update request, set the "proposed address". After the delay, if not contested, the main protocol address can be updated.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[173](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L173-L173)']
```solidity
173:     function changeStandardImplementation(address newVaultImpl) external onlyOwner { // <= FOUND
174:         if (newVaultImpl == address(0)) revert ZeroAddress();
175:         if (newVaultImpl == Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG) revert ReservedAddress();
176:         _self().vaultImpl = newVaultImpl;
177:         emit UpgradedAllVaults(newVaultImpl);
178:     }
```
['[183](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L183-L183)']
```solidity
183:     function changeImplementationForVault(address vault, address newVaultImpl) external onlyOwner { // <= FOUND
184:         CoreLib.Storage storage self = _self();
185:         if (!self.isVaultImplAllowlisted(newVaultImpl)) revert VaultImplNotAllowlisted();
186:         
187:         
188:         if (self.vaultToImplMap[vault] == address(0)) revert VaultNotAChildVault();
189: 
190:         self.vaultToImplMap[vault] = newVaultImpl;
191:         emit UpgradedVault(newVaultImpl, vault);
192:     }
```
['[83](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L83-L83)']
```solidity
83:     function changeNodeImplementation(address newNodeImplementation) // <= FOUND
84:         external
85:         onlyOwnerOrRoles(Constants.MANAGER_ROLE)
86:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_NODE_IMPLEMENTATION)
87:     {
88:         if (newNodeImplementation == address(0)) revert ZeroAddress();
89: 
90:         _state().nodeImpl = newNodeImplementation;
91:         emit UpgradedAllNodes(newNodeImplementation);
92:     }
```


</details>

## [Low-32] SafeTransferLib does not ensure that the token contract exists

### Resolution 
SafeTransferLib as similarly named function as OpenZepelins SafeERC20 module however it's functions such as safeTransferFrom don't check if the contract exists which can result in silent failures when performing such operations. As such it is recommended to perform a contract existence check beforehand. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[5](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L5-L5)']
```solidity
5: import {SafeTransferLib} from "solady/src/utils/SafeTransferLib.sol"; // <= FOUND
```


</details>

## [Low-33] Avoid mutating function parameters

### Resolution 
Function parameters in Solidity are passed by value, meaning they are essentially local copies. Mutating them can lead to confusion and errors because the changes don't persist outside the function. By keeping function parameters immutable, you ensure clarity in code behavior, preventing unintended side-effects. If you need to modify a value based on a parameter, use a local variable inside the function, leaving the original parameter unaltered. By adhering to this practice, you maintain a clear distinction between input data and the internal processing logic, improving code readability and reducing the potential for bugs.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[299](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L299-L312)']
```solidity
299:     function slashAssets(uint256 totalAssetsToSlash, address slashingHandler)
300:         external
301:         onlyOwner
302:         nonReentrant
303:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_SLASHER)
304:         returns (uint256 transferAmount)
305:     {
306:         NativeVaultLib.Storage storage self = _state();
307: 
308:         if (slashingHandler != self.slashStore) revert NotSlashStore();
309: 
310:         
311:         if (totalAssetsToSlash > self.totalAssets) {
312:             totalAssetsToSlash = self.totalAssets; // <= FOUND
313:         }
314: 
315:         self.totalAssets -= totalAssetsToSlash;
316:         emit Slashed(totalAssetsToSlash);
317:         return totalAssetsToSlash;
318:     }
```
['[118](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L118-L129)']
```solidity
118:     function deployVaults(
119:         Storage storage self,
120:         address operator,
121:         address implementation,
122:         VaultLib.Config[] calldata vaultConfigs
123:     ) external returns (IKarakBaseVault[] memory) {
124:         validateVaultConfigs(self, vaultConfigs, implementation);
125:         IKarakBaseVault[] memory vaults = new IKarakBaseVault[](vaultConfigs.length);
126: 
127:         if (implementation == address(0)) {
128:             
129:             implementation = Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG; // <= FOUND
130:         }
131: 
132:         for (uint256 i = 0; i < vaultConfigs.length; i++) {
133:             IKarakBaseVault vault = createVault(
134:                 self,
135:                 operator,
136:                 vaultConfigs[i].asset,
137:                 vaultConfigs[i].name,
138:                 vaultConfigs[i].symbol,
139:                 vaultConfigs[i].extraData,
140:                 implementation
141:             );
142:             vaults[i] = vault;
143:             self.operatorState[operator].addVault(vault);
144:             emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);
145:         }
146:         return vaults;
147:     }
```


</details>

## [Low-34] Prefer skip over revert model in iteration

### Resolution 
It is preferable to skip operations on an array index when a condition is not met rather than reverting the whole transaction as reverting can introduce the possiblity of malicous actors purposefully introducing array objects which fail conditional checks within for/while loops so group operations fail. As such it is recommended to simply skip such array indices over reverting unless there is a valid security or logic reason behind not doing so.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[71](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L71-L72)']
```solidity
71:        for (uint256 i = 0; i < assets.length; i++) { // <= FOUND
72:             if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress(); // <= FOUND
73:             self.assetSlashingHandlers[assets[i]] = slashingHandlers[i];
74:         }
```
['[71](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L71-L72)']
```solidity
71:         for (uint256 i = 0; i < assets.length; i++) { // <= FOUND
72:             if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress(); // <= FOUND
73:             self.assetSlashingHandlers[assets[i]] = slashingHandlers[i];
74:         }
```
['[50](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L50-L55)']
```solidity
50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) { // <= FOUND
51:             if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {
52:                 revert VaultNotStakedToDSS();
53:             }
54:             if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad(); // <= FOUND
55:             if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached(); // <= FOUND
56:         }
```
['[50](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L50-L55)']
```solidity
50:         for (uint256 i = 0; i < slashingRequest.vaults.length; i++) { // <= FOUND
51:             if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {
52:                 revert VaultNotStakedToDSS();
53:             }
54:             if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad(); // <= FOUND
55:             if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached(); // <= FOUND
56:         }
```
['[84](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L84-L85)']
```solidity
84:         for (uint256 i = 0; i < vaultConfigs.length; i++) { // <= FOUND
85:             if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted(); // <= FOUND
86:         }
```


</details>

## [Low-35] Nonce variables should be uint256

### Resolution 
Using `uint256` for nonce variables is a best practice in Solidity for several reasons. Nonce, typically used for ensuring the uniqueness of transactions or for generating pseudorandom numbers, can potentially be incremented many times. Choosing `uint256` ensures that the nonce has a sufficiently large range to avoid overflow, even under heavy usage or over an extended period. An overflow in a nonce variable can lead to security vulnerabilities, such as replay attacks or other unexpected behaviors. By using `uint256`, developers can mitigate these risks, ensuring more robust and secure smart contract operations, especially in systems with high transaction throughput or long-term operational expectancy.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[33](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L33-L33)']
```solidity
33:         uint48 nonce; // <= FOUND
```
['[34](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L34-L34)']
```solidity
34:         uint96 nonce; // <= FOUND
```


</details>

## [Low-36] Division in comparison

### Resolution 
To ensure accuracy in comparisons within programming, especially when dealing with integers, it's often more efficient to use multiplication rather than division. This approach stems from the fact that division operations are generally slower and more complex than multiplication. And in the context of solidity they can cause precision errors.

Suppose you want to compare if a/b is greater than c/d (where a, b, c, and d are integers). Instead of performing division, which is prone to precision errors, you can cross-multiply to avoid division. The comparison a/b > c/d is equivalent to a*d > b*c. This way, you only use multiplication, which is faster and avoids potential inaccuracies or complexities associated with division.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[55](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L55-L55)']
```solidity
55:         if (gasleft() < (hookCallGasLimit * 64 / 63 + hookGasBuffer)) revert NotEnoughGas(); // <= FOUND
```
['[87](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L87-L87)']
```solidity
87:         if (gasleft() < (supportsInterfaceGasLimit * 64 / 63 + hookGasBuffer)) { // <= FOUND
```


</details>

## [Low-37] Library has public/external functions

### Resolution 
Libraries in Solidity are meant to be static collections of functions. They are deployed once and their code is reused by contracts through DELEGATECALL, which executes the library's code in the context of the calling contract. Public or external functions in libraries can be misleading because libraries are not supposed to maintain state or have external interactions in the way contracts do. Designing libraries with these kinds of functions goes against their intended purpose and can lead to confusion or misuse. For state management or external interactions, using contracts instead of libraries is more appropriate. Libraries should focus on utility functions that can operate on the data passed to them without side effects, enhancing code reuse and gas efficiency.

Num of instances: 6

### Findings 


<details><summary>Click to show findings</summary>

['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/utils/CommonUtils.sol#L4-L48)']
```solidity
4: library CommonUtils { // <= FOUND
5:     
7:     function sortArr(address[] memory arr) private pure {
8:         if (arr.length == 0) return;
9:         sort(arr, 0, arr.length - 1);
10:     }
11: 
12:     function sort(address[] memory arr, uint256 left, uint256 right) private pure {
13:         if (left >= right) return;
14:         uint256 lastUnsortedInd = left;
15:         uint256 pivot = right;
16:         for (uint256 i = left; i < right; i++) {
17:             if (arr[i] <= arr[pivot]) {
18:                 if (i != lastUnsortedInd) swap(arr, i, lastUnsortedInd);
19:                 lastUnsortedInd++;
20:             }
21:         }
22:         swap(arr, pivot, lastUnsortedInd);
23:         if (lastUnsortedInd > left) {
24:             sort(arr, left, lastUnsortedInd - 1);
25:         }
26:         sort(arr, lastUnsortedInd, right);
27:     }
28: 
29:     function swap(address[] memory arr, uint256 left, uint256 right) private pure {
30:         address temp = arr[left];
31:         arr[left] = arr[right];
32:         arr[right] = temp;
33:     }
34: 
39:     function hasDuplicates(address[] memory arr) external pure returns (bool) { // <= FOUND
40:         sortArr(arr);
41:         if (arr.length == 0) return false;
42:         for (uint256 i = 0; i < arr.length - 1; i++) {
43:             if (arr[i] == arr[i + 1]) return true;
44:         }
45:         return false;
46:     }
47: 
48:     function isSmartContract(address addr) external view returns (bool) { // <= FOUND
49:         uint256 size;
50:         assembly {
51:             size := extcodesize(addr)
52:         }
53:         return size > 0;
54:     }
55: }
```
['[14](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L14-L173)']
```solidity
14: library Operator { // <= FOUND
15:     using EnumerableSet for EnumerableSet.AddressSet;
16:     using CoreLib for CoreLib.Storage;
17: 
18:     struct State {
19:         EnumerableSet.AddressSet vaults;
20:         EnumerableSet.AddressSet dssMap;
21:         mapping(IDSS dss => EnumerableSet.AddressSet vaultStakeInDss) vaultStakedInDssMap;
22:         mapping(IDSS dss => uint256 timestamp) nextSlashableTimestamp; 
23:         mapping(address vault => bytes32 updateHash) pendingStakeUpdates; 
24:     }
25: 
26:     struct StakeUpdateRequest {
27:         address vault;
28:         IDSS dss;
29:         bool toStake; 
30:     }
31: 
32:     struct QueuedStakeUpdate {
33:         uint48 nonce;
34:         uint48 startTimestamp;
35:         address operator;
36:         StakeUpdateRequest updateRequest;
37:     }
38: 
39:     function getVaults(State storage operatorState) internal view returns (address[] memory) {
40:         return operatorState.vaults.values();
41:     }
42: 
43:     function addVault(State storage operatorState, IKarakBaseVault vault) internal {
44:         if (vault == IKarakBaseVault(address(0))) revert ZeroAddress();
45:         if (operatorState.vaults.length() == Constants.MAX_VAULTS_PER_OPERATOR) revert MaxVaultCapacityReached();
46:         operatorState.vaults.add(address(vault));
47:     }
48: 
49:     function calculateRoot(QueuedStakeUpdate memory newStake) internal pure returns (bytes32) {
50:         return keccak256(abi.encode(newStake));
51:     }
52: 
53:     function validateStakeUpdateRequest(State storage operatorState, StakeUpdateRequest memory stakeUpdate)
54:         internal
55:         view
56:     {
57:         if (operatorState.pendingStakeUpdates[stakeUpdate.vault] != bytes32(0)) revert PendingStakeUpdateRequest();
58:         if (!operatorState.vaults.contains(stakeUpdate.vault)) revert VaultNotAChildVault();
59:     }
60: 
61:     function requestUpdateVaultStakeInDSS( // <= FOUND
62:         CoreLib.Storage storage self,
63:         StakeUpdateRequest memory requestStakeUpdate,
64:         uint128 nonce,
65:         address operator
66:     ) external returns (QueuedStakeUpdate memory queuedStake) {
67:         State storage operatorState = self.operatorState[operator];
68:         validateStakeUpdateRequest(operatorState, requestStakeUpdate);
69:         queuedStake = QueuedStakeUpdate({
70:             nonce: uint48(nonce),
71:             startTimestamp: uint48(block.timestamp),
72:             operator: operator,
73:             updateRequest: requestStakeUpdate
74:         });
75:         operatorState.pendingStakeUpdates[requestStakeUpdate.vault] = calculateRoot(queuedStake);
76:         IDSS dss = requestStakeUpdate.dss;
77: 
78:         HookLib.callHookIfInterfaceImplemented({
79:             dss: dss,
80:             data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate),
81:             interfaceId: dss.requestUpdateStakeHook.selector,
82:             ignoreFailure: !requestStakeUpdate.toStake,
83:             hookCallGasLimit: self.hookCallGasLimit,
84:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
85:             hookGasBuffer: self.hookGasBuffer
86:         });
87:     }
88: 
89:     function validateQueuedStakeUpdate(State storage operatorState, QueuedStakeUpdate memory queuedStakeUpdate)
90:         internal
91:         view
92:     {
93:         if (queuedStakeUpdate.startTimestamp + Constants.MIN_STAKE_UPDATE_DELAY > block.timestamp) {
94:             revert OperatorStakeUpdateDelayNotPassed();
95:         }
96:         if (
97:             calculateRoot(queuedStakeUpdate) != operatorState.pendingStakeUpdates[queuedStakeUpdate.updateRequest.vault]
98:         ) {
99:             revert InvalidQueuedStakeUpdateInput();
100:         }
101:     }
102: 
103:     function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal {
104:         if (toStake) {
105:             operatorState.vaultStakedInDssMap[dss].add(vault);
106:         } else {
107:             operatorState.vaultStakedInDssMap[dss].remove(vault);
108:         }
109:     }
110: 
111:     function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate) // <= FOUND
112:         external
113:     {
114:         State storage operatorState = self.operatorState[queuedStakeUpdate.operator];
115:         validateQueuedStakeUpdate(operatorState, queuedStakeUpdate);
116:         updateVaultStakeInDSS(
117:             operatorState,
118:             queuedStakeUpdate.updateRequest.vault,
119:             queuedStakeUpdate.updateRequest.dss,
120:             queuedStakeUpdate.updateRequest.toStake
121:         );
122:         delete operatorState.pendingStakeUpdates[queuedStakeUpdate.updateRequest.vault];
123:         IDSS dss = queuedStakeUpdate.updateRequest.dss;
124:         HookLib.callHookIfInterfaceImplemented({
125:             dss: dss,
126:             data: abi.encodeWithSelector(dss.finishUpdateStakeHook.selector, msg.sender),
127:             interfaceId: dss.finishUpdateStakeHook.selector,
128:             ignoreFailure: true,
129:             hookCallGasLimit: self.hookCallGasLimit,
130:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
131:             hookGasBuffer: self.hookGasBuffer
132:         });
133:     }
134: 
135:     function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss)
136:         internal
137:         view
138:         returns (bool)
139:     {
140:         return self.operatorState[operator].dssMap.contains(address(dss));
141:     }
142: 
143:     function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view {
144:         if (!self.isDSSRegistered(dss)) revert DSSNotRegistered();
145:         if (!isOperatorRegisteredToDSS(self, operator, dss)) {
146:             revert OperatorNotValidatingForDSS();
147:         }
148:     }
149: 
150:     function registerOperatorToDSS( // <= FOUND
151:         CoreLib.Storage storage self,
152:         IDSS dss,
153:         address operator,
154:         bytes memory registrationHookData
155:     ) external {
156:         State storage operatorState = self.operatorState[operator];
157:         if (isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorAlreadyRegisteredToDSS();
158:         if (operatorState.dssMap.length() == Constants.MAX_DSS_PER_OPERATOR) revert MaxDSSCapacityReached();
159: 
160:         operatorState.dssMap.add(address(dss));
161: 
162:         HookLib.callHookIfInterfaceImplemented({
163:             dss: dss,
164:             data: abi.encodeWithSelector(dss.registrationHook.selector, operator, registrationHookData),
165:             interfaceId: dss.registrationHook.selector,
166:             ignoreFailure: false,
167:             hookCallGasLimit: self.hookCallGasLimit,
168:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
169:             hookGasBuffer: self.hookGasBuffer
170:         });
171:     }
172: 
173:     function getVaultsStakedToDSS(State storage operatorState, IDSS dss) // <= FOUND
174:         public
175:         view
176:         returns (address[] memory vaults)
177:     {
178:         vaults = operatorState.vaultStakedInDssMap[dss].values();
179:     }
180: 
181:     function unregisterOperatorFromDSS( // <= FOUND
182:         CoreLib.Storage storage self,
183:         IDSS dss,
184:         address operator,
185:         bytes memory unregistrationHookData
186:     ) external {
187:         State storage operatorState = self.operatorState[operator];
188:         
189:         address[] memory vaults = getVaultsStakedToDSS(operatorState, dss);
190:         if (vaults.length != 0) revert AllVaultsNotUnstakedFromDSS();
191:         if (!isOperatorRegisteredToDSS(self, operator, dss)) revert OperatorNotValidatingForDSS();
192: 
193:         self.operatorState[operator].dssMap.remove(address(dss));
194:         HookLib.callHookIfInterfaceImplemented({
195:             dss: dss,
196:             data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData),
197:             interfaceId: dss.unregistrationHook.selector,
198:             ignoreFailure: true, 
199:             hookCallGasLimit: self.hookCallGasLimit,
200:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
201:             hookGasBuffer: self.hookGasBuffer
202:         });
203:     }
204: 
209:     function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator)
210:         internal
211:         view
212:         returns (address[] memory dssAddresses)
213:     {
214:         dssAddresses = self.operatorState[operator].dssMap.values();
215:     }
216: 
217:     function isVaultStakeToDSS(State storage operatorState, IDSS dss, address vault) internal view returns (bool) {
218:         return operatorState.vaultStakedInDssMap[dss].contains(vault);
219:     }
220: 
224:     function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault)
225:         external
226:         view
227:         returns (uint256 count)
228:     {
229:         address operator = vault.vaultConfig().operator;
230:         address[] memory dssAddresses = getDSSsOperatorIsRegisteredTo(self, operator);
231:         State storage operatorState = self.operatorState[operator];
232:         for (uint256 i = 0; i < dssAddresses.length; i++) {
233:             if (isVaultStakeToDSS(operatorState, IDSS(dssAddresses[i]), address(vault))) count++;
234:         }
235:     }
236: }
```
['[7](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L7-L141)']
```solidity
7: library BeaconProofs { // <= FOUND
8:     
9:     uint256 internal constant BEACON_STATE_HEIGHT = 5;
10:     uint256 internal constant BEACON_STATE_ROOT_IDX = 3;
11:     uint256 internal constant BEACON_BLOCK_HEADER_HEIGHT = 3;
12: 
14:     uint256 internal constant PUBKEY_IDX = 0;
15:     uint256 internal constant NUM_FIELDS = 8;
16:     uint256 internal constant BALANCE_IDX = 2;
17:     uint256 internal constant CONTAINER_IDX = 11;
18:     uint256 internal constant EXIT_EPOCH_IDX = 6;
19:     uint256 internal constant VALIDATOR_HEIGHT = 40;
20:     uint256 internal constant WITHDRAWAL_CREDENTIALS_IDX = 1;
21: 
23:     uint256 internal constant BALANCE_CONTAINER_IDX = 12;
24:     uint256 internal constant BALANCE_HEIGHT = 38;
25: 
26:     struct BeaconStateRootProof {
27:         uint64 timestamp;
28:         bytes32 beaconStateRoot;
29:         bytes proof;
30:     }
31: 
32:     struct ValidatorProof {
33:         uint40 validatorIndex;
34:         bytes32 validatorRoot;
35:         bytes proof;
36:     }
37: 
38:     struct ValidatorFieldsProof {
39:         ValidatorProof validatorProof;
40:         bytes32[] validatorFields;
41:     }
42: 
43:     struct BalanceContainer {
44:         bytes32 containerRoot;
45:         bytes proof;
46:     }
47: 
48:     struct BalanceProof {
49:         bytes32 pubkeyHash;
50:         bytes32 balanceRoot;
51:         bytes proof;
52:     }
53: 
54:     function fromLittleEndianUint64(bytes32 lenum) internal pure returns (uint64 n) {
55:         n = uint64(uint256(lenum >> 192));
56:         return (n >> 56) | ((0x00FF000000000000 & n) >> 40) | ((0x0000FF0000000000 & n) >> 24)
57:             | ((0x000000FF00000000 & n) >> 8) | ((0x00000000FF000000 & n) << 8) | ((0x0000000000FF0000 & n) << 24)
58:             | ((0x000000000000FF00 & n) << 40) | ((0x00000000000000FF & n) << 56);
59:     }
60: 
61:     function validateBeaconStateRootProof(bytes32 beaconBlockRoot, BeaconStateRootProof calldata beaconStateRootProof)
62:         internal
63:         view
64:     {
65:         if (beaconStateRootProof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT)) revert InvalidBeaconStateProof();
66:         if (
67:             !Merkle.verifyInclusionSha256(
68:                 beaconStateRootProof.proof, beaconBlockRoot, beaconStateRootProof.beaconStateRoot, BEACON_STATE_ROOT_IDX
69:             )
70:         ) revert InvalidBeaconStateProof();
71:     }
72: 
73:     function validateValidatorProof(
74:         uint40 validatorIndex,
75:         bytes32[] calldata validatorFields,
76:         bytes calldata validatorProof,
77:         bytes32 beaconStateRoot
78:     ) internal view {
79:         if (validatorFields.length != NUM_FIELDS) revert InvalidValidatorFieldsLength();
80: 
81:         bytes32 validatorRoot = Merkle.merkleizeSha256(validatorFields);
82: 
83:         
84:         
85:         uint256 index = (CONTAINER_IDX << (VALIDATOR_HEIGHT + 1)) | uint256(validatorIndex);
86: 
87:         
88:         if (validatorProof.length != 32 * ((VALIDATOR_HEIGHT + 1) + BEACON_STATE_HEIGHT)) {
89:             revert InvalidValidatorFieldsProofLength();
90:         }
91:         
92:         if (!Merkle.verifyInclusionSha256(validatorProof, beaconStateRoot, validatorRoot, index)) {
93:             revert InvalidValidatorFieldsProofInclusion();
94:         }
95:     }
96: 
97:     function validateBalanceContainer(bytes32 beaconBlockRoot, BalanceContainer calldata proof) internal view {
98:         if (proof.proof.length != 32 * (BEACON_BLOCK_HEADER_HEIGHT + BEACON_STATE_HEIGHT)) {
99:             revert InvalidBalanceRootProof();
100:         }
101: 
102:         uint256 index = (BEACON_STATE_ROOT_IDX << (BEACON_STATE_HEIGHT)) | BALANCE_CONTAINER_IDX;
103: 
104:         if (
105:             !Merkle.verifyInclusionSha256({
106:                 proof: proof.proof,
107:                 root: beaconBlockRoot,
108:                 leaf: proof.containerRoot,
109:                 index: index
110:             })
111:         ) revert InvalidBalanceRootProof();
112:     }
113: 
114:     function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof)
115:         internal
116:         view
117:         returns (uint256 validatorBalanceWei)
118:     {
119:         if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();
120: 
121:         uint256 balanceIndex = uint256(validatorIndex / 4);
122: 
123:         if (
124:             !Merkle.verifyInclusionSha256({
125:                 proof: proof.proof,
126:                 root: balanceRoot,
127:                 leaf: proof.balanceRoot,
128:                 index: balanceIndex
129:             })
130:         ) revert InvalidBalanceProof();
131: 
132:         
133:         uint256 bitShiftAmount = (validatorIndex % 4) * 64;
134:         return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;
135:     }
136: 
137:     function getEffectiveBalanceWei(bytes32[] memory validatorFields) internal pure returns (uint256) {
138:         return uint256(fromLittleEndianUint64(validatorFields[BALANCE_IDX])) * 1 gwei;
139:     }
140: 
141:     function getPubkeyHash(bytes32[] calldata validatorFields) external pure returns (bytes32) { // <= FOUND
142:         return validatorFields[PUBKEY_IDX];
143:     }
144: 
145:     function getExitEpoch(bytes32[] memory validatorFields) internal pure returns (uint64) {
146:         return fromLittleEndianUint64(validatorFields[EXIT_EPOCH_IDX]);
147:     }
148: 
149:     function getWithdrawalCredentials(bytes32[] memory validatorFields) internal pure returns (bytes32) {
150:         return validatorFields[WITHDRAWAL_CREDENTIALS_IDX];
151:     }
152: }
```
['[13](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreStorageSlots.sol#L13-L27)']
```solidity
13: library CoreStorageSlots { // <= FOUND
14:     
15:     function operatorStateMappingSlot() internal pure returns (bytes32) {
16:         return bytes32(CORE_STORAGE_SLOT + OPERATOR_STATE_MAPPING_OFFSET);
17:     }
18: 
19:     function operatorStateSlot(address operator) internal pure returns (bytes32) {
20:         return keccak256(abi.encode(operator, operatorStateMappingSlot()));
21:     }
22: 
23:     function pendingStakeUpdateMappingSlot(address operator) internal pure returns (bytes32) {
24:         return bytes32(uint256(operatorStateSlot(operator)) + PENDING_STAKE_UPDATE_MAPPING_OFFSET);
25:     }
26: 
27:     function vaultPendingStakeUpdateSlot(address operator, address vault) public pure returns (bytes32) { // <= FOUND
28:         return keccak256(abi.encode(vault, pendingStakeUpdateMappingSlot(operator)));
29:     }
30: }
```
['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L16-L77)']
```solidity
16: library CoreLib { // <= FOUND
17:     using Operator for Operator.State;
18: 
20:     struct Storage {
21:         
22:         mapping(address operator => Operator.State) operatorState;
23:         
24:         mapping(address vault => address implementation) vaultToImplMap;
25:         mapping(address implementation => bool) allowlistedVaultImpl;
26:         
27:         mapping(address asset => address slashingHandler) assetSlashingHandlers;
28:         
29:         mapping(bytes32 slashRoot => bool) slashingRequests;
30:         mapping(IDSS dss => uint256 slashablePercentageWad) dssMaxSlashablePercentageWad;
31:         address vaultImpl;
32:         uint96 vaultNonce;
33:         address vetoCommittee;
34:         uint96 nonce;
35:         uint32 hookCallGasLimit;
36:         uint32 supportsInterfaceGasLimit;
37:         uint32 hookGasBuffer;
38:     }
39: 
40:     function init(
41:         Storage storage self,
42:         address _vaultImpl,
43:         address _vetoCommittee,
44:         uint32 _hookCallGasLimit,
45:         uint32 _supportsInterfaceGasLimit,
46:         uint32 _hookGasBuffer
47:     ) internal {
48:         if (_vaultImpl == address(0) || _vetoCommittee == address(0)) {
49:             revert ZeroAddress();
50:         }
51:         self.vaultImpl = _vaultImpl;
52:         self.vetoCommittee = _vetoCommittee;
53:         updateGasValues(self, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
54:     }
55: 
56:     function updateGasValues(
57:         Storage storage self,
58:         uint32 _hookCallGasLimit,
59:         uint32 _supportsInterfaceGasLimit,
60:         uint32 _hookGasBuffer
61:     ) internal {
62:         self.hookCallGasLimit = _hookCallGasLimit;
63:         self.hookGasBuffer = _hookGasBuffer;
64:         self.supportsInterfaceGasLimit = _supportsInterfaceGasLimit;
65:     }
66: 
67:     function allowlistAssets(Storage storage self, address[] memory assets, address[] memory slashingHandlers) // <= FOUND
68:         external
69:     {
70:         if (assets.length != slashingHandlers.length) revert LengthsDontMatch();
71:         for (uint256 i = 0; i < assets.length; i++) {
72:             if (slashingHandlers[i] == address(0) || assets[i] == address(0)) revert ZeroAddress();
73:             self.assetSlashingHandlers[assets[i]] = slashingHandlers[i];
74:         }
75:     }
76: 
77:     function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation) // <= FOUND
78:         public
79:         view
80:     {
81:         if (!(implementation == address(0) || isVaultImplAllowlisted(self, implementation))) {
82:             revert VaultImplNotAllowlisted();
83:         }
84:         for (uint256 i = 0; i < vaultConfigs.length; i++) {
85:             if (self.assetSlashingHandlers[vaultConfigs[i].asset] == address(0)) revert AssetNotAllowlisted();
86:         }
87:     }
88: 
89:     function createVault(
90:         Storage storage self,
91:         address operator,
92:         address depositToken,
93:         string memory name,
94:         string memory symbol,
95:         bytes memory extraData,
96:         address implementation
97:     ) internal returns (IKarakBaseVault) {
98:         
99:         bytes32 salt = keccak256(abi.encodePacked(operator, depositToken, self.vaultNonce++));
100: 
101:         address expectedNewVaultAddr =
102:             LibClone.predictDeterministicAddressERC1967BeaconProxy(address(this), salt, address(this));
103: 
104:         self.vaultToImplMap[address(expectedNewVaultAddr)] = implementation;
105: 
106:         IKarakBaseVault vault = cloneVault(salt);
107:         vault.initialize(address(this), operator, depositToken, name, symbol, extraData);
108: 
109:         
110:         if (expectedNewVaultAddr != address(vault)) {
111:             revert VaultCreationFailedAddrMismatch(expectedNewVaultAddr, address(vault));
112:         }
113: 
114:         emit NewVault(address(vault), implementation);
115:         return vault;
116:     }
117: 
118:     function deployVaults( // <= FOUND
119:         Storage storage self,
120:         address operator,
121:         address implementation,
122:         VaultLib.Config[] calldata vaultConfigs
123:     ) external returns (IKarakBaseVault[] memory) {
124:         validateVaultConfigs(self, vaultConfigs, implementation);
125:         IKarakBaseVault[] memory vaults = new IKarakBaseVault[](vaultConfigs.length);
126: 
127:         if (implementation == address(0)) {
128:             
129:             implementation = Constants.DEFAULT_VAULT_IMPLEMENTATION_FLAG;
130:         }
131: 
132:         for (uint256 i = 0; i < vaultConfigs.length; i++) {
133:             IKarakBaseVault vault = createVault(
134:                 self,
135:                 operator,
136:                 vaultConfigs[i].asset,
137:                 vaultConfigs[i].name,
138:                 vaultConfigs[i].symbol,
139:                 vaultConfigs[i].extraData,
140:                 implementation
141:             );
142:             vaults[i] = vault;
143:             self.operatorState[operator].addVault(vault);
144:             emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);
145:         }
146:         return vaults;
147:     }
148: 
149:     function cloneVault(bytes32 salt) internal returns (IKarakBaseVault) {
150:         return IKarakBaseVault(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt)));
151:     }
152: 
153:     function allowlistVaultImpl(Storage storage self, address implementation) internal {
154:         self.allowlistedVaultImpl[implementation] = true;
155:     }
156: 
157:     function isVaultImplAllowlisted(Storage storage self, address implementation) internal view returns (bool) {
158:         return self.allowlistedVaultImpl[implementation] || implementation == self.vaultImpl;
159:     }
160: 
161:     function isDSSRegistered(Storage storage self, IDSS dss) internal view returns (bool) {
162:         return self.dssMaxSlashablePercentageWad[dss] != 0;
163:     }
164: }
```
['[18](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L18-L174)']
```solidity
18: library SlasherLib { // <= FOUND
19:     using Operator for Operator.State;
20:     using EnumerableMap for EnumerableMap.AddressToUintMap;
21:     using CommonUtils for address[];
22: 
23:     struct SlashRequest {
24:         address operator;
25:         uint96[] slashPercentagesWad;
26:         address[] vaults;
27:     }
28: 
29:     struct QueuedSlashing {
30:         IDSS dss;
31:         uint96 timestamp;
32:         address operator;
33:         address[] vaults;
34:         uint256[] earmarkedStakes;
35:         uint256 nonce;
36:     }
37: 
38:     function calculateRoot(QueuedSlashing memory queuedSlashing) internal pure returns (bytes32 root) {
39:         root = keccak256(abi.encode(queuedSlashing));
40:     }
41: 
42:     function validateVaultsAndSlashPercentages(
43:         CoreLib.Storage storage self,
44:         SlashRequest memory slashingRequest,
45:         IDSS dss
46:     ) internal view {
47:         if (slashingRequest.vaults.hasDuplicates()) revert DuplicateSlashingVaults();
48: 
49:         uint256 maxSlashPercentageWad = getDSSMaxSlashablePercentageWad(self, dss);
50:         for (uint256 i = 0; i < slashingRequest.vaults.length; i++) {
51:             if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {
52:                 revert VaultNotStakedToDSS();
53:             }
54:             if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad();
55:             if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached();
56:         }
57:     }
58: 
59:     function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss)
60:         internal
61:         view
62:     {
63:         
64:         if (block.timestamp < self.operatorState[slashingRequest.operator].nextSlashableTimestamp[dss]) {
65:             revert SlashingCooldownNotPassed();
66:         }
67:         
68:         if (slashingRequest.slashPercentagesWad.length != slashingRequest.vaults.length) revert LengthsDontMatch();
69:         
70:         if (slashingRequest.vaults.length > Constants.MAX_SLASHABLE_VAULTS_PER_REQUEST) {
71:             revert MaxSlashableVaultsPerRequestBreached();
72:         }
73:         
74:         if (slashingRequest.vaults.length == 0) revert EmptyArray();
75:         
76:         validateVaultsAndSlashPercentages(self, slashingRequest, dss);
77:     }
78: 
79:     function fetchEarmarkedStakes(SlashRequest memory slashingMetadata)
80:         internal
81:         view
82:         returns (uint256[] memory earmarkedStakes)
83:     {
84:         earmarkedStakes = new uint256[](slashingMetadata.vaults.length);
85:         for (uint256 i = 0; i < slashingMetadata.vaults.length; ++i) {
86:             earmarkedStakes[i] = Math.mulDiv(
87:                 slashingMetadata.slashPercentagesWad[i],
88:                 IKarakBaseVault(slashingMetadata.vaults[i]).totalAssets(),
89:                 Constants.MAX_SLASHING_PERCENT_WAD
90:             );
91:         }
92:     }
93: 
94:     function requestSlashing( // <= FOUND
95:         CoreLib.Storage storage self,
96:         IDSS dss,
97:         SlashRequest memory slashingMetadata,
98:         uint256 nonce
99:     ) external returns (QueuedSlashing memory queuedSlashing) {
100:         validateRequestSlashingParams(self, slashingMetadata, dss);
101:         uint256[] memory earmarkedStakes = fetchEarmarkedStakes(slashingMetadata);
102:         queuedSlashing = QueuedSlashing({
103:             dss: dss,
104:             timestamp: uint96(block.timestamp),
105:             operator: slashingMetadata.operator,
106:             vaults: slashingMetadata.vaults,
107:             earmarkedStakes: earmarkedStakes,
108:             nonce: nonce
109:         });
110:         self.slashingRequests[calculateRoot(queuedSlashing)] = true;
111:         self.operatorState[slashingMetadata.operator].nextSlashableTimestamp[dss] =
112:             block.timestamp + Constants.SLASHING_COOLDOWN;
113:         HookLib.callHookIfInterfaceImplemented({
114:             dss: dss,
115:             data: abi.encodeWithSelector(
116:                 dss.requestSlashingHook.selector, slashingMetadata.operator, slashingMetadata.slashPercentagesWad
117:             ),
118:             interfaceId: dss.requestSlashingHook.selector,
119:             ignoreFailure: true,
120:             hookCallGasLimit: self.hookCallGasLimit,
121:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
122:             hookGasBuffer: self.hookGasBuffer
123:         });
124:     }
125: 
126:     function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external { // <= FOUND
127:         bytes32 slashRoot = calculateRoot(queuedSlashing);
128:         if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();
129:         if (queuedSlashing.timestamp + Constants.SLASHING_VETO_WINDOW > block.timestamp) {
130:             revert MinSlashingDelayNotPassed();
131:         }
132:         delete self.slashingRequests[slashRoot];
133: 
134:         for (uint256 i = 0; i < queuedSlashing.vaults.length; i++) {
135:             IKarakBaseVault(queuedSlashing.vaults[i]).slashAssets(
136:                 queuedSlashing.earmarkedStakes[i],
137:                 self.assetSlashingHandlers[IKarakBaseVault(queuedSlashing.vaults[i]).asset()]
138:             );
139:         }
140:         IDSS dss = queuedSlashing.dss;
141: 
142:         HookLib.callHookIfInterfaceImplemented({
143:             dss: dss,
144:             data: abi.encodeWithSelector(dss.finishSlashingHook.selector, queuedSlashing.operator),
145:             interfaceId: dss.finishSlashingHook.selector,
146:             ignoreFailure: true,
147:             hookCallGasLimit: self.hookCallGasLimit,
148:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
149:             hookGasBuffer: self.hookGasBuffer
150:         });
151:     }
152: 
153:     function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external { // <= FOUND
154:         bytes32 slashRoot = calculateRoot(queuedSlashing);
155:         if (!self.slashingRequests[slashRoot]) revert InvalidSlashingParams();
156:         delete self.slashingRequests[slashRoot];
157:         IDSS dss = queuedSlashing.dss;
158: 
159:         HookLib.callHookIfInterfaceImplemented({
160:             dss: dss,
161:             data: abi.encodeWithSelector(dss.cancelSlashingHook.selector, queuedSlashing.operator),
162:             interfaceId: dss.cancelSlashingHook.selector,
163:             ignoreFailure: true,
164:             hookCallGasLimit: self.hookCallGasLimit,
165:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
166:             hookGasBuffer: self.hookGasBuffer
167:         });
168:     }
169: 
170:     function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) { // <= FOUND
171:         return self.dssMaxSlashablePercentageWad[dss];
172:     }
173: 
174:     function setDSSMaxSlashablePercentageWad( // <= FOUND
175:         CoreLib.Storage storage self,
176:         IDSS dss,
177:         uint256 dssMaxSlashablePercentageWad
178:     ) public {
179:         uint256 currentSlashablePercentageWad = self.dssMaxSlashablePercentageWad[dss];
180:         if (currentSlashablePercentageWad != 0) revert DSSAlreadyRegistered();
181:         if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();
182:         if (dssMaxSlashablePercentageWad > Constants.MAX_SLASHING_PERCENT_WAD) revert MaxSlashPercentageWadBreached();
183:         self.dssMaxSlashablePercentageWad[dss] = dssMaxSlashablePercentageWad;
184:     }
185: }
```


</details>

## [Low-38] Constructor doesn't set initial owner

### Resolution 
In recent versions of the OpenZeppelin Ownable library, ownership has to be initialized within the constructor by adding Ownable(<owner_address>) to the constructor declaration. This is only a LOW issue as in older versions of OZ lib this will not cause an issue as the Ownable constructor automatically sets the owner to msg.sender.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L26-L26)']
```solidity
26:     constructor() {
27:         _disableInitializers();
28:     }
```
['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L26-L26)']
```solidity
26:     constructor() {
27:         _disableInitializers();
28:     }
```
['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L26-L26)']
```solidity
26:     constructor() {
27:         _disableInitializers();
28:     }
```
['[14](https://github.com/code-423n4/2024-07-karak/tree/main/src/Querier.sol#L14-L14)']
```solidity
14:     constructor(address coreAddress) {
15:         core = ICore(coreAddress);
16:     }
```


</details>

## [NonCritical-1] ERC777 tokens can introduce reentrancy risks

### Resolution 
ERC777 is an advanced token standard that introduces hooks, allowing operators to execute additional logic during transfers. While this feature offers greater flexibility, it also opens up the possibility of reentrancy attacks. Specifically, when tokens are sent, the receiving contract's `tokensReceived` hook gets called, and this external call can execute arbitrary code. An attacker can exploit this feature to re-enter the original function, potentially leading to double-spending or other types of financial manipulation.

To mitigate reentrancy risks with ERC777, it's crucial to adopt established security measures, such as utilizing reentrancy guards or following the check-effects-interactions pattern. Some developers opt to stick with the simpler ERC20 standard, which does not have these hooks, to minimize this risk. If you do choose to use ERC777, extreme caution and thorough auditing are advised to secure against potential reentrancy vulnerabilities.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[52](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L52-L58)']
```solidity
52:     function handleSlashing(IERC20 token, uint256 amount) external { // <= FOUND
53:         if (amount == 0) revert ZeroAmount();
54:         if (!_config().supportedAssets[token]) revert UnsupportedAsset();
55: 
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount); // <= FOUND
57:         
58:         SafeTransferLib.safeTransfer(address(token), address(0), amount); // <= FOUND
59:     }
```
['[544](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L544-L544)']
```solidity
544:     function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) { // <= FOUND
545:         
546:         from = from;
547:         to = to;
548:         amount = amount;
549: 
550:         revert NotImplemented();
551:     }
```


</details>

## [NonCritical-2] Floating pragma should be avoided

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[2](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L2-L2)']
```solidity
2: pragma solidity ^0.8.25; // <= FOUND
```
['[3](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L3-L3)']
```solidity
3: pragma solidity ^0.8.21; // <= FOUND
```
['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L4-L4)']
```solidity
4: pragma solidity ^0.8.0; // <= FOUND
```


</details>

## [NonCritical-3] Open TODO in comments

### Resolution 
Production code should not have open TODOs as this makes code appear incomplete at production deployment

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[235](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L235-L235)']
```solidity
235: // TODO: make more recent snapshot compulsory // <= FOUND
```


</details>

## [NonCritical-4] Not all event definitions are utilizing indexed variables.

### Resolution 
Try to index as much as three variables in event declarations as this is more gas efficient when done on value type variables (uint, address etc) however not for bytes and string variables 

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[24](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L24-L24)']
```solidity
24: event Paused(address account, uint256 map); // <= FOUND
```
['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L26-L26)']
```solidity
26: event Unpaused(address account, uint256 map); // <= FOUND
```


</details>

## [NonCritical-5] Explicitly define visibility of state variables to prevent misconceptions on what can access the variable

### Resolution 
Such state variables should be marked as private as this is the default visibility

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[70](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L70-L70)']
```solidity
70:     address nodeOwner; // <= FOUND
```


</details>

## [NonCritical-6] Functions within contracts are not ordered according to the solidity style guide

### Resolution 
The following order should be used within contracts

constructor

receive function (if exists)

fallback function (if exists)

external

public

internal

private

Rearrange the contract functions and contructors to fit this ordering

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L26-L26)']
```solidity
26: contract Core is IBeacon, ICore, OwnableRoles, Initializable, ReentrancyGuard, Pauser, ExtSloads  // <= FOUND
```
['[25](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L25-L25)']
```solidity
25: contract NativeVault is ERC4626, IBeacon, Pauser, INativeVault, OwnableRoles, ReentrancyGuard  // <= FOUND
```
['[10](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L10-L10)']
```solidity
10: contract Pauser is Initializable, ContextUpgradeable  // <= FOUND
```


</details>

## [NonCritical-7] Double type casts create complexity within the code

### Resolution 
Double type casting should be avoided in Solidity contracts to prevent unintended consequences and ensure accurate data representation. Performing multiple type casts in succession can lead to unexpected truncation, rounding errors, or loss of precision, potentially compromising the contract's functionality and reliability. Furthermore, double type casting can make the code less readable and harder to maintain, increasing the likelihood of errors and misunderstandings during development and debugging. To ensure precise and consistent data handling, developers should use appropriate data types and avoid unnecessary or excessive type casting, promoting a more robust and dependable contract execution.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[55](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L55-L55)']
```solidity
55:         n = uint64(uint256(lenum >> 192)); // <= FOUND
```
['[134](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L134-L134)']
```solidity
134:         return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei; // <= FOUND
```
['[24](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreStorageSlots.sol#L24-L24)']
```solidity
24:         return bytes32(uint256(operatorStateSlot(operator)) + PENDING_STAKE_UPDATE_MAPPING_OFFSET); // <= FOUND
```


</details>

## [NonCritical-8] Emits without msg.sender parameter

### Resolution 
In Solidity, when `msg.sender` plays a crucial role in a function's logic, it's important for transparency and auditability that any events emitted by this function include `msg.sender` as a parameter. This practice enhances the traceability and accountability of transactions, allowing users and external observers to easily track who initiated a particular action. Including `msg.sender` in event logs helps in creating a clear and verifiable record of interactions with the contract, thereby increasing user trust and facilitating easier debugging and analysis of contract behavior. It's a key aspect of writing clear, transparent, and user-friendly smart contracts.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[220](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L220-L230)']
```solidity
220:     function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest)
221:         external
222:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
223:         nonReentrant
224:         returns (SlasherLib.QueuedSlashing memory queuedSlashing)
225:     {
226:         IDSS dss = IDSS(msg.sender); // <= FOUND
227:         CoreLib.Storage storage self = _self();
228:         self.checkIfOperatorIsRegInRegDSS(slashingRequest.operator, dss);
229:         queuedSlashing = self.requestSlashing(dss, slashingRequest, self.nonce++);
230:         emit RequestedSlashing(address(dss), slashingRequest); // <= FOUND
231:     }
```


</details>

## [NonCritical-9] Unused modifiers present

### Resolution 
If these serve no purpose, they should be safely removed

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[44](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L44-L44)']
```solidity
44:     modifier whenNotPaused() { // <= FOUND
45:         if (paused()) revert EnforcedPause();
46:         _;
47:     }
```


</details>

## [NonCritical-10] Defined named returns not used within function 

### Resolution 
Such instances can be replaced with unnamed returns

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L78-L83)']
```solidity
78:     function deposit(uint256 assets, address to) // <= FOUND
79:         public
80:         override(ERC4626, IVault)
81:         whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
82:         nonReentrant
83:         returns (uint256 shares) // <= FOUND
84:     {
85:         if (assets == 0) revert ZeroAmount();
86:         return super.deposit(assets, to);
87:     }
```
['[299](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L299-L304)']
```solidity
299:     function slashAssets(uint256 totalAssetsToSlash, address slashingHandler) // <= FOUND
300:         external
301:         onlyOwner
302:         nonReentrant
303:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_SLASHER)
304:         returns (uint256 transferAmount) // <= FOUND
305:     {
306:         NativeVaultLib.Storage storage self = _state();
307: 
308:         if (slashingHandler != self.slashStore) revert NotSlashStore();
309: 
310:         
311:         if (totalAssetsToSlash > self.totalAssets) {
312:             totalAssetsToSlash = self.totalAssets;
313:         }
314: 
315:         self.totalAssets -= totalAssetsToSlash;
316:         emit Slashed(totalAssetsToSlash);
317:         return totalAssetsToSlash;
318:     }
```
['[114](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L114-L117)']
```solidity
114:     function validateBalance(bytes32 balanceRoot, uint40 validatorIndex, BalanceProof calldata proof) // <= FOUND
115:         internal
116:         view
117:         returns (uint256 validatorBalanceWei) // <= FOUND
118:     {
119:         if (proof.proof.length != 32 * (BALANCE_HEIGHT + 1)) revert InvalidBalanceProof();
120: 
121:         uint256 balanceIndex = uint256(validatorIndex / 4);
122: 
123:         if (
124:             !Merkle.verifyInclusionSha256({
125:                 proof: proof.proof,
126:                 root: balanceRoot,
127:                 leaf: proof.balanceRoot,
128:                 index: balanceIndex
129:             })
130:         ) revert InvalidBalanceProof();
131: 
132:         
133:         uint256 bitShiftAmount = (validatorIndex % 4) * 64;
134:         return uint256(fromLittleEndianUint64(bytes32((uint256(proof.balanceRoot) << bitShiftAmount)))) * 1 gwei;
135:     }
```


</details>

## [NonCritical-11] Initialize functions do not emit an event

### Resolution 
Emitting an event within initializer functions in Solidity is a best practice for providing transparency and traceability. Initializer functions set the initial state and values of an upgradeable contract. Emitting an event during initialization allows anyone to verify and audit the initial state of the contract via the transaction logs. This can be particularly useful for verifying the parameters set during initialization, tracking the contract's deployment, and troubleshooting or debugging. Therefore, developers should include an event emission in their initializer functions, providing a clear record of the contract's initialization and enhancing the contract's transparency and security.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[33](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L33-L33)']
```solidity
33:     function initialize(address owner, IERC20[] calldata _supportedAssets) external initializer { // <= FOUND
34:         _initializeOwner(owner);
35:         Config storage config = _config();
36:         for (uint256 i = 0; i < _supportedAssets.length; i++) {
37:             config.supportedAssets[_supportedAssets[i]] = true;
38:         }
39:     }
```
['[20](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashStore.sol#L20-L20)']
```solidity
20:     function initialize(address _owner) external initializer { // <= FOUND
21:         _initializeOwner(_owner);
22:     }
```
['[51](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L51-L51)']
```solidity
51:     function initialize( // <= FOUND
52:         address _owner,
53:         address _operator,
54:         address _depositToken,
55:         string memory _name,
56:         string memory _symbol,
57:         bytes memory _extraData
58:     ) external initializer {
59:         _initializeOwner(_owner);
60:         __Pauser_init();
61: 
62:         (bool decimalsSuccess, uint8 result) = _tryGetAssetDecimals(address(_depositToken));
63:         VaultLib.Config storage config = _config();
64: 
65:         config.asset = _depositToken;
66:         config.name = _name;
67:         config.symbol = _symbol;
68:         config.decimals = decimalsSuccess ? result : _DEFAULT_UNDERLYING_DECIMALS;
69:         config.operator = _operator;
70:         config.extraData = _extraData;
71:     }
```
['[53](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L53-L53)']
```solidity
53:     function initialize( // <= FOUND
54:         address _vaultImpl,
55:         address _manager,
56:         address _vetoCommittee,
57:         uint32 _hookCallGasLimit,
58:         uint32 _supportsInterfaceGasLimit,
59:         uint32 _hookGasBuffer
60:     ) external initializer {
61:         _initializeOwner(msg.sender);
62:         __Pauser_init();
63: 
64:         _grantRoles(_manager, Constants.MANAGER_ROLE);
65:         _grantRoles(_vetoCommittee, Constants.VETO_COMMITTEE_ROLE);
66: 
67:         _self().init(_vaultImpl, _vetoCommittee, _hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
68:     }
```
['[28](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeNode.sol#L28-L28)']
```solidity
28:     function initialize(address _owner, address _nodeOwner) external initializer { // <= FOUND
29:         _initializeOwner(_owner);
30:         __Pauser_init();
31: 
32:         nodeOwner = _nodeOwner;
33:     }
```


</details>

## [NonCritical-12] Event emit should emit a parameter

### Resolution 
Events in Solidity offer valuable insight into the contract's execution as they log specific instances of state changes or value transfers. However, if events do not include any parameters, their usefulness can be significantly reduced. Events without parameters can provide limited information, mainly signaling that a specific operation occurred, but lacking the context of what exactly changed. It's generally recommended to include relevant parameters, such as state changes or value modifications, in the emitted events. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[99](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L99-L100)']
```solidity
99:             
100:             emit InterfaceNotSupported(); // <= FOUND
```


</details>

## [NonCritical-13] No equate comparison checks between to and from address parameters

### Resolution 
The function lacks a standard check: it does not validate if the 'to' and 'from' addresses are identical. This omission can lead to unintended outcomes if the same address is used in both parameters. To rectify this, we recommend implementing a comparison check at the beginning of the function. In the context of Solidity, the command `require(to != from, "To and From addresses can't be the same");` could be utilized. This addition will generate an error if the 'to' and 'from' addresses are the same, thereby fortifying the function's robustness and security.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[544](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L544-L544)']
```solidity
544:     function transferFrom(address from, address to, uint256 amount) public pure override returns (bool) { // <= FOUND
545:         
546:         from = from;
547:         to = to;
548:         amount = amount;
549: 
550:         revert NotImplemented();
551:     }
```


</details>

## [NonCritical-14] Assembly block creates dirty bits

### Resolution 
Manipulating data directly at the free memory pointer location without subsequently adjusting the pointer can lead to unwanted data remnants, or "dirty bits", in that memory spot. This can cause challenges for the Solidity optimizer, making it difficult to determine if memory cleaning is required before reuse, potentially resulting in less efficient optimization. To mitigate this issue, it's advised to always update the free memory pointer following any data write operation. Furthermore, using the `assembly ("memory-safe") { ... }` annotation will clearly indicate to the optimizer the sections of your code that are memory-safe, improving code efficiency and reducing the potential for errors.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[58](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L58-L61)']
```solidity
58:                 assembly {
59:                     mstore(0x00, computedHash)
60:                     mstore(0x20, mload(add(proof, i)))
61:                     computedHash := keccak256(0x00, 0x40) // <= FOUND
62:                     index := div(index, 2)
63:                 }
```
['[116](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L116-L119)']
```solidity
116:                 assembly {
117:                     mstore(0x00, mload(computedHash))
118:                     mstore(0x20, mload(add(proof, i)))
119:                     if iszero(staticcall(sub(gas(), 2000), 2, 0x00, 0x40, computedHash, 0x20)) { revert(0, 0) } // <= FOUND
120:                     index := div(index, 2)
121:                 }
```


</details>

## [NonCritical-15] Unused import

### Resolution 
If these serve no purpose, they should be safely removed

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L4-L4)']
```solidity
4: import {Create2} from "@openzeppelin/contracts/utils/Create2.sol"; // <= FOUND
```


</details>

## [NonCritical-16] Missing events in sensitive functions

### Resolution 
Sensitive setter functions in smart contracts often alter critical state variables. Without events emitted in these functions, external observers or dApps cannot easily track or react to these state changes. Missing events can obscure contract activity, hampering transparency and making integration more challenging. To resolve this, incorporate appropriate event emissions within these functions. Events offer an efficient way to log crucial changes, aiding in real-time tracking and post-transaction verification.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[274](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L274-L274)']
```solidity
274:     function setGasValues(uint32 _hookCallGasLimit, uint32 _hookGasBuffer, uint32 _supportsInterfaceGasLimit) // <= FOUND
275:         external
276:         onlyRolesOrOwner(Constants.MANAGER_ROLE)
277:     {
278:         _self().updateGasValues(_hookCallGasLimit, _supportsInterfaceGasLimit, _hookGasBuffer);
279:     }
```
['[174](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L174-L174)']
```solidity
174:     function setDSSMaxSlashablePercentageWad( // <= FOUND
175:         CoreLib.Storage storage self,
176:         IDSS dss,
177:         uint256 dssMaxSlashablePercentageWad
178:     ) public {
179:         uint256 currentSlashablePercentageWad = self.dssMaxSlashablePercentageWad[dss];
180:         if (currentSlashablePercentageWad != 0) revert DSSAlreadyRegistered();
181:         if (dssMaxSlashablePercentageWad == 0) revert ZeroSlashPercentageWad();
182:         if (dssMaxSlashablePercentageWad > Constants.MAX_SLASHING_PERCENT_WAD) revert MaxSlashPercentageWadBreached();
183:         self.dssMaxSlashablePercentageWad[dss] = dssMaxSlashablePercentageWad;
184:     }
```
['[103](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L103-L103)']
```solidity
103:     function updateVaultStakeInDSS(State storage operatorState, address vault, IDSS dss, bool toStake) internal { // <= FOUND
104:         if (toStake) {
105:             operatorState.vaultStakedInDssMap[dss].add(vault);
106:         } else {
107:             operatorState.vaultStakedInDssMap[dss].remove(vault);
108:         }
109:     }
```
['[56](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L56-L56)']
```solidity
56:     function updateGasValues( // <= FOUND
57:         Storage storage self,
58:         uint32 _hookCallGasLimit,
59:         uint32 _supportsInterfaceGasLimit,
60:         uint32 _hookGasBuffer
61:     ) internal {
62:         self.hookCallGasLimit = _hookCallGasLimit;
63:         self.hookGasBuffer = _hookGasBuffer;
64:         self.supportsInterfaceGasLimit = _supportsInterfaceGasLimit;
65:     }
```
['[517](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L517-L517)']
```solidity
517:     function _updateBalance(address _of, int256 assets) internal { // <= FOUND
518:         if (assets > 0) {
519:             _increaseBalance(_of, uint256(assets));
520:         } else if (assets < 0) {
521:             _decreaseBalance(_of, uint256(-assets));
522:         } else {
523:             return;
524:         }
525:     }
```


</details>

## [NonCritical-17] Ensure block.timestamp is only used in long time intervals

### Resolution 
`block.timestamp` represents the current block's timestamp and can be influenced, within limits, by miners. For short time intervals, this malleability can be exploited, potentially allowing miners to manipulate contract behavior. For instance, they might fast-forward an expiration or delay an event. When designing smart contracts, if precise time checks are needed for short intervals, alternatives like block numbers can be considered. However, for longer durations where a few seconds of deviation is inconsequential, `block.timestamp` is generally safe and efficient. Always assess the implications of time manipulations for the specific use-case before utilizing `block.timestamp`. In practice, if you're using block.timestamp to measure intervals that are a matter of days, weeks, or longer, the potential manipulation by miners becomes less significant. Always prioritize the security and integrity of your smart contract operations when making these decisions.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[111](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L111-L112)']
```solidity
111:         self.operatorState[slashingMetadata.operator].nextSlashableTimestamp[dss] =
112:             block.timestamp + Constants.SLASHING_COOLDOWN; // <= FOUND
```


</details>

## [NonCritical-18] A event should be emitted if a non immutable state variable is set in a constructor

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[14](https://github.com/code-423n4/2024-07-karak/tree/main/src/Querier.sol#L14-L15)']
```solidity
14:     constructor(address coreAddress) {
15:         core = ICore(coreAddress); // <= FOUND
16:     }
```


</details>

## [NonCritical-19] gasLimit should be uint64

### Resolution 
To ensure compatability with the EVM gasLimits should be uint64 to prevent values higher than what is compatible. In instances where L2's are used this is even more paramount as a gasLimit higher than max(uint64) may be allowed within the L2, this may not be the case with hte underlying L1 such as ZKEVM and the EVM

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/HookLib.sol#L16-L22)']
```solidity
16:     
22:     function performLowLevelCallAndLimitReturnData(address target, bytes memory data, uint256 gasLimit) // <= FOUND
23:         internal
24:         returns (bool success, bytes32 returnVal)
25:     {
```


</details>

## [NonCritical-20] Pure function storage pointer bug

### Resolution 
In Solidity, a function marked as `pure` is expected not to read from or modify the state of the blockchain, meaning it shouldn't access or alter any state variables. However, a common oversight occurs when such functions inadvertently use storage pointers. A storage pointer in Solidity refers directly to a state variable, and a pure function using these pointers may end up interacting with the contract's state, contradicting its pure designation. This can lead to subtle bugs because the compiler doesn't flag this misuse, as it expects no state interaction in pure functions. The resolution is to thoroughly review pure functions to ensure they don't use storage pointers, or if necessary, reclassify them as `view` functions if they must read (but not modify) the contract's state. This distinction is crucial for both accurate representation of the function's behavior and for maintaining contract integrity and security.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[61](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L61-L61)']
```solidity
61:     function _config() internal pure returns (Config storage $) { // <= FOUND
62:         assembly {
63:             $.slot := CONFIG_SLOT
64:         }
65:     }
```
['[297](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L297-L297)']
```solidity
297:     function _state() internal pure returns (VaultLib.State storage $) { // <= FOUND
298:         assembly {
299:             $.slot := STATE_SLOT
300:         }
301:     }
```
['[409](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L409-L409)']
```solidity
409:     function _config() internal pure returns (VaultLib.Config storage $) { // <= FOUND
410:         assembly {
411:             $.slot := CONFIG_SLOT
412:         }
413:     }
```
['[309](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L309-L309)']
```solidity
309:     function _storage() internal pure returns (VaultLib.State storage $, VaultLib.Config storage $$) { // <= FOUND
310:         assembly {
311:             $.slot := STATE_SLOT
312:             $$.slot := CONFIG_SLOT
313:         }
314:     }
```
['[385](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L385-L385)']
```solidity
385:     function _self() internal pure returns (CoreLib.Storage storage $) { // <= FOUND
386:         assembly {
387:             $.slot := STORAGE_SLOT
388:         }
389:     }
```
['[403](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L403-L403)']
```solidity
403:     function _state() internal pure returns (NativeVaultLib.Storage storage $) { // <= FOUND
404:         assembly {
405:             $.slot := STATE_SLOT
406:         }
407:     }
```
['[409](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L409-L409)']
```solidity
409:     function _config() internal pure returns (VaultLib.Config storage $) { // <= FOUND
410:         assembly {
411:             $.slot := CONFIG_SLOT
412:         }
413:     }
```
['[18](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L18-L18)']
```solidity
18:     function _getPauserStorage() private pure returns (PauserStorage storage $) { // <= FOUND
19:         assembly {
20:             $.slot := PAUSER_STORAGE_SLOT
21:         }
22:     }
```


</details>

## [NonCritical-21] Use 'using' keyword when using specific imports rather than calling the specific import directly

### Resolution 
In Solidity, the `using` keyword can streamline the use of library functions for specific types. Instead of calling library functions directly with their full import paths, you can declare a library once with `using` for a specific type. This approach makes your code more readable and concise. For example, instead of `LibraryName.functionName(variable)`, you would first declare `using LibraryName for TypeName;` at the contract level. After this, you can call library functions directly on variables of `TypeName` like `variable.functionName()`. This method not only enhances code clarity but also promotes cleaner and more organized code, especially when multiple functions from the same library are used frequently.

Num of instances: 106

### Findings 


<details><summary>Click to show findings</summary>

['[56](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L56-L56)']
```solidity
56:         SafeTransferLib.safeTransferFrom(address(token), msg.sender, address(this), amount); // <= FOUND 'SafeTransferLib.'
```
['[58](https://github.com/code-423n4/2024-07-karak/tree/main/src/SlashingHandler.sol#L58-L59)']
```solidity
58:         
59:         SafeTransferLib.safeTransfer(address(token), address(0), amount); // <= FOUND 'SafeTransferLib.'
```
['[201](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L201-L202)']
```solidity
201:         
202:         SafeTransferLib.safeApproveWithRetry(asset(), slashingHandler, transferAmount); // <= FOUND 'SafeTransferLib.'
```
['[30](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L30-L30)']
```solidity
30:     using VaultLib for VaultLib.State; // <= FOUND 'VaultLib.'
```
['[66](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L66-L66)']
```solidity
66:         VaultLib.Config storage config = _config(); // <= FOUND 'VaultLib.'
```
['[134](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L134-L134)']
```solidity
134:         (VaultLib.State storage state, VaultLib.Config storage config) = _storage(); // <= FOUND 'VaultLib.'
```
['[631](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L631-L632)']
```solidity
631:     
632:     function vaultConfig() public pure returns (VaultLib.Config memory) { // <= FOUND 'VaultLib.'
```
['[297](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L297-L300)']
```solidity
297:     
300:     function _state() internal pure returns (VaultLib.State storage $) { // <= FOUND 'VaultLib.'
```
['[409](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L409-L409)']
```solidity
409:     function _config() internal pure returns (VaultLib.Config storage $) { // <= FOUND 'VaultLib.'
```
['[309](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L309-L309)']
```solidity
309:     function _storage() internal pure returns (VaultLib.State storage $, VaultLib.Config storage $$) { // <= FOUND 'VaultLib.'
```
['[33](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L33-L33)']
```solidity
33:     using VaultLib for VaultLib.Config; // <= FOUND 'VaultLib.'
```
['[161](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L161-L167)']
```solidity
161:     
167:     function deployVaults(VaultLib.Config[] calldata vaultConfigs, address vaultImpl) // <= FOUND 'VaultLib.'
168:         external
169:         whenFunctionNotPaused(Constants.PAUSE_CORE_DEPLOY_VAULTS)
170:         nonReentrant
171:         returns (IKarakBaseVault[] memory vaults)
172:     {
```
['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L26-L26)']
```solidity
26:     using NativeVaultLib for NativeVaultLib.Storage; // <= FOUND 'VaultLib.'
```
['[65](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L65-L65)']
```solidity
65:         NativeVaultLib.Storage storage self = _state(); // <= FOUND 'VaultLib.'
```
['[137](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L137-L137)']
```solidity
137:         NativeVaultLib.NativeNode storage node = self.ownerToNode[nodeOwner]; // <= FOUND 'VaultLib.'
```
['[138](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L138-L138)']
```solidity
138:         NativeVaultLib.Snapshot memory snapshot = node.currentSnapshot; // <= FOUND 'VaultLib.'
```
['[145](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L145-L145)']
```solidity
145:             NativeVaultLib.ValidatorDetails memory validatorDetails = // <= FOUND 'VaultLib.'
146:                 node.validatorPubkeyHashToDetails[balanceProofs[i].pubkeyHash];
```
['[148](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L148-L148)']
```solidity
148:             if (validatorDetails.status != NativeVaultLib.ValidatorStatus.ACTIVE) revert InactiveValidator(); // <= FOUND 'VaultLib.'
```
['[216](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L216-L216)']
```solidity
216:         NativeVaultLib.NativeNode storage node = _state().ownerToNode[nodeOwner]; // <= FOUND 'VaultLib.'
```
['[65](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L65-L66)']
```solidity
65:         
66:         NativeVaultLib.Storage storage self = _state(); // <= FOUND 'VaultLib.'
```
['[237](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L237-L237)']
```solidity
237:         NativeVaultLib.NativeNode storage node = self.ownerToNode[msg.sender]; // <= FOUND 'VaultLib.'
```
['[247](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L247-L247)']
```solidity
247:         withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++); // <= FOUND 'VaultLib.'
```
['[268](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L268-L268)']
```solidity
268:         NativeVaultLib.QueuedWithdrawal memory startedWithdrawal = self.withdrawalMap[withdrawalKey]; // <= FOUND 'VaultLib.'
```
['[269](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L269-L269)']
```solidity
269:         NativeVaultLib.NativeNode storage node = self.ownerToNode[startedWithdrawal.nodeOwner]; // <= FOUND 'VaultLib.'
```
['[360](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L360-L360)']
```solidity
360:         return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)].start > 0; // <= FOUND 'VaultLib.'
```
['[363](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L363-L366)']
```solidity
363:     function getQueuedWithdrawal(address nodeOwner, uint256 withdrawNonce)
364:         public
365:         view
366:         returns (NativeVaultLib.QueuedWithdrawal memory) // <= FOUND 'VaultLib.'
367:     {
```
['[368](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L368-L368)']
```solidity
368:         return _state().withdrawalMap[NativeVaultLib.calculateWithdrawKey(nodeOwner, withdrawNonce)]; // <= FOUND 'VaultLib.'
```
['[375](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L375-L379)']
```solidity
375:     function getValidatorDetails(bytes32 pubKey, address nodeOwner)
376:         external
377:         view
378:         nodeExists(nodeOwner)
379:         returns (NativeVaultLib.ValidatorDetails memory) // <= FOUND 'VaultLib.'
380:     {
```
['[392](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L392-L396)']
```solidity
392:     function currentSnapshot(address nodeOwner)
393:         external
394:         view
395:         nodeExists(nodeOwner)
396:         returns (NativeVaultLib.Snapshot memory) // <= FOUND 'VaultLib.'
397:     {
```
['[403](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L403-L406)']
```solidity
403:     
406:     function _state() internal pure returns (NativeVaultLib.Storage storage $) { // <= FOUND 'VaultLib.'
```
['[448](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L448-L448)']
```solidity
448:     function _startSnapshot(NativeVaultLib.NativeNode storage node, bool revertIfNoBalanceChange, address nodeOwner) // <= FOUND 'VaultLib.'
449:         internal
450:     {
```
['[463](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L463-L463)']
```solidity
463:         NativeVaultLib.Snapshot memory snapshot = NativeVaultLib.Snapshot({ // <= FOUND 'VaultLib.'
464:             parentBeaconBlockRoot: _getParentBlockRoot(uint64(block.timestamp)),
465:             nodeBalanceWei: nodeBalanceWei,
466:             balanceDeltaWei: 0,
467:             remainingProofs: node.activeValidatorCount
468:         });
```
['[476](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L476-L478)']
```solidity
476:     function _updateSnapshot(
477:         NativeVaultLib.NativeNode storage node, // <= FOUND 'VaultLib.'
478:         NativeVaultLib.Snapshot memory snapshot, // <= FOUND 'VaultLib.'
479:         address nodeOwner
480:     ) internal {
```
['[631](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L631-L631)']
```solidity
631:     function vaultConfig() public pure returns (VaultLib.Config memory) { // <= FOUND 'VaultLib.'
```
['[77](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L77-L77)']
```solidity
77:     function validateVaultConfigs(Storage storage self, VaultLib.Config[] calldata vaultConfigs, address implementation) // <= FOUND 'VaultLib.'
78:         public
79:         view
80:     {
```
['[118](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L118-L122)']
```solidity
118:     function deployVaults(
119:         Storage storage self,
120:         address operator,
121:         address implementation,
122:         VaultLib.Config[] calldata vaultConfigs // <= FOUND 'VaultLib.'
123:     ) external returns (IKarakBaseVault[] memory) {
```
['[93](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L93-L93)']
```solidity
93:     function deployNode(Storage storage self, VaultLib.Config storage config, address owner) // <= FOUND 'VaultLib.'
94:         internal
95:         returns (address)
96:     {
```
['[154](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L154-L154)']
```solidity
154:         NativeVaultLib.ValidatorDetails memory validatorDetails = // <= FOUND 'VaultLib.'
155:             self.ownerToNode[nodeOwner].validatorPubkeyHashToDetails[validatorPubkeyHash];
```
['[157](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L157-L157)']
```solidity
157:         if (validatorDetails.status != NativeVaultLib.ValidatorStatus.INACTIVE) revert ValidatorAlreadyActive(); // <= FOUND 'VaultLib.'
```
['[177](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L177-L177)']
```solidity
177:         validatorDetails.status = NativeVaultLib.ValidatorStatus.ACTIVE; // <= FOUND 'VaultLib.'
```
['[139](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L139-L139)']
```solidity
139:         withdrawalKey = WithdrawLib.calculateWithdrawKey(staker, state.stakerToWithdrawNonce[staker]++); // <= FOUND 'WithdrawLib.'
```
['[164](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L164-L164)']
```solidity
164:         WithdrawLib.QueuedWithdrawal memory startedWithdrawal = state.validateQueuedWithdrawal(withdrawalKey); // <= FOUND 'WithdrawLib.'
```
['[251](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L251-L251)']
```solidity
251:         return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)].start > 0; // <= FOUND 'WithdrawLib.'
```
['[258](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L258-L265)']
```solidity
258:     
262:     function getQueuedWithdrawal(address staker, uint256 _withdrawNonce)
263:         public
264:         view
265:         returns (WithdrawLib.QueuedWithdrawal memory) // <= FOUND 'WithdrawLib.'
266:     {
```
['[263](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L263-L263)']
```solidity
263:         return _state().withdrawalMap[WithdrawLib.calculateWithdrawKey(staker, _withdrawNonce)]; // <= FOUND 'WithdrawLib.'
```
['[21](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/VaultLib.sol#L21-L21)']
```solidity
21:         mapping(bytes32 stakerWithdrawNonceKey => WithdrawLib.QueuedWithdrawal withdrawal) withdrawalMap; // <= FOUND 'WithdrawLib.'
```
['[24](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/VaultLib.sol#L24-L27)']
```solidity
24:     function validateQueuedWithdrawal(State storage self, bytes32 withdrawalKey)
25:         internal
26:         view
27:         returns (WithdrawLib.QueuedWithdrawal memory qdWithdrawal) // <= FOUND 'WithdrawLib.'
28:     {
```
['[16](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L16-L16)']
```solidity
16:     using CoreLib for CoreLib.Storage; // <= FOUND 'CoreLib.'
```
['[28](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L28-L28)']
```solidity
28:     using Operator for CoreLib.Storage; // <= FOUND 'CoreLib.'
```
['[32](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L32-L32)']
```solidity
32:     using SlasherLib for CoreLib.Storage; // <= FOUND 'CoreLib.'
```
['[103](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L103-L103)']
```solidity
103:         CoreLib.Storage storage self = _self(); // <= FOUND 'CoreLib.'
```
['[385](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L385-L388)']
```solidity
385:     
388:     function _self() internal pure returns (CoreLib.Storage storage $) { // <= FOUND 'CoreLib.'
```
['[61](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L61-L62)']
```solidity
61:     function requestUpdateVaultStakeInDSS(
62:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
63:         StakeUpdateRequest memory requestStakeUpdate,
64:         uint128 nonce,
65:         address operator
66:     ) external returns (QueuedStakeUpdate memory queuedStake) {
```
['[111](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L111-L111)']
```solidity
111:     function validateAndUpdateVaultStakeInDSS(CoreLib.Storage storage self, QueuedStakeUpdate memory queuedStakeUpdate) // <= FOUND 'CoreLib.'
112:         external
113:     {
```
['[135](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L135-L135)']
```solidity
135:     function isOperatorRegisteredToDSS(CoreLib.Storage storage self, address operator, IDSS dss) // <= FOUND 'CoreLib.'
136:         internal
137:         view
138:         returns (bool)
139:     {
```
['[143](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L143-L143)']
```solidity
143:     function checkIfOperatorIsRegInRegDSS(CoreLib.Storage storage self, address operator, IDSS dss) internal view { // <= FOUND 'CoreLib.'
```
['[150](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L150-L151)']
```solidity
150:     function registerOperatorToDSS(
151:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
152:         IDSS dss,
153:         address operator,
154:         bytes memory registrationHookData
155:     ) external {
```
['[181](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L181-L182)']
```solidity
181:     function unregisterOperatorFromDSS(
182:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
183:         IDSS dss,
184:         address operator,
185:         bytes memory unregistrationHookData
186:     ) external {
```
['[209](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L209-L213)']
```solidity
209:     
213:     function getDSSsOperatorIsRegisteredTo(CoreLib.Storage storage self, address operator) // <= FOUND 'CoreLib.'
214:         internal
215:         view
216:         returns (address[] memory dssAddresses)
217:     {
```
['[224](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L224-L227)']
```solidity
224:     
227:     function getDSSCountVaultStakedTo(CoreLib.Storage storage self, IKarakBaseVault vault) // <= FOUND 'CoreLib.'
228:         external
229:         view
230:         returns (uint256 count)
231:     {
```
['[42](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L42-L43)']
```solidity
42:     function validateVaultsAndSlashPercentages(
43:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
44:         SlashRequest memory slashingRequest,
45:         IDSS dss
46:     ) internal view {
```
['[59](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L59-L59)']
```solidity
59:     function validateRequestSlashingParams(CoreLib.Storage storage self, SlashRequest memory slashingRequest, IDSS dss) // <= FOUND 'CoreLib.'
60:         internal
61:         view
62:     {
```
['[94](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L94-L95)']
```solidity
94:     function requestSlashing(
95:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
96:         IDSS dss,
97:         SlashRequest memory slashingMetadata,
98:         uint256 nonce
99:     ) external returns (QueuedSlashing memory queuedSlashing) {
```
['[126](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L126-L126)']
```solidity
126:     function finalizeSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external { // <= FOUND 'CoreLib.'
```
['[153](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L153-L153)']
```solidity
153:     function cancelSlashing(CoreLib.Storage storage self, QueuedSlashing memory queuedSlashing) external { // <= FOUND 'CoreLib.'
```
['[170](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L170-L170)']
```solidity
170:     function getDSSMaxSlashablePercentageWad(CoreLib.Storage storage self, IDSS dss) public view returns (uint256) { // <= FOUND 'CoreLib.'
```
['[174](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L174-L175)']
```solidity
174:     function setDSSMaxSlashablePercentageWad(
175:         CoreLib.Storage storage self, // <= FOUND 'CoreLib.'
176:         IDSS dss,
177:         uint256 dssMaxSlashablePercentageWad
178:     ) public {
```
['[30](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L30-L30)']
```solidity
30:     using SlasherLib for SlasherLib.QueuedSlashing; // <= FOUND 'SlasherLib.'
```
['[31](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L31-L31)']
```solidity
31:     using SlasherLib for SlasherLib.SlashRequest; // <= FOUND 'SlasherLib.'
```
['[220](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L220-L226)']
```solidity
220:     
222:     function requestSlashing(SlasherLib.SlashRequest calldata slashingRequest) // <= FOUND 'SlasherLib.'
223:         external
224:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_SLASHING)
225:         nonReentrant
226:         returns (SlasherLib.QueuedSlashing memory queuedSlashing) // <= FOUND 'SlasherLib.'
227:     {
```
['[235](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L235-L237)']
```solidity
235:     
237:     function cancelSlashing(SlasherLib.QueuedSlashing memory queuedSlashing) // <= FOUND 'SlasherLib.'
238:         external
239:         whenFunctionNotPaused(Constants.PAUSE_CORE_CANCEL_SLASHING)
240:         nonReentrant
241:         onlyRoles(Constants.VETO_COMMITTEE_ROLE)
242:     {
```
['[248](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L248-L251)']
```solidity
248:     
251:     function finalizeSlashing(SlasherLib.QueuedSlashing memory queuedSlashing) // <= FOUND 'SlasherLib.'
252:         external
253:         nonReentrant
254:         whenFunctionNotPaused(Constants.PAUSE_CORE_FINALIZE_SLASHING)
255:     {
```
['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L78-L78)']
```solidity
78:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
79:             dss: dss,
80:             data: abi.encodeWithSelector(dss.requestUpdateStakeHook.selector, operator, requestStakeUpdate),
81:             interfaceId: dss.requestUpdateStakeHook.selector,
82:             ignoreFailure: !requestStakeUpdate.toStake,
83:             hookCallGasLimit: self.hookCallGasLimit,
84:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
85:             hookGasBuffer: self.hookGasBuffer
86:         });
```
['[124](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L124-L124)']
```solidity
124:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
125:             dss: dss,
126:             data: abi.encodeWithSelector(dss.finishUpdateStakeHook.selector, msg.sender),
127:             interfaceId: dss.finishUpdateStakeHook.selector,
128:             ignoreFailure: true,
129:             hookCallGasLimit: self.hookCallGasLimit,
130:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
131:             hookGasBuffer: self.hookGasBuffer
132:         });
```
['[162](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L162-L162)']
```solidity
162:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
163:             dss: dss,
164:             data: abi.encodeWithSelector(dss.registrationHook.selector, operator, registrationHookData),
165:             interfaceId: dss.registrationHook.selector,
166:             ignoreFailure: false,
167:             hookCallGasLimit: self.hookCallGasLimit,
168:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
169:             hookGasBuffer: self.hookGasBuffer
170:         });
```
['[194](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Operator.sol#L194-L194)']
```solidity
194:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
195:             dss: dss,
196:             data: abi.encodeWithSelector(dss.unregistrationHook.selector, operator, unregistrationHookData),
197:             interfaceId: dss.unregistrationHook.selector,
198:             ignoreFailure: true, 
199:             hookCallGasLimit: self.hookCallGasLimit,
200:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
201:             hookGasBuffer: self.hookGasBuffer
202:         });
```
['[113](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L113-L113)']
```solidity
113:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
114:             dss: dss,
115:             data: abi.encodeWithSelector(
116:                 dss.requestSlashingHook.selector, slashingMetadata.operator, slashingMetadata.slashPercentagesWad
117:             ),
118:             interfaceId: dss.requestSlashingHook.selector,
119:             ignoreFailure: true,
120:             hookCallGasLimit: self.hookCallGasLimit,
121:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
122:             hookGasBuffer: self.hookGasBuffer
123:         });
```
['[142](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L142-L142)']
```solidity
142:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
143:             dss: dss,
144:             data: abi.encodeWithSelector(dss.finishSlashingHook.selector, queuedSlashing.operator),
145:             interfaceId: dss.finishSlashingHook.selector,
146:             ignoreFailure: true,
147:             hookCallGasLimit: self.hookCallGasLimit,
148:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
149:             hookGasBuffer: self.hookGasBuffer
150:         });
```
['[159](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L159-L159)']
```solidity
159:         HookLib.callHookIfInterfaceImplemented({ // <= FOUND 'HookLib.'
160:             dss: dss,
161:             data: abi.encodeWithSelector(dss.cancelSlashingHook.selector, queuedSlashing.operator),
162:             interfaceId: dss.cancelSlashingHook.selector,
163:             ignoreFailure: true,
164:             hookCallGasLimit: self.hookCallGasLimit,
165:             supportsInterfaceGasLimit: self.supportsInterfaceGasLimit,
166:             hookGasBuffer: self.hookGasBuffer
167:         });
```
['[101](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L101-L102)']
```solidity
101:         address expectedNewVaultAddr =
102:             LibClone.predictDeterministicAddressERC1967BeaconProxy(address(this), salt, address(this)); // <= FOUND 'LibClone.'
```
['[150](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L150-L150)']
```solidity
150:         return IKarakBaseVault(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt))); // <= FOUND 'LibClone.'
```
['[99](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L99-L99)']
```solidity
99:         INativeNode newNode = INativeNode(address(LibClone.deployDeterministicERC1967BeaconProxy(address(this), salt))); // <= FOUND 'LibClone.'
```
['[19](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L19-L19)']
```solidity
19:     using Operator for Operator.State; // <= FOUND 'Operator.'
```
['[130](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L130-L138)']
```solidity
130:     
134:     function requestUpdateVaultStakeInDSS(Operator.StakeUpdateRequest memory vaultStakeUpdateRequest) // <= FOUND 'Operator.'
135:         external
136:         nonReentrant
137:         whenFunctionNotPaused(Constants.PAUSE_CORE_REQUEST_STAKE_UPDATE)
138:         returns (Operator.QueuedStakeUpdate memory updatedStake) // <= FOUND 'Operator.'
139:     {
```
['[146](https://github.com/code-423n4/2024-07-karak/tree/main/src/Core.sol#L146-L149)']
```solidity
146:     
149:     function finalizeUpdateVaultStakeInDSS(Operator.QueuedStakeUpdate memory queuedStake) // <= FOUND 'Operator.'
150:         external
151:         nonReentrant
152:         whenFunctionNotPaused(Constants.PAUSE_CORE_FINALIZE_STAKE_UPDATE)
153:     {
```
['[22](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L22-L23)']
```solidity
22:         
23:         mapping(address operator => Operator.State) operatorState; // <= FOUND 'Operator.'
```
['[126](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L126-L134)']
```solidity
126:     
131:     function validateSnapshotProofs(
132:         address nodeOwner,
133:         BeaconProofs.BalanceProof[] calldata balanceProofs, // <= FOUND 'BeaconProofs.'
134:         BeaconProofs.BalanceContainer calldata balanceContainer // <= FOUND 'BeaconProofs.'
135:     )
136:         external
137:         nonReentrant
138:         nodeExists(nodeOwner)
139:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_VALIDATE_SNAPSHOT)
140:     {
```
['[142](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L142-L142)']
```solidity
142:         BeaconProofs.validateBalanceContainer(snapshot.parentBeaconBlockRoot, balanceContainer); // <= FOUND 'BeaconProofs.'
```
['[168](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L168-L175)']
```solidity
168:     
172:     function validateWithdrawalCredentials(
173:         address nodeOwner,
174:         BeaconProofs.BeaconStateRootProof calldata beaconStateRootProof, // <= FOUND 'BeaconProofs.'
175:         BeaconProofs.ValidatorFieldsProof[] calldata validatorFieldsProofs // <= FOUND 'BeaconProofs.'
176:     )
177:         external
178:         nonReentrant
179:         nodeExists(nodeOwner)
180:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_VALIDATE_WITHDRAW_CREDS)
181:     {
```
['[190](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L190-L190)']
```solidity
190:         BeaconProofs.validateBeaconStateRootProof( // <= FOUND 'BeaconProofs.'
191:             _getParentBlockRoot(beaconStateRootProof.timestamp), beaconStateRootProof
192:         );
```
['[110](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L110-L115)']
```solidity
110:     function validateSnapshotProof(
111:         Storage storage self,
112:         address nodeOwner,
113:         ValidatorDetails memory validatorDetails,
114:         bytes32 balanceRoot,
115:         BeaconProofs.BalanceProof calldata proof // <= FOUND 'BeaconProofs.'
116:     ) internal returns (int256 balanceDeltaWei) {
```
['[122](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L122-L122)']
```solidity
122:         uint256 newBalanceWei = BeaconProofs.validateBalance(balanceRoot, validatorIndex, proof); // <= FOUND 'BeaconProofs.'
```
['[146](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L146-L151)']
```solidity
146:     function validateWithdrawalCredentials(
147:         Storage storage self,
148:         address nodeOwner,
149:         uint64 updateTimestamp,
150:         bytes32 beaconStateRoot,
151:         BeaconProofs.ValidatorFieldsProof calldata validatorFieldsProof // <= FOUND 'BeaconProofs.'
152:     ) internal returns (uint256) {
```
['[153](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L153-L153)']
```solidity
153:         bytes32 validatorPubkeyHash = BeaconProofs.getPubkeyHash(validatorFieldsProof.validatorFields); // <= FOUND 'BeaconProofs.'
```
['[158](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L158-L158)']
```solidity
158:         if (BeaconProofs.getExitEpoch(validatorFieldsProof.validatorFields) != type(uint64).max) { // <= FOUND 'BeaconProofs.'
```
['[162](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L162-L164)']
```solidity
162:         
163:         if (
164:             BeaconProofs.getWithdrawalCredentials(validatorFieldsProof.validatorFields) // <= FOUND 'BeaconProofs.'
165:                 != bytes32(abi.encodePacked(bytes1(uint8(1)), bytes11(0), address(self.ownerToNode[nodeOwner].nodeAddress)))
166:         ) {
```
['[169](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L169-L169)']
```solidity
169:         uint256 restakedBalanceWei = BeaconProofs.getEffectiveBalanceWei(validatorFieldsProof.validatorFields); // <= FOUND 'BeaconProofs.'
```
['[170](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L170-L170)']
```solidity
170:         BeaconProofs.validateValidatorProof( // <= FOUND 'BeaconProofs.'
171:             validatorFieldsProof.validatorProof.validatorIndex,
172:             validatorFieldsProof.validatorFields,
173:             validatorFieldsProof.validatorProof.proof,
174:             beaconStateRoot
175:         );
```
['[30](https://github.com/code-423n4/2024-07-karak/tree/main/src/Querier.sol#L30-L30)']
```solidity
30:             slots[i] = CoreStorageSlots.vaultPendingStakeUpdateSlot(operator, stakedVaults[i]); // <= FOUND 'CoreStorageSlots.'
```
['[66](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L66-L67)']
```solidity
66:         if (
67:             !Merkle.verifyInclusionSha256( // <= FOUND 'Merkle.'
68:                 beaconStateRootProof.proof, beaconBlockRoot, beaconStateRootProof.beaconStateRoot, BEACON_STATE_ROOT_IDX
69:             )
70:         ) revert InvalidBeaconStateProof();
```
['[81](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L81-L81)']
```solidity
81:         bytes32 validatorRoot = Merkle.merkleizeSha256(validatorFields); // <= FOUND 'Merkle.'
```
['[92](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L92-L93)']
```solidity
92:         
93:         if (!Merkle.verifyInclusionSha256(validatorProof, beaconStateRoot, validatorRoot, index)) { // <= FOUND 'Merkle.'
```
['[104](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L104-L105)']
```solidity
104:         if (
105:             !Merkle.verifyInclusionSha256({ // <= FOUND 'Merkle.'
106:                 proof: proof.proof,
107:                 root: beaconBlockRoot,
108:                 leaf: proof.containerRoot,
109:                 index: index
110:             })
```
['[123](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L123-L124)']
```solidity
123:         if (
124:             !Merkle.verifyInclusionSha256({ // <= FOUND 'Merkle.'
125:                 proof: proof.proof,
126:                 root: balanceRoot,
127:                 leaf: proof.balanceRoot,
128:                 index: balanceIndex
129:             })
```
['[53](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L53-L53)']
```solidity
53:         require(proof.length % 32 == 0, "Merkle.processInclusionProofKeccak: proof length should be a multiple of 32"); // <= FOUND 'Merkle.'
```
['[108](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L108-L110)']
```solidity
108:         require(
109:             proof.length != 0 && proof.length % 32 == 0,
110:             "Merkle.processInclusionProofSha256: proof length should be a non-zero multiple of 32" // <= FOUND 'Merkle.'
111:         );
```


</details>

## [NonCritical-22] Inconsistent checks of address params against address(0)

### Resolution 
Only some address parameters are checked against address(0), to ensure consistency ensure all address parameters are checked.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[46](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L46-L49)']
```solidity
46:     function initialize(
47:         address _owner, // <= FOUND
48:         address _operator, // <= FOUND
49:         address _depositToken, // <= FOUND
50:         string memory _name,
51:         string memory _symbol,
52:         bytes memory _extraData
53:     ) external initializer {
54:         _initializeOwner(_owner);
55:         __Pauser_init();
56: 
57:         if (_depositToken != Constants.DEAD_BEEF) revert DepositTokenNotAccepted();
58: 
59:         (address manager, address slashStore, address nodeImplementation) =
60:             abi.decode(_extraData, (address, address, address));
61: 
62:         if (manager == address(0) || slashStore == address(0) || nodeImplementation == address(0)) revert ZeroAddress();
63:         _grantRoles(manager, Constants.MANAGER_ROLE);
64: 
65:         NativeVaultLib.Storage storage self = _state();
66:         VaultLib.Config storage config = _config();
67: 
68:         config.asset = _depositToken;
69:         config.name = _name;
70:         config.symbol = _symbol;
71:         config.decimals = 18;
72:         config.operator = _operator;
73:         config.extraData = _extraData;
74: 
75:         self.slashStore = slashStore;
76:         self.nodeImpl = nodeImplementation;
77: 
78:         emit NativeVaultInitialized(_owner, manager, _operator, slashStore);
79:     }
```


</details>

## [NonCritical-23] Avoid declaring variables with the names of defined functions within the project

### Resolution 
Having such variables can create confusion in both developers and in users of the project. Consider renaming these variables to improve code clarity.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[118](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L118-L121)']
```solidity
118:     function deployVaults(
119:         Storage storage self,
120:         address operator,
121:         address implementation, // <= FOUND
122:         VaultLib.Config[] calldata vaultConfigs
123:     ) external returns (IKarakBaseVault[] memory) {
```
['[78](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L78-L79)']
```solidity
78:         
79:         uint256 totalAssets; // <= FOUND
```
['[55](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L55-L56)']
```solidity
55:         
56:         uint256 activeValidatorCount; // <= FOUND
```
['[53](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L53-L54)']
```solidity
53:         
54:         uint64 lastSnapshotTimestamp; // <= FOUND
```
['[57](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L57-L58)']
```solidity
57:         
58:         uint64 currentSnapshotTimestamp; // <= FOUND
```


</details>

## [NonCritical-24] Contract and Abstract files should have a fixed compiler version

### Resolution 
Using a fixed compiler version in Solidity contract and abstract files ensures consistency and predictability in smart contract behavior. A fixed version prevents unforeseen issues arising from compiler updates, which might introduce breaking changes or new bugs. It guarantees that the contract's behavior remains stable and consistent with the version used during its development and testing.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[4](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/MerkleProofs.sol#L4-L4)']
```solidity
4: pragma solidity ^0.8.0; // <= FOUND
```
['[3](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/Pauser.sol#L3-L3)']
```solidity
3: pragma solidity ^0.8.21; // <= FOUND
```


</details>

## [NonCritical-25] Function call in event emit

### Resolution 
Emits are designed to make users aware of state variable changes. As such the event declaration should be clear on what it will output, by passing in function calls this can affect the readability of a emit declaration. As such it is advisable to make function calls outside of the event emit and pass the return value into the emit instead.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[228](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L228-L255)']
```solidity
228:     function startWithdrawal(address to, uint256 weiAmount)
229:         external
230:         nonReentrant
231:         nodeExists(msg.sender)
232:         whenFunctionNotPaused(Constants.PAUSE_NATIVEVAULT_START_WITHDRAWAL)
233:         returns (bytes32 withdrawalKey)
234:     {
235:         
236:         NativeVaultLib.Storage storage self = _state();
237:         NativeVaultLib.NativeNode storage node = self.ownerToNode[msg.sender];
238:         if (weiAmount > withdrawableWei(msg.sender) - self.nodeOwnerToWithdrawAmount[msg.sender]) {
239:             revert WithdrawMoreThanMax();
240:         }
241:         self.nodeOwnerToWithdrawAmount[msg.sender] += weiAmount;
242: 
243:         if (block.timestamp >= node.lastSnapshotTimestamp + Constants.SNAPSHOT_EXPIRY) {
244:             revert SnapshotExpired();
245:         }
246: 
247:         withdrawalKey = NativeVaultLib.calculateWithdrawKey(msg.sender, self.nodeOwnerToWithdrawNonce[msg.sender]++);
248:         address nodeOwner = msg.sender;
249: 
250:         self.withdrawalMap[withdrawalKey].to = to;
251:         self.withdrawalMap[withdrawalKey].assets = weiAmount;
252:         self.withdrawalMap[withdrawalKey].nodeOwner = nodeOwner;
253:         self.withdrawalMap[withdrawalKey].start = uint96(block.timestamp);
254: 
255:         emit StartedWithdraw(nodeOwner, _config().operator, withdrawalKey, weiAmount, to); // <= FOUND
256: 
257:         return withdrawalKey;
258:     }
```


</details>

## [NonCritical-26] For loop iterates on arrays not indexed

### Resolution 
Ensuring matching input array lengths in functions is crucial to prevent logical errors and inconsistencies in smart contracts. Mismatched array lengths can lead to incomplete operations or incorrect data handling, particularly if one array's length is assumed to reflect another's. For instance, iterating over a shorter array than intended could result in unprocessed elements from a longer array, potentially causing unintended consequences in contract execution. Validating that all input arrays have intended lengths before performing operations helps safeguard against such errors, ensuring that all elements are appropriately processed and the contract behaves as expected.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[50](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L50-L55)']
```solidity
50:        for (uint256 i = 0; i < slashingRequest.vaults.length; i++) { // <= FOUND
51:             if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {
52:                 revert VaultNotStakedToDSS();
53:             }
54:             if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad(); // <= FOUND
55:             if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached(); // <= FOUND
56:         }
```
['[50](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L50-L55)']
```solidity
50:         for (uint256 i = 0; i < slashingRequest.vaults.length; i++) { // <= FOUND
51:             if (!self.operatorState[slashingRequest.operator].isVaultStakeToDSS(dss, slashingRequest.vaults[i])) {
52:                 revert VaultNotStakedToDSS();
53:             }
54:             if (slashingRequest.slashPercentagesWad[i] == 0) revert ZeroSlashPercentageWad(); // <= FOUND
55:             if (slashingRequest.slashPercentagesWad[i] > maxSlashPercentageWad) revert MaxSlashPercentageWadBreached(); // <= FOUND
56:         }
```
['[132](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/CoreLib.sol#L132-L142)']
```solidity
132:         for (uint256 i = 0; i < vaultConfigs.length; i++) { // <= FOUND
133:             IKarakBaseVault vault = createVault(
134:                 self,
135:                 operator,
136:                 vaultConfigs[i].asset,
137:                 vaultConfigs[i].name,
138:                 vaultConfigs[i].symbol,
139:                 vaultConfigs[i].extraData,
140:                 implementation
141:             );
142:             vaults[i] = vault; // <= FOUND
143:             self.operatorState[operator].addVault(vault);
144:             emit DeployedVault(operator, address(vault), vaultConfigs[i].asset);
145:         }
```


</details>

## [NonCritical-27] Avoid using 'owner' or '_owner' as a parameter name

### Resolution 
Using 'owner' or '_owner' as a parameter name in functions, especially in contracts inheriting from or interacting with OpenZeppelin's `Ownable` contract, can lead to confusion and potential bugs. These contracts often have a state variable named `owner`, managed by the `Ownable` pattern for access control. Using the same name for function parameters may obscure the contract's `owner` state variable, complicating code readability and maintenance. Prefer alternative descriptive names for parameters to maintain clarity and prevent conflicts with established ownership patterns.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[331](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L331-L331)']
```solidity
331:     function withdraw(uint256 assets, address to, address owner) // <= FOUND
332:         public
333:         override
334:         whenFunctionNotPaused(Constants.PAUSE_VAULT_WITHDRAW)
335:         nonReentrant
336:         returns (uint256 shares)
337:     
```
['[348](https://github.com/code-423n4/2024-07-karak/tree/main/src/Vault.sol#L348-L348)']
```solidity
348:     function redeem(uint256 shares, address to, address owner) // <= FOUND
349:         public
350:         override
351:         whenFunctionNotPaused(Constants.PAUSE_VAULT_REDEEM)
352:         nonReentrant
353:         returns (uint256 assets)
354:     
```
['[571](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L571-L571)']
```solidity
571:     function withdraw(uint256 assets, address to, address owner) public pure override returns (uint256 shares)  // <= FOUND
```
['[581](https://github.com/code-423n4/2024-07-karak/tree/main/src/NativeVault.sol#L581-L581)']
```solidity
581:     function redeem(uint256 shares, address to, address owner) public pure override returns (uint256 assets)  // <= FOUND
```
['[93](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L93-L93)']
```solidity
93:     function deployNode(Storage storage self, VaultLib.Config storage config, address owner) // <= FOUND
94:         internal
95:         returns (address)
96:     
```


</details>

## [NonCritical-28] Avoid arithmetic directly within array indices

### Resolution 
Avoiding arithmetic directly within array indices, like `test[i + 2]`, is recommended to prevent errors such as index out of bounds or incorrect data access. This practice enhances code readability and maintainability. Instead, calculate the index beforehand, store it in a variable, and then use that variable to access the array element. This approach reduces mistakes, especially in complex loops or when handling dynamic data, ensuring that each access is clear and verifiable. It's about keeping code clean and understandable, minimizing potential bugs.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[15](https://github.com/code-423n4/2024-07-karak/tree/main/src/utils/ExtSloads.sol#L15-L15)']
```solidity
15:             bytes32 slot = slots[i++]; // <= FOUND
```


</details>

## [NonCritical-29] Memory-safe annotation missing

### Resolution 
Tagging assembly blocks as "memory safe" in Solidity helps maintainers and auditors quickly identify areas of the code less likely to introduce vulnerabilities due to improper memory access. This practice promotes safer contract development by clearly communicating assumptions about memory handling, aiding in the review process, and reducing the risk of introducing memory-related bugs. It's a part of best coding practices, enhancing code clarity and security, especially in complex, low-level operations where Solidity's safety checks are bypassed.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[50](https://github.com/code-423n4/2024-07-karak/tree/main/src/utils/CommonUtils.sol#L50-L50)']
```solidity
50:         assembly {
51:             size := extcodesize(addr)
52:         }
```


</details>

## [NonCritical-30] Constant state variables defined more than once

### Resolution 
Rather than redefining state variable constant, consider utilising a library to store all constants as this will prevent data redundancy

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[10](https://github.com/code-423n4/2024-07-karak/tree/main/src/Querier.sol#L10-L10)']
```solidity
10: string public constant VERSION = "2.0.0"; // <= FOUND
```


</details>

## [NonCritical-31] Unnecessary struct attribute prefix

### Resolution 
In struct definitions, using redundant prefixes for attributes is unnecessary. For instance, in a struct named Employee, attributes like employeeName, employeeID, and employeeEmail can be simplified to name, ID, and email respectively, since they are already inherently associated with Employee. By removing these repetitive prefixes, the code becomes more concise and easier to read, maintaining its contextual clarity.

Num of instances: 6

### Findings 


<details><summary>Click to show findings</summary>

['[26](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L26-L28)']
```solidity
26:     struct BeaconStateRootProof { // <= FOUND
27:         uint64 timestamp;
28:         bytes32 beaconStateRoot; // <= FOUND
29:         bytes proof;
30:     }
```
['[32](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L32-L34)']
```solidity
32:     struct ValidatorProof { // <= FOUND
33:         uint40 validatorIndex; // <= FOUND
34:         bytes32 validatorRoot; // <= FOUND
35:         bytes proof;
36:     }
```
['[38](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L38-L40)']
```solidity
38:     struct ValidatorFieldsProof { // <= FOUND
39:         ValidatorProof validatorProof; // <= FOUND
40:         bytes32[] validatorFields; // <= FOUND
41:     }
```
['[48](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/BeaconProofsLib.sol#L48-L50)']
```solidity
48:     struct BalanceProof { // <= FOUND
49:         bytes32 pubkeyHash;
50:         bytes32 balanceRoot; // <= FOUND
51:         bytes proof;
52:     }
```
['[23](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/SlasherLib.sol#L23-L25)']
```solidity
23:     struct SlashRequest { // <= FOUND
24:         address operator;
25:         uint96[] slashPercentagesWad; // <= FOUND
26:         address[] vaults;
27:     }
```
['[21](https://github.com/code-423n4/2024-07-karak/tree/main/src/entities/NativeVaultLib.sol#L21-L23)']
```solidity
21:     struct ValidatorDetails { // <= FOUND
22:         
23:         uint40 validatorIndex; // <= FOUND
24:         
25:         ValidatorStatus status;
26:         
27:         uint256 restakedBalanceWei;
28:         
29:         uint64 lastBalanceUpdateTimestamp;
30:     }
```


</details>
