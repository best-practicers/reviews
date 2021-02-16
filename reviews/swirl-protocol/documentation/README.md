# documentation
## By: [carlfarterson](https://github.com/carlfarterson), [kjr217](https://github.com/kjr217)

## Summary / Recommendations
Overall, ...

### Recommendations
* Our first recommendation is ..
* Our sescond recommendation is ... 

## Scope
```
├── README.md
└── contracts
    ├── ChainLinkGasCalculator.sol
    ├── ChainLinkGasCalculator.sol
    ├── DCAPoolFacade.sol
    ├── DCAPoolFactory.sol
    ├── DCAScheduler.sol
    ├── DCAVault.sol
    └── strategies
        ├── BadgerSettBuyStrategy.sol
        └── OneInchBuyStrategy.sol
    └── libs
        ├── Compression.sol
        ├── DCAAccessControl.sol
        ├── PeriodAware.sol
        ├── PriceFeedConsumer.sol
        ├── SlidingWindow.sol
        └── Types.sol
```

## File Review
### `contracts/`
#### `ChainLinkGasCalculator.sol`
N/A
#### `DCAPoolFacade.sol`
N/A
#### `DCAPoolFactory.sol`
Add comments for web assembly within `createPool()`.
#### `DCAScheduler.sol`
N/A
#### `DCAVault.sol`
N/A

### `contracts/strategies/`
#### `BadgerSettBuyStrategy.sol`
N/A
#### `OneInchBuyStrategy.sol`
N/A

### `contracts/libs`
#### `Compression.sol`
N/A
#### `DCAAccessControl.sol`
Add natspec comments to `onlyVault()` and `onlyScheduler()` modifiers, `addVault()`, `removeVault()`, `addScheduler()`, and `removeScheduler()` functions. 
#### `PeriodAware.sol`
N/A
#### `PriceFeedConsumer.sol`
N/A
#### `SlidingWindow.sol`
N/A
#### `Types.sol`
N/A
