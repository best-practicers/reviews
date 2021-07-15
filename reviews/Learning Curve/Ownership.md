# Access Control

## Created by:
Marcel Jackisch

## Summary
The LEARN is minted based on locking DAI (reserve) in the LEARN token contract. 
This happens via simple transfer from the previous DAI owner to the contract.

The contracts seem to work permissionlessly after deployment.
There is no ownership or access control. 

Due to time constraints, `KernelFactory.sol` was not yet analyzed in detail. 
However it likewise lacks permissions and it seems all (`external`) functions can and should accessed publicly without concern.

## Scope
├── contracts
│   ├── BasicERC20.sol
│   ├── KernelFactory.sol
│   ├─[x] LearningCurve.sol
│   ├── PRBMath.sol
│   └── PRBMathUD60x18.sol

## Findings

### `LearningCurve.sol`
none


