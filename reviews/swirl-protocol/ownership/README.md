# swirl-protocol documentation / ownership


## Summary
Swirl-protocol uses its own implementation of industry standard Openzeppelin AccessControl library, defined as `DCAAccessControl.sol`.
Tests defined in `DCAPoolFacade.test.ts` pass correctly on granting, withdrawing and restricting access roles in contract functions.
Swirl-protocol is centralized around defined roles. Users need to fully trust these roles to always act in their best interest.
Compromise of any of defined roles could put user funds at risk. 

## Structure of Access Control

Contract has admin role, four main access roles and one role for K3per network used to evaluate pools.

```
DEFAULT_ADMIN_ROLE
EXECUTOR_ROLE
REGISTRAR_ROLE
SCHEDULER_ROLE
VAULT_ROLE
```

## Admin

**ADMIN** role is set up during contract creation by msg.sender and used as `onlyAdmin` modifier inside of a contract.

**ADMIN** role is responsible for managing contract operations involving user funds by setting Vaults properties.

**ADMIN** has strict control over what happens with user payments, savings and investments. This is expected in a contract like swirl-protocol, however, user should be aware how much of control is given to contract, as core functionality is defined top down *(Vault strategies, fees, minimum purchase, slippage tolerance)*.

In core contracts **DEFAULT_ADMIN_ROLE** can: 

`DCAPoolFacade.sol`
* Set the minimum bond required by a keeper to call this contract
* Enables/Disables keeper network integration
* Collect unused balance from this contract
	
`DCAPoolFactory.sol`
* Create a new DCA pool
* Set the buy strategy used by newly create vaults 
* Enables a token to be used as base in new vaults
* Enables a token to be used as order in new vaults
	
`DCAScheduler.sol`
* Set the minimum total purchase quantity for this pool to become ready
* Set fees charged by the protocol. Maximum 3%
* Set recipient for fees
	
`DCAVault.sol`
* Collect unused balance from this pool
* Set the minimum order quantity for this pool
* Sets the new withdrawal strategy.
	
`ChainLinkGasCalculator.sol`
* Add a feed for the token provided

In strategies contracts **DEFAULT_ADMIN_ROLE** can:

`OneInchBuyStrategy.sol`
* Enable base token for swaps
* Set slippage tolerance
* Set 1 inch parts for split calculation

## Executor

**EXECUTOR** role is setup during contract creation and used as `onlyExecutor` modifier inside of a contract.

**EXECUTOR** has only one task in swirl-protocol, to evaluate a swap effect on given Vault.

**EXECUTOR**, depending on succesfull evaluation, implements Fill or Kill and calls coresponding Vault.

Order filling for vaults is directly dependent on **EXECUTOR_ROLE**.

In core contracts **EXECUTOR** can:
	
`DCAScheduler.sol`
* Performs an evaluation to effect a swap

## Registrar
	
**REGISTRAR** role is setup during contract creation and used as `onlyRegistrar` modifier inside of a contract.

**REGISTRAR** has only one task in swirl-protocol, to insert created pool into the register.

**REGISTRAR** has no custody of tokens itself.

In core contracts **REGISTRAR** can:

`DCAPoolFacade.sol`
* Insert a pool into the register

## Scheduler
	
**SCHEDULER** role is setup during contract creation and used as `onlyScheduler` modifier inside of a contract.

**SCHEDULER** has only one task in swirl-protocol, to notify vault of performed execution of tokens exchange.

**SCHEDULER** has indirect control over user balance by pushing changes to cumulative purchase results.

In core contracts **SCHEDULER_ROLE** can:

`DCAVault.sol`
* Notify vault of a performed execution

## Vault
	
**VAULT** role is setup during contract creation and used as `onlyVault` modifier inside of a contract.

**VAULT** controls what pools are scheduled to run with user tokens. **VAULT** can add and edit pools.

**VAULT** has indirect control over user funds by defining what strategies are used for token purchases. 

In core contracts **VAULT_ROLE** can:

`DCAScheduler.sol`
* Adds a pool to the scheduler
* Edit the schedules for a pool


## Recommendations
* High documentation transparency regarding vault strategies (What, why, when).

## Scope
```
contracts/
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
