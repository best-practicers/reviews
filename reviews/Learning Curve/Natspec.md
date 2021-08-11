# Natspec
## By: [@rihp](https://github.com/rihp),[@carlfarterson](https://github.com/carlfarterson)

## Summary


## Scope
```
├── contracts
    ├── BasicERC20.sol
    ├── KernelFactory.sol
    ├── LearningCurve.sol
    ├── PRBMath.sol
    └── PRBMathUD60x18.sol
```

## File Review
### `LearningCurve.sol`
* Add `@returns` tags to `getBurnableForReserveAmount()` and `getMintableForReserveAmount()`

### `KernelFactory.sol`
* Interfaces `I_Vault` and `I_LearningCurve` could either use natspec, or be imported from another file.
* `redeem()`, `verify()`, and `mint()` could utilize `@dev` to shorten the notice and effectively display developer-specific documentation.

- Indentation on line [363](https://github.com/kernel-community/learning-curve/blob/61fea3584a920b33dab3753dd08cea1872284bdd/contracts/KernelFactory.sol#L363)
