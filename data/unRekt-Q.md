## Title
Missing `address(0)` check in `withdraw` function of `NativeNode.sol`, funds can't be recovered

## Vulnerability Details

`withdraw` function of `NativeNode.sol` do not check for `address(0)` for `address to`.

If funds are deposited in `0` address then it is unrecoverable.

```solidity
    function withdraw(address to, uint256 weiAmount)//@audit - missing 0 address check
        external
        onlyOwner
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_NODE_WITHDRAW)
    {
        Address.sendValue(payable(to), weiAmount);
        emit NodeETHWithdrawn(address(this), to, weiAmount);
    }
```

## Impact

Funds deposited to a `0` address is not recoverable.

## Code snippet

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/NativeNode.sol#L39-L47

## Tools Used 

Manual review

## Recommended Mitigation
Implement o address check

```solidity
if(to==address(0)) revert ZeroAddresspassed();
```


## Title
No `0` address checks in `deposit` functions of `Vault.sol`, can lead to loosing of funds.

## Summary

No checks for `address(0)`

## Vulnerability Details

In both `deposit` function of `Vault.sol`, `address to` is not checked for `0` address. If funds are deposited in `0` address then it is unrecoverable.

```solidity
    function deposit(uint256 assets, address to)
    
        public
        override(ERC4626, IVault)
        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT)
        nonReentrant
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        return super.deposit(assets, to);
    }
```
```solidity
    function deposit(uint256 assets, address to, uint256 minSharesOut)
    
        external
        nonReentrant
        whenFunctionNotPaused(Constants.PAUSE_VAULT_DEPOSIT_SLIPPAGE)
        returns (uint256 shares)
    {
        if (assets == 0) revert ZeroAmount();
        shares = super.deposit(assets, to);
        if (shares < minSharesOut) revert NotEnoughShares();
       
    }
```
## Impact

Funds deposited to a `0` address is not recoverable.

## Code snippet

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L78-L87

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/Vault.sol#L94-L103

## Tools Used 

Manual review

## Recommended Mitigation

Check for `0` address. 
E.g.
```solidity
if(to==address(0)) revert ZeroAddresspassed();
```
