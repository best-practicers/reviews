# Documentation
## Created by: [bestape](https://github.com/bestape)

## Summary
* The [natspec](https://docs.soliditylang.org/en/v0.7.5/natspec-format.html) documentation standard is not used.
* It is unclear if any documentation standard is used.
* Available comments provide the basic development outline, and are presented in multiple languages. 
* As a swap, these contracts are more complex than traditional NFT contracts.
* The complexity of a swap makes it all the more important to follow documentation standards.
* Names like ERC1155Five that add an index but not a descriptor are hard to understand.

## Scope
```
├── Docs.docx
├── contracts
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
└── test
    └── 001_deployment_test.js
```

## File Review
### `Docs.docx`
* Not .md file.
* README.md is Git convention.
* Did not open to review. 
* The .docx format is unsafe, due to macros.
* Could have created a VM in a GUI to review the .docx in a silo, but did not.
* This review was done in a CLI ssh environment.
* The .docx format is unusable in CLI ssh environments.

---
### `contracts/`
#### `BatchSwap.sol`
* Documentation could help with this, or function wrappers, but some of the for loops are functions without names. 
* A comment with the same words as the name of the function it describes is unhelpful.
* Uncertain about script flow, especially because there are multiple get functions.

#### `TradeSquads.sol`
* Trait array objects not given names.
* Names like nRandRes are hard to understand.
* For and while loops not given names.

--- 
### `test/`
#### `001_deployment_test.js`
* 1903 lines of code is too long, and this script should be split into multiple scripts.
* Given the length of the script, as well as the async functions, I cannot determine script flow.
