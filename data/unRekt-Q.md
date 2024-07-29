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
