# documentation
## By: [carlfarterson](https://github.com/carlfarterson), [kjr217](https://github.com/kjr217)

## Summary & Recommendations
* One misspelling in comments.
* Many contracts are missing full natspec coverage.
* __RECOMMENDATION__: Apply changes found below.
* __RECOMMENDATION__: Add flow charts of how contracts interact with one another.  [Solidity Visual Developer](https://marketplace.visualstudio.com/items?itemName=tintinweb.solidity-visual-auditor) and [Surya](https://github.com/ConsenSys/surya) are two popular Consensys Diligence-powered tools which provide visual analysis of smart contracts.

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
---
### `contracts/`
#### `ChainLinkGasCalculator.sol`
* [Line 45](https://github.com/tonic-finance/swirl-protocol/blob/87dfa63222fffe245ac66258c7afb9a9084e7e1c/contracts/ChainLinkGasCalculator.sol#L45) misspelled "whether"

#### `DCAPoolFacade.sol`
* Define state variables
* Add definition to `onlyKeeper()`

#### `DCAPoolFactory.sol`
* Add comments to explain web assembly within `createPool()`

#### `DCAScheduler.sol`
* Several functions missing `@return` natspec tag
    * `ready()`
    * `_ready()`
    * `getSchedule()`
    * `maxCycles()`

#### `DCAVault.sol`
* Define `Account` struct
---
### `contracts/strategies/`
#### `BadgerSettBuyStrategy.sol`
N/A

#### `OneInchBuyStrategy.sol`
* Define state variables

---
### `contracts/libs/`
#### `Compression.sol`
* Add `@title`, `@author`, and `@notice` natspec tags

#### `DCAAccessControl.sol`
* Add natspec comments to
    * `onlyVault()`
    * `onlyScheduler()`
    * `addVault()`
    * `removeVault()`
    * `addScheduler()`
    * `removeScheduler()`

#### `PeriodAware.sol`
N/A

#### `PriceFeedConsumer.sol`
N/A

#### `SlidingWindow.sol`
* Add `@title`, `@author`, and `@notice` natspec tags
* Several functions missing `@return` natspec tag
    * `next()`
    * `peek()`
    * `toArray()`

#### `Types.sol`
* Add `@title`, `@author`, and `@notice` natspec tags
