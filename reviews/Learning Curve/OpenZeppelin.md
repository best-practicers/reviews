# OpenZeppelin
## Created by: [Kyle Smith](https://github.com/bestape), [@carlfarterson](https://github.com/carlfarterson)

## Summary
This repository is not a complex application of OpenZeppelin and is relatively straightforward.

## File Review

### `contracts/BasicERC20.sol`

Imports OpenZeppelin `token/ERC20/ERC20.sol`:

* The `BasicERC20` contract inherits `ERC20`.

* The constructor aligns with the inherited OpenZeppelin `ERC20` constructor.

* The public function `mint` correctly calls the inherited OpenZepplin `ERC20` _mint function.

### `contracts/KernelFactory.sol`

Imports OpenZeppelin `utils/Counters.sol`:

* Correctly uses `Counters.Counter` not `Counters` directly.

* `batchIdTracker` and `courseIdTracker` both inherit `Counters.Counter`.

* `batchIdTracker` and `courseIdTracker` both only use the `Counters.Counter` library's functions.

Imports OpenZeppelin `token/ERC20/IERC20.sol` and `token/ERC20/utils/SafeERC20.sol`:

* The `KernelFactory` contract doesn't use inheritance.

* Wraps `IERC20` within `SafeERC20`.

* `stable` inherits `IERC20`.

* `stable` calls the `stable.approve` `IERC20` library's function.

* All other `stable` calls use the `SafeERC20` library's functions.

Imports `LearningCurve.sol`.

* Calls an OpenZeppelin `ERC20` library function via `I_LearningCurve`.

* Calls a `LearningCurve` library function via `I_LearningCurve`.

### `contracts/LearningCurve.sol`

Imports OpenZeppelin `token/ERC20/ERC20.sol`, `token/ERC20/IERC20.sol` and `token/ERC20/utils/SafeERC20.sol`:

* The `LearningCurve` contract inherits `ERC20`.

* The public functions `initialise`, `mint` and `mintForAddress` correctly call the inherited OpenZepplin `ERC20` _mint function.

* Wraps `IERC20` within `SafeERC20`.

* `reserve` inherits `IERC20`.

* `reserve` calls use the `SafeERC20` library's functions.

###  `contracts/PBRMath.sol`

* Doesn't use OpenZeppelin.

###  `contracts/PBRMathUD60x18.sol`

* Doesn't use OpenZeppelin.
