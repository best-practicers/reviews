# documentation
## By: [Kevin Keaveney](https://github.com/kkeaveney) & [Ethan Jones](https://github.com/0xEthan)

## Summary / Recommendations
Checks, Effects, Interactions pattern has been used throughout the contracts to prevent reentrancy. All events emitted have been
ordered accordingly to mitigate reentracy attacks.

### Recommendations
* Our first suggestion is .. Use of Open Zepplin OpenZeppelin ReentrancyGuard modifier


## Scope
```
├── README.md
└── contracts
    └── ext
        ├── Timelock.sol
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
* SafeERC20 for IERC20 is used in withdraw
* Withdraw function is protected with an onlyAdmin modifier, so re-entrancy is not a risk.
#### `DCAPoolFactory.sol`
* N/A
#### `DCAScheduler.sol`
* SafeERC20 for IERC20 is used in evaluate
#### `DCAVault.sol`
* SafeERC20 for IERC20 is used createAccount, _processBalanceChange, withdraw, collectDust
* Checks, Effects, Interactions pattern in createAccount, editAccount, _processBalanceChange
* AccountModified event (editAccount) is orderred accordingly to prevent reentrancy
* Withdraw function has high damage potential, and a lock could be considered to protect against unforseen or not-yet-discovered attack vectors.

### `contracts/ext/`
#### `Timelock.sol`
* An external call to a target address cannot be reentered as the call must come from admin
* ExecuteTransaction event is orderred accordingly to prevent reentrancy

### `contracts/strategies/`
#### `BadgerSettBuyStrategy.sol`
N/A
#### `OneInchBuyStrategy`
* The riskiest function, _swap, is well protected because the funds are transferred to the contract before execution of the swap, and it is interacting with a known, hard-coded contract. My only suggestion would be to turn _oneInch to a constant.
### `contracts/libs`
#### `Compression.sol`
N/A
#### `DCAAccessControl.sol`
N/A
#### `PeriodAware.sol`
N/A
#### `PriceFeedConsumer.sol`
N/A
#### `SlidingWindow.sol`
N/A
#### `Types.sol`
N/A
>>>>>>> Stashed changes
