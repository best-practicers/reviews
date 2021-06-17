# Testing


## Summary

- I could not get these tests to run properly - I'm not sure if there was additional config or project files that were removed for the audit. It would have helped if these had been included.

### Recommendations
- Looks like the test file starts out with a bunch of helper functions. It might be nice to label this or split them out.
- In general the test code is repetitive and could definitely be refactored.
- While the deployment tests seem comprehensive, there is no attempt at any other kind of testing. Unit tests or a more structured approach to test writing would make it much easier to see where coverage is lacking.

## Scope

```
├── docs.docx
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

### `tests/`
#### `001__deployment_test.js`
- L66 Examples of duplicate blocks in the switch statement - this could be simplified by extracting the token lists.
- L265 These two conditionals could be refactored by using a variable in place of delegatedAmounts[i]
- L281 These two blocks are also identical apart from the tokenId being used