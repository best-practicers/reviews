# Documentation
## Created by: [andytudhope](https://github.com/andytudhope/)

_Disclaimer: I wrote the documentation, so am deeply biased :)_

## Summary

* The [natspec](https://docs.soliditylang.org/en/v0.8.4/natspec-format.html) documentation standard is uniformly used.
* A custom documentation standard is used.
* Available comments provide the basic development outline.
* Documentation is only presented in English. 
* These contracts are simple, especially in terms of ownership (there are no privileged roles), access and logic.

## Scope

* Public documentation [here](https://kernel.community/en/guiding/contracts).
* Contracts [here](https://github.com/kernel-community/learning-curve).
```
├── contracts
    ├── KernelFactory.sol
    ├── LearningCurve.sol
└── tests
```

## File Review

### Public Documentation

* Clear visual representation of the potential flows of value through the two core contracts.
* Each method and event is documented and up-to-date.
* None of the structs, mappings, and other stored declarations are documented.
* There is some insight provided into the choice for constant values like `k` provided at the end of the document.
* The spirit, intention and rationale of the work is clearly discussed.

---

### `contracts/`
#### `KernelFactory.sol`

* Undocumented declarations generally have short descriptions in the comments above about their function and reason for being.
* Natspec is used uniformly throughout.
* Two interfaces - for a Yearn Vault and for the Learning Curve - are declared, but undocumented (apart from informally so in the leading visualization in the Public Documentation).
* Contains numerous `get` functions, all well documented. The only concern is potentially `getEligibleAmounts` which can alter the contract's state, as opposed to the other `get` functions. This could likely be refactored.

#### `LearningCurve.sol`

* Well documented, Natspec used uniformly throughout.
* Biggest concern is the use of `magic` PRBMAthUD60x18 library for natural logarithms. Comments like `x the number to be magic'd` are not very helpful. However, the [PRBMath library](https://github.com/hifi-finance/prb-math) itself is fairly well documented and doing natural logarithms on chain is just a complex thing to get right.
* `getBurnableForReserveAmount` also appears to be a strange way of handling burns. Ideally, learners could just send LEARN to the contract, have it be burnt, have the contract calculate how much DAI to return and be done with it. On further inspection, this is not possible on-chain due to the complexity of the calculation, given the curve goes according to a natural logarithmic decay. This means the logic has to happen in a fairly round-about manner, which is not ideal. However, this seems the only tractable solution for now and I have no good recommendations on how to improve it.