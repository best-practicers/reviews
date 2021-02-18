# testing
## By: [hollygrimm](https://github.com/hollygrimm)

## Summary & Recommendations
* Unit test coverage is excellent
* Integration tests cover the end-to-end interactions of all the contracts
* Excellent usage of Alchemy to fork the mainnet from a specific block number for integration testing

## Scope
```
├── README.md
└── test
    └── integration
        ├── 1Inch.test.ts
        ├── GasCalculator.test.ts
        └── PoolsE2E.test.ts        
    └── unit
        ├── DCAPoolFacade.test.ts
        ├── DCAPoolFacadeWithMock.test.ts
        ├── DCAPoolFactory.test.ts
        ├── DCAPoolFactoryWithMock.test.ts
        ├── DCAScheduler.test.ts
        ├── DCASchedulerWithMock.test.ts
        ├── DCAVault.test.ts
        ├── DCAVaultWithMock.test.ts
        ├── Gas.test.ts
        ├── PriceFeedConsumer.test.ts
        └── SlidingWindow.test.ts
    └── utils
        ├── integration.ts
        └── utils.ts
```

## Unit Testing
Each of the contracts, `DCAPoolFacade.sol`, `DCAPoolFactory.sol`, `DCAScheduler.sol`, `DCAVault.sol` are being thoroughly tested using hardhat-waffle.

Tests using the chai matchers `calledOnContract` and `calledOnContractWith` have been separated out into separate files suffixed 'WithMock'. These tests are utilizing the waffle provider directly. See more details on the issue here: https://github.com/nomiclabs/hardhat/issues/638

## Integration Testing
ALl the integration tests call `resetFork()` from `utils\integration.ts` which uses Alchemy to fork from a specific block number.

### 1Inch.test.ts
Deploys and tests the 1Inch buy strategy

### GasCalculator.test.ts
Deploys and tests the Chainlink gas calculator

### PoolsE2E.test.ts
Deploys and tests the full end-to-end pooling





