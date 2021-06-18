# Testing

Created by: Anthony Graignic
Date: 2021-06-17
Commit ID(NFTTrader.io): bc3cca51004b903e4e6e3495f5bf53875ea59fd6

## Summary

- The single test file only concerns `BatchSwap.sol` contract and no tests levels are specified.
- The project was provided with basic instructions in Docs.docx on how to execute tests and without compilation/testing chain, nor package management i.e. `package.json`. After several tries and unfortunately, I wasn't able to make the tests work.

## Recommendations

- The test file contains utilitary/helper methods that should be in another file to clarify the test file.
- The test "Deploy Smart Contracts" doesn't contain assertions and should be moved to a `before ()` method if only used to deploy contracts.
- The tests could use the Arrange, Act and Assert (AAA) pattern to gain readibility.

## Scope

```
├── Docs.docx
└── test
  └── 001_deployment_test.js
```

## File Review

### `tests/`

#### `001_deployment_test.js`

- L391 - No assertions is done in "One-to-One ERC721"
- L505 - No assertions is done in "One-to-Many ERC721 swap"
