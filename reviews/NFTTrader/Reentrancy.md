# Reentrancy

## By: Arcturus

## Summary

- The contracts use onlyOwner modifiers throughout to control access except for select unknown circumstances.

### Recommendations

-

## Scope

```
├── Docs.docx
└── test
  └── 001_deployment_test.js
└── contracts
  ├── AXBridge.sol
  ├── BatchSwap.sol
  ├── BatchVault.sol
  ├── CKBridge.sol
  ├── ERC1155Five.sol
  ├── ERC1155Four.sol
  ├── ERC1155One.sol
  ├── ERC1155Six.sol
  ├── ERC1155Three.sol
  ├── ERC1155Two.sol
  ├── ERC20Four.sol
  ├── ERC20One.sol
  ├── ERC20Three.sol
  ├── ERC20Two.sol
  ├── ERC721Four.sol
  ├── ERC721One.sol
  ├── ERC721Three.sol
  ├── ERC721Two.sol
  ├── Pausable.sol
  └── TradeSquads.sol
```

## File Review

### `contracts/`

#### `AXBridge.sol`

- AXBridge is defined as Ownable with an onlyOwner modifier on its only function `bridgeSafeTransferFrom`. Although `bridgeSafeTransferFrom` makes an external function call `transferFrom`, on `bridgeSafeTransferFrom` the onlyOwner modifier appears to prevent it from being susceptible to reentrancy. That said, a reetrancy guard would be advisable since this function is executed via a custom interface on the Batchswap.sol contract.

#### `BatchSwap.sol`

- Batchswap
  - createSwapIntent
    - State set after CryptoPunk interface(external function call) check on L#185 but no apparent obvious side effect possible.

#### `BatchVault.sol`

- sendVaultBalance ()
  - Function can only be called by the owner (as a result of OpenZeppelin Ownable) and appears to not be susceptible to reentrancy.

#### `CKBridge.sol`

- `bridgeSafeTransferFrom` can be called by anyone with `CKInterface.transfer()` unclear why. Re-entrancy Guard recommended or another modifier/guard (such as onlyOwner). Not consistent with `bridgeSafeTransferFrom` on the `AXBridge.sol`

#### ERC1155Five.sol - ERC721Two.sol

- Contracts appear to be test contracts implementing standard ERC20, ERC721, a and ERC1155 OpenZeppelin functionality. No external function calls made, awardItem on ERC721 and ERC1155 can be called by any user.

#### TradeSquads.sol

- createSwapIntent() - swapIds.increment() is called after transfers but they are the standard interfaces for ERC20, ERC721, and ERC1155 as long as the contracts themselves aren't malicious.
