# Access Control

## Created by:
Ben Beale

## Summary
The scope of this review encompasses access control for both `LearningCurve.sol` and `KernelFactory.sol`. 

The LEARN is minted based on locking DAI (reserve) in the LEARN token contract. 
This happens via simple transfer from the previous DAI owner to the contract.

The contracts seem to work permissionlessly after deployment.
There is no ownership or access control. 

The `LearningCurve` contract was covered by Marcel Jackisch, and I reviewed `KernelFactory`.
 
Similar to `LearningCurve`, the `KernelFactory` contract lacks permissions and consists of many `view` functions which make no state changes. All (`external`) calls appear to behave as expected.

One area that caught my attention was the internal function `getEligibleAmount`. Because it appears to modify state variables, it may make sense to factor out the calculation, state changing and event emitting components into a separate internal function, while keeping the existing function, making it a `view` and adding an `external` modifier for consistency with the other getters. 

## Scope
```
├── contracts
│   ├── BasicERC20.sol
│   ├─[x] KernelFactory.sol
│   ├── LearningCurve.sol
│   ├── PRBMath.sol
│   └── PRBMathUD60x18.sol
```
## Findings

### `KernelFactory.sol`
getEligibleAmount
- Consider splitting into multiple functions, restricting access where the state changing operations are performed, and make the existing function an external view like the other getters. 
