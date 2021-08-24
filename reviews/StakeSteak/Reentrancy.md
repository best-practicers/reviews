# Reentrancy
## Commit-SHA: [a3789a6](https://github.com/xam-darnold/steak-public-contracts/commit/a3789a61a54cbda943324abc814932e8d137347d)
## Done by: [mariuspod](https://github.com/mariuspod)
### Reviewed by:

## Summary
* There are 2 severe issues found by slither in `SteakHouse.sol` regarding reentrancy:
  * Reentrancy in SteakHouse.deposit(uint256,uint256) [contracts/SteakHouse.sol#231-256](https://github.com/xam-darnold/steak-public-contracts/blob/a3789a61a54cbda943324abc814932e8d137347d/contracts/SteakHouse.sol#L231-L256):
	  External calls:
	  - user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) [contracts/SteakHouse.sol#238](https://github.com/xam-darnold/steak-public-contracts/blob/a3789a61a54cbda943324abc814932e8d137347d/contracts/SteakHouse.sol#L238)
  * Reentrancy in SteakHouse.withdraw(uint256,uint256) [contracts/SteakHouse.sol#259-272](https://github.com/xam-darnold/steak-public-contracts/blob/a3789a61a54cbda943324abc814932e8d137347d/contracts/SteakHouse.sol#L259-L272):
	  External calls:
	  - user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) [contracts/SteakHouse.sol#266](https://github.com/xam-darnold/steak-public-contracts/blob/a3789a61a54cbda943324abc814932e8d137347d/contracts/SteakHouse.sol#L266)

* However, due to the fact that the issue could only be exploited if the steak token was manipulated during deployment it only could be an issue the first time this is deployed or for every fork of it:
  * [constructor assignment](https://github.com/xam-darnold/steak-public-contracts/blob/master/contracts/SteakHouse.sol#L78)
  * [field definition as immutable](https://github.com/xam-darnold/steak-public-contracts/blob/master/contracts/SteakHouse.sol#L45)

## Recommendations
* Don't use the `immutable` modifier for the steak token variable, instead first deploy the steak token and then hardcode its address into the SteakHouse.sol so that there is less risk during deployments that a malicious token is accidently deployed which could take advantage of the reentrancy problem.
* Use a mutex variable to lock repetitive calls in #deposit and #withdraw or use [OZ ReentrancyGuard](https://docs.openzeppelin.com/contracts/4.x/api/security#ReentrancyGuard)
* Use the `Checks-Effects-Interactions` pattern so that state changes are done before external calls: [#withdraw](https://github.com/xam-darnold/steak-public-contracts/blob/a3789a61a54cbda943324abc814932e8d137347d/contracts/SteakHouse.sol#L267-L270)

## Full Slither reports

### SteakHouse.sol
* [main report](reports/slither-main.md)
