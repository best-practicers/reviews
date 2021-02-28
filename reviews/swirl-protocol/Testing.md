# Testing
## Created by: [hollygrimm](https://github.com/hollygrimm)
## Reviewed by: [carlfarterson](https://github.com/carlfarterson)

## Summary
* Unit test coverage is excellent
* Integration tests cover the end-to-end interactions of all the contracts
* Excellent usage of Alchemy to fork the mainnet from a specific block number for integration testing

## Recommendations
N/A

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
Each of the contracts, `DCAPoolFacade.sol`, `DCAPoolFactory.sol`, `DCAScheduler.sol`, `DCAVault.sol` are being thoroughly tested using [hardhat-waffle](https://hardhat.org/plugins/nomiclabs-hardhat-waffle.html).

Tests using the chai matchers `calledOnContract` and `calledOnContractWith` have been separated out into separate files suffixed 'WithMock'. These tests are utilizing the waffle provider directly. See more details on the issue [here](https://github.com/nomiclabs/hardhat/issues/638)

## Integration Testing
All the integration tests call `resetFork()` from `utils/integration.ts` which uses [Alchemy](https://alchemyapi.io) to fork from a specific block number.

### 1Inch.test.ts
Deploys and tests the [1Inch](https://1inch.exchange/#/) buy strategy

### GasCalculator.test.ts
Deploys and tests the [Chainlink](https://chain.link) gas calculator

### PoolsE2E.test.ts
Deploys and tests the full end-to-end pooling
