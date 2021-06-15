# OpenZeppelin

## Created by:

- Arcturus

## Summary

- Contracts implement OpenZeppelin Ownable along with a custom Pausable which inherits from OpenZeppelin ownable.

## Recommendations

- Create a folder structure to better understand the scope of each contract and whether it is for mocks/testing or actual functionality
- High Level documentation should be in markdown (not docx - unable to read within github and creates vector for ransomware)
- Contract sometimes uses Custom Pausable contract and in others OpenZeppelin Pausable Contract. Should instead just use OZ contract unless there's a reason for custom contract.

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

- (Possible access control feel free to remove) AXBridge is defined as Ownable with an onlyOwner modifier on its only function `bridgeSafeTransferFrom`. However, `bridgeSafeTransferFrom` uses the AXInterface which is only defined as an abstract contract which wraps the address provided in the function input which is provided by the user. There is the possibility the address provided here can be malicious by the owner (either deliberate or by mistake) and `transferFrom` can make unintended effects. Additionally this contract could face a denial of service/inability to execute due to an unbounded `ids` length in the for loop. This could render the contract useless if the `ids` length is too large and the unknown `transferFrom` is too gas intensive.

#### `BatchSwap.sol`

- (Possible access control feel free to remove) `setWhitelist` can be called by Owner which in theory could set a malicious dApp with an unsafe `bridgeSafeTransferFrom` or other erc20 functions called on whitelisted dApps.

#### `BatchVault.sol`

- Implements OpenZeppelin `onlyOwner` and OZ `whenNotPaused`, overall looks good.
- (Possible access control feel free to remove) Unsure why `getVaultBalance` has `onlyOwner` modifier as it is a readOnly method of contract state.

#### `CKBridge.sol`

- (Possible access control feel free to remove) In contract `CKBridge`, function `bridgeSafeTransferFrom` can be called by anyone.

#### ERC1155Five.sol - ERC721Two.sol

- Seemingly Test contracts, need more clarity if they have any other function

#### TradeSquads.sol

- Uses custom Pausable Contract instead of OZ Pausable contract.
- `awardItem`
  - ? Should this have an onlyOwner modifier?
- `assetTrait`
  - ? Should this have an onlyOwner modifier?
- `getVaultBalance` is a read-only method but has an onlyOwner modifier which doesn't seem necessary or useful(?)
- `sendVaultBalance` owner can send the vault balance to any receiver they call.
