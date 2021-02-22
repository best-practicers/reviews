# swirl-protocol documentation / ownership

## Summary
* Swirl-protocol uses its own implementation of industry standard Openzeppelin AccessControl library, defined as `DCAAccessControl.sol`.
* Tests defined in `DCAPoolFacade.test.ts` pass correctly on granting, withdrawing and restricting access roles in contract functions.
* Swirl-protocol is centralized around defined roles. Users need to fully trust these roles to always act in their best interest.
* Compromise of any of defined roles could put user funds at risk. 

## Recommendations
* High documentation transparency regarding vault strategies (What, why, when).

## Structure of Access Control

Contract has admin role, four main access roles and one role for K3per network used to evaluate pools.

```
DEFAULT_ADMIN_ROLE
EXECUTOR_ROLE
REGISTRAR_ROLE
SCHEDULER_ROLE
VAULT_ROLE
```

Role | Usage (as modifier) | About | Relationship with $ | Interaction with contracts
|---|---|---|---|---|
|**ADMIN**| `onlyAdmin()` | managing contract operations involving user funds by setting Vaults properties | Direct control, manages user payments, saving, and investment |<ul>`DCAPoolFacade.sol`<li>Set the minimum bond required by a keeper to call this contract</li><li>Enables/Disables keeper network integration</li><li>Collect unused balance from this contract</li></ul><ul>`DCAPoolFactory.sol`<li>Create a new DCA pool</li><li>Set the buy strategy used by newly create vaults </li><li>Enables a token to be used as base in new vaults</li><li>Enables a token to be used as order in new vaults</li></ul><ul>`DCAScheduler.sol`<li>Set the minimum total purchase quantity for this pool to become ready</li><li>Set fees charged by the protocol. Maximum 3%</li><li>Set recipient for fees</li></ul>	<ul>`DCAVault.sol`<li>Collect unused balance from this pool</li><li>Set the minimum order quantity for this pool</li><li>Sets the new withdrawal strategy.</li></ul><ul>`ChainLinkGasCalculator.sol`<li>Add a feed for the token provided</li></ul><ul>`strategies/OneInchBuyStrategy.sol`<li>Enable base token for swaps</li><li>Set slippage tolerance</li><li>Set 1 inch parts for split calculation</li></ul>
|**EXECUTOR**| `onlyExecutor()` | Evaluate swap effect on a vault by implementing Fill/Kill and calls corresponding vault | Indirect control, order filling is dependent on this role |  <ul> `DCAScheduler.sol`<li>Performs an evaluation to effect a swap</li></ul>
|**REGISTRAR**| `onlyRegistrar()` | Inserts pools into the registrar | No custody of tokens | <ul>`DCAPoolFacade.sol`<li>Insert a pool into the register</li></ul>
|**SCHEDULER**| `onlyScheduler()` | Notifies vault of performed execution of token exchange | Indirect control, pushes changes to cumulative purchase results | <ul>`DCAVault.sol`<li>Notify vault of a performed execution</li></ul>
|**VAULT**| `onlyVault()` | Controls which pools are scheduled to run with user tokens by adding/editing pools|Indirect control, defines which strategies are used for token purchases | <ul>`DCAScheduler.sol`<li>Adds a pool to the scheduler</li><li>Edit the schedules for a pool</li></ul>

### TODO: Link contracts that use each modifier
