# 1. Implementation of Balance Check for Withdrawals in SlashStore Contract

## Description

The `SlashStore.sol` contract allows the owner to withdraw funds to a specified address. However, it currently lacks a balance check to prevent the owner from withdrawing more Ether than the contract holds. Implementing this check will ensure the contract maintains a proper balance and prevents erroneous or malicious withdrawals:

https://github.com/code-423n4/2024-07-karak/blob/f5e52fdcb4c20c4318d532a9f08f7876e9afb321/src/SlashStore.sol#L32-L35

```solidity
    function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {
        Address.sendValue(payable(to), weiAmount);
        emit NodeETHWithdrawn(address(this), to, weiAmount);
    }
```

## Recommendations

Add a check in the `withdraw()` function to ensure the withdrawal amount does not exceed the contract's current balance:

```solidity

function withdraw(address to, uint256 weiAmount) external nonReentrant onlyOwner {
    if (address(this).balance < weiAmount) revert InsufficientBalance();
    Address.sendValue(payable(to), weiAmount);
    emit NodeETHWithdrawn(address(this), to, weiAmount);
}
```