** Description
The project does not check address(0) when initializing parameters _owner in NativeNode.sol, _manager in Core.sol, _operator and _owner in NativeVault.sol, _owner in SlashingHandler.sol, _owner in SlashStore.sol, _operator and _owner in Vault.sol.

** Impact
If the project is initialized with the wrong parameters, it will have to be deployed again.

** POC
https://github.com/code-423n4/2024-07-karak/blob/main/src/NativeNode.sol#L29
https://github.com/code-423n4/2024-07-karak/blob/main/src/Core.sol#L64
https://github.com/code-423n4/2024-07-karak/blob/main/src/NativeVault.sol#L54-L72
https://github.com/code-423n4/2024-07-karak/blob/main/src/SlashingHandler.sol#L34
https://github.com/code-423n4/2024-07-karak/blob/main/src/SlashStore.sol#L21
https://github.com/code-423n4/2024-07-karak/blob/main/src/Vault.sol#L59-L69

** Recommendations
Core.sol:

+        require(_manager!=address(0));
         _initializeOwner(msg.sender);

NativeNode.sol:

+        require(_owner!=address(0));
        _initializeOwner(_owner);

NativeVault.sol:
+        require(_owner!=address(0) && _operator!=address(0));
        _initializeOwner(_owner);

SlashingHandler.sol:
+        require(_owner!=address(0));
        _initializeOwner(owner);

SlashStore.sol:
+        require(_owner!=address(0));
        _initializeOwner(_owner);

Vault.sol:
+        require(_owner!=address(0) && _operator!=address(0));
        _initializeOwner(_owner);