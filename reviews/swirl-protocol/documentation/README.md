# documentation
## By: [carlfarterson](https://github.com/carlfarterson), [kjr217](https://github.com/kjr217)

## Summary / Recommendations
Overall, ...

### Recommendations
* Our first recommendation is ..
* Flow charts of how the contracts interact would be beneficial.

## Scope
```
├── README.md
└── contracts
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
* addFeed() Line 45 misspelt "whether"
* addFeed() Perhaps provide a more specific definition of quote

#### `DCAPoolFacade.sol`
* definitions of state variables would imprve readiblity
* onlyKeeper() modifier definition

#### `DCAPoolFactory.sol`
* Add comments for web assembly within `createPool()`.
#### `DCAScheduler.sol`
* view and pure functions missing return natspec tag (ready(), \_ready(), getSchedule(), maxCycles())
#### `DCAVault.sol`
* define Account struct
* \_processBalanceChange() newTotalQty parameter could be explained better.

### `contracts/strategies/`
#### `BadgerSettBuyStrategy.sol`
N/A
#### `OneInchBuyStrategy.sol`
* definition of state variables

### `contracts/libs`
#### `Compression.sol`
* title, author, notice tags?
#### `DCAAccessControl.sol`
* Add natspec comments to `onlyVault()` and `onlyScheduler()` modifiers, `addVault()`, `removeVault()`, `addScheduler()`, and `removeScheduler()` functions. 
#### `PeriodAware.sol`
N/A
#### `PriceFeedConsumer.sol`
N/A
#### `SlidingWindow.sol`
* title, author, notice tags?
* return natspec tag missing on next(), peek() and toArray()
#### `Types.sol`
* title, author, notice tags?
