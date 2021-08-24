```bash
~/steak-public-contracts$ slither contracts/SteakHouse.sol

Reentrancy in SteakHouse.deposit(uint256,uint256) (contracts/SteakHouse.sol#231-256):
	External calls:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#238)
		- returndata = address(token).functionCall(data,SafeERC20: low-level call failed) (contracts/ERC20/SafeERC20.sol#71)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#296)
		- steak.safeTransfer(_to,steakTokenBalance - pendingHarvestFee) (contracts/SteakHouse.sol#297)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#300)
		- steak.safeTransfer(_to,_amount - pendingHarvestFee) (contracts/SteakHouse.sol#301)
	- pool.stakingToken.safeTransferFrom(address(msg.sender),address(this),_amount) (contracts/SteakHouse.sol#244-248)
	- pool.stakingToken.safeTransfer(owner(),pendingWithdrawFee) (contracts/SteakHouse.sol#249)
	External calls sending eth:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#238)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
	State variables written after the call(s):
	- pool.stakingTokenTotalAmount += amountToStake (contracts/SteakHouse.sol#252)
	- user.amount += amountToStake (contracts/SteakHouse.sol#251)
	- user.rewardDebt = user.amount * pool.accSteakPerShare / 1e12 (contracts/SteakHouse.sol#253)
Reentrancy in SteakHouse.withdraw(uint256,uint256) (contracts/SteakHouse.sol#259-272):
	External calls:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#266)
		- returndata = address(token).functionCall(data,SafeERC20: low-level call failed) (contracts/ERC20/SafeERC20.sol#71)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#296)
		- steak.safeTransfer(_to,steakTokenBalance - pendingHarvestFee) (contracts/SteakHouse.sol#297)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#300)
		- steak.safeTransfer(_to,_amount - pendingHarvestFee) (contracts/SteakHouse.sol#301)
	External calls sending eth:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#266)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
	State variables written after the call(s):
	- pool.stakingTokenTotalAmount -= _amount (contracts/SteakHouse.sol#268)
	- user.amount -= _amount (contracts/SteakHouse.sol#267)
	- user.rewardDebt = user.amount * pool.accSteakPerShare / 1e12 (contracts/SteakHouse.sol#269)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities

SteakHouse.pendingSteak(uint256,address) (contracts/SteakHouse.sol#185-202) performs a multiplication on the result of a division:
	-steakReward = multiplier * steakPerSecond * pool.allocPoint / totalAllocPoint (contracts/SteakHouse.sol#197-198)
	-accSteakPerShare += steakReward * 1e12 / pool.stakingTokenTotalAmount (contracts/SteakHouse.sol#199)
SteakHouse.updatePool(uint256) (contracts/SteakHouse.sol#213-228) performs a multiplication on the result of a division:
	-steakReward = multiplier * steakPerSecond * pool.allocPoint / totalAllocPoint (contracts/SteakHouse.sol#224-225)
	-pool.accSteakPerShare += steakReward * 1e12 / pool.stakingTokenTotalAmount (contracts/SteakHouse.sol#226)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#divide-before-multiply

SteakHouse.safeRewardTransfer(address,uint256) (contracts/SteakHouse.sol#288-303) uses a dangerous strict equality:
	- steakTokenBalance == 0 (contracts/SteakHouse.sol#291)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#dangerous-strict-equalities

SteakHouse.deposit(uint256,uint256).pendingWithdrawFee (contracts/SteakHouse.sol#240) is a local variable never initialized
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-local-variables

SteakHouse.changeEndTime(uint32) (contracts/SteakHouse.sol#86-88) should emit an event for: 
	- endTime += addSeconds (contracts/SteakHouse.sol#87) 
SteakHouse.setSteakPerSecond(uint256,bool) (contracts/SteakHouse.sol#102-107) should emit an event for: 
	- steakPerSecond = _steakPerSecond (contracts/SteakHouse.sol#106) 
SteakHouse.add(uint16,IERC20,bool) (contracts/SteakHouse.sol#117-137) should emit an event for: 
	- totalAllocPoint += _allocPoint (contracts/SteakHouse.sol#127) 
SteakHouse.set(uint256,uint16,bool) (contracts/SteakHouse.sol#141-151) should emit an event for: 
	- totalAllocPoint = totalAllocPoint - poolInfo[_pid].allocPoint + _allocPoint (contracts/SteakHouse.sol#149) 
SteakHouse.setHarvestFee(uint256) (contracts/SteakHouse.sol#159-162) should emit an event for: 
	- harvestFee = _harvestFee (contracts/SteakHouse.sol#161) 
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-events-arithmetic

SteakHouse.setFeeReceiver(address)._feeReceiver (contracts/SteakHouse.sol#164) lacks a zero-check on :
		- feeReceiver = _feeReceiver (contracts/SteakHouse.sol#165)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation

Reentrancy in SteakHouse.deposit(uint256,uint256) (contracts/SteakHouse.sol#231-256):
	External calls:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#238)
		- returndata = address(token).functionCall(data,SafeERC20: low-level call failed) (contracts/ERC20/SafeERC20.sol#71)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#296)
		- steak.safeTransfer(_to,steakTokenBalance - pendingHarvestFee) (contracts/SteakHouse.sol#297)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#300)
		- steak.safeTransfer(_to,_amount - pendingHarvestFee) (contracts/SteakHouse.sol#301)
	- pool.stakingToken.safeTransferFrom(address(msg.sender),address(this),_amount) (contracts/SteakHouse.sol#244-248)
	- pool.stakingToken.safeTransfer(owner(),pendingWithdrawFee) (contracts/SteakHouse.sol#249)
	External calls sending eth:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#238)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
	Event emitted after the call(s):
	- Deposit(msg.sender,_pid,amountToStake) (contracts/SteakHouse.sol#254)
	- FeeCollected(msg.sender,_pid,pendingWithdrawFee) (contracts/SteakHouse.sol#255)
Reentrancy in SteakHouse.emergencyWithdraw(uint256) (contracts/SteakHouse.sol#275-284):
	External calls:
	- pool.stakingToken.safeTransfer(address(msg.sender),userAmount) (contracts/SteakHouse.sol#282)
	Event emitted after the call(s):
	- EmergencyWithdraw(msg.sender,_pid,userAmount) (contracts/SteakHouse.sol#283)
Reentrancy in SteakHouse.withdraw(uint256,uint256) (contracts/SteakHouse.sol#259-272):
	External calls:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#266)
		- returndata = address(token).functionCall(data,SafeERC20: low-level call failed) (contracts/ERC20/SafeERC20.sol#71)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#296)
		- steak.safeTransfer(_to,steakTokenBalance - pendingHarvestFee) (contracts/SteakHouse.sol#297)
		- steak.safeTransfer(feeReceiver,pendingHarvestFee) (contracts/SteakHouse.sol#300)
		- steak.safeTransfer(_to,_amount - pendingHarvestFee) (contracts/SteakHouse.sol#301)
	- pool.stakingToken.safeTransfer(address(msg.sender),_amount) (contracts/SteakHouse.sol#270)
	External calls sending eth:
	- user.remainingSteakTokenReward = safeRewardTransfer(msg.sender,pending) (contracts/SteakHouse.sol#266)
		- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
	Event emitted after the call(s):
	- Withdraw(msg.sender,_pid,_amount) (contracts/SteakHouse.sol#271)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3

SteakHouse.collect(uint256) (contracts/SteakHouse.sol#92-97) uses timestamp for comparisons
	Dangerous comparisons:
	- require(bool,string)(block.timestamp >= endTime + 604800,too early to collect) (contracts/SteakHouse.sol#93)
SteakHouse.add(uint16,IERC20,bool) (contracts/SteakHouse.sol#117-137) uses timestamp for comparisons
	Dangerous comparisons:
	- block.timestamp > startTime (contracts/SteakHouse.sol#125-126)
SteakHouse.getMultiplier(uint256,uint256) (contracts/SteakHouse.sol#169-182) uses timestamp for comparisons
	Dangerous comparisons:
	- _from > endTime || _to < startTime (contracts/SteakHouse.sol#175)
	- _to > endTime (contracts/SteakHouse.sol#178)
SteakHouse.pendingSteak(uint256,address) (contracts/SteakHouse.sol#185-202) uses timestamp for comparisons
	Dangerous comparisons:
	- block.timestamp > pool.lastRewardTime && pool.stakingTokenTotalAmount != 0 (contracts/SteakHouse.sol#194)
SteakHouse.massUpdatePools() (contracts/SteakHouse.sol#205-210) uses timestamp for comparisons
	Dangerous comparisons:
	- pid < length (contracts/SteakHouse.sol#207)
SteakHouse.updatePool(uint256) (contracts/SteakHouse.sol#213-228) uses timestamp for comparisons
	Dangerous comparisons:
	- block.timestamp <= pool.lastRewardTime (contracts/SteakHouse.sol#215)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#block-timestamp

Address.isContract(address) (contracts/utils/Address.sol#26-35) uses assembly
	- INLINE ASM (contracts/utils/Address.sol#33)
Address._verifyCallResult(bool,bytes,string) (contracts/utils/Address.sol#171-188) uses assembly
	- INLINE ASM (contracts/utils/Address.sol#180-183)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage

Address.functionCall(address,bytes) (contracts/utils/Address.sol#79-81) is never used and should be removed
Address.functionCallWithValue(address,bytes,uint256) (contracts/utils/Address.sol#104-106) is never used and should be removed
Address.functionDelegateCall(address,bytes) (contracts/utils/Address.sol#153-155) is never used and should be removed
Address.functionDelegateCall(address,bytes,string) (contracts/utils/Address.sol#163-169) is never used and should be removed
Address.functionStaticCall(address,bytes) (contracts/utils/Address.sol#129-131) is never used and should be removed
Address.functionStaticCall(address,bytes,string) (contracts/utils/Address.sol#139-145) is never used and should be removed
Address.sendValue(address,uint256) (contracts/utils/Address.sol#53-59) is never used and should be removed
Context._msgData() (contracts/utils/Context.sol#20-23) is never used and should be removed
SafeERC20.safeApprove(IERC20,address,uint256) (contracts/ERC20/SafeERC20.sol#35-44) is never used and should be removed
SafeERC20.safeDecreaseAllowance(IERC20,address,uint256) (contracts/ERC20/SafeERC20.sol#51-58) is never used and should be removed
SafeERC20.safeIncreaseAllowance(IERC20,address,uint256) (contracts/ERC20/SafeERC20.sol#46-49) is never used and should be removed
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#dead-code

SteakHouse.feeReceiver (contracts/SteakHouse.sol#55) is set pre-construction with a non-constant function or state variable:
	- owner()
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#function-initializing-state

Pragma version^0.8.0 (contracts/ERC20/IERC20.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
Pragma version^0.8.0 (contracts/ERC20/SafeERC20.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
Pragma version^0.8.0 (contracts/SteakHouse.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
Pragma version^0.8.0 (contracts/utils/Address.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
Pragma version^0.8.0 (contracts/utils/Context.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
Pragma version^0.8.0 (contracts/utils/Ownable.sol#3) necessitates a version too recent to be trusted. Consider deploying with 0.6.12/0.7.6
solc-0.8.0 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity

Low level call in Address.sendValue(address,uint256) (contracts/utils/Address.sol#53-59):
	- (success) = recipient.call{value: amount}() (contracts/utils/Address.sol#57)
Low level call in Address.functionCallWithValue(address,bytes,uint256,string) (contracts/utils/Address.sol#114-121):
	- (success,returndata) = target.call{value: value}(data) (contracts/utils/Address.sol#119)
Low level call in Address.functionStaticCall(address,bytes,string) (contracts/utils/Address.sol#139-145):
	- (success,returndata) = target.staticcall(data) (contracts/utils/Address.sol#143)
Low level call in Address.functionDelegateCall(address,bytes,string) (contracts/utils/Address.sol#163-169):
	- (success,returndata) = target.delegatecall(data) (contracts/utils/Address.sol#167)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls

Parameter SteakHouse.collect(uint256)._amount (contracts/SteakHouse.sol#92) is not in mixedCase
Parameter SteakHouse.setSteakPerSecond(uint256,bool)._steakPerSecond (contracts/SteakHouse.sol#102) is not in mixedCase
Parameter SteakHouse.setSteakPerSecond(uint256,bool)._withUpdate (contracts/SteakHouse.sol#102) is not in mixedCase
Parameter SteakHouse.add(uint16,IERC20,bool)._allocPoint (contracts/SteakHouse.sol#118) is not in mixedCase
Parameter SteakHouse.add(uint16,IERC20,bool)._stakingToken (contracts/SteakHouse.sol#119) is not in mixedCase
Parameter SteakHouse.add(uint16,IERC20,bool)._withUpdate (contracts/SteakHouse.sol#120) is not in mixedCase
Parameter SteakHouse.set(uint256,uint16,bool)._pid (contracts/SteakHouse.sol#142) is not in mixedCase
Parameter SteakHouse.set(uint256,uint16,bool)._allocPoint (contracts/SteakHouse.sol#143) is not in mixedCase
Parameter SteakHouse.set(uint256,uint16,bool)._withUpdate (contracts/SteakHouse.sol#144) is not in mixedCase
Parameter SteakHouse.setWithdrawFee(uint256)._withdrawFee (contracts/SteakHouse.sol#154) is not in mixedCase
Parameter SteakHouse.setHarvestFee(uint256)._harvestFee (contracts/SteakHouse.sol#159) is not in mixedCase
Parameter SteakHouse.setFeeReceiver(address)._feeReceiver (contracts/SteakHouse.sol#164) is not in mixedCase
Parameter SteakHouse.getMultiplier(uint256,uint256)._from (contracts/SteakHouse.sol#169) is not in mixedCase
Parameter SteakHouse.getMultiplier(uint256,uint256)._to (contracts/SteakHouse.sol#169) is not in mixedCase
Parameter SteakHouse.pendingSteak(uint256,address)._pid (contracts/SteakHouse.sol#185) is not in mixedCase
Parameter SteakHouse.pendingSteak(uint256,address)._user (contracts/SteakHouse.sol#185) is not in mixedCase
Parameter SteakHouse.updatePool(uint256)._pid (contracts/SteakHouse.sol#213) is not in mixedCase
Parameter SteakHouse.deposit(uint256,uint256)._pid (contracts/SteakHouse.sol#231) is not in mixedCase
Parameter SteakHouse.deposit(uint256,uint256)._amount (contracts/SteakHouse.sol#231) is not in mixedCase
Parameter SteakHouse.withdraw(uint256,uint256)._pid (contracts/SteakHouse.sol#259) is not in mixedCase
Parameter SteakHouse.withdraw(uint256,uint256)._amount (contracts/SteakHouse.sol#259) is not in mixedCase
Parameter SteakHouse.emergencyWithdraw(uint256)._pid (contracts/SteakHouse.sol#275) is not in mixedCase
Parameter SteakHouse.safeRewardTransfer(address,uint256)._to (contracts/SteakHouse.sol#288) is not in mixedCase
Parameter SteakHouse.safeRewardTransfer(address,uint256)._amount (contracts/SteakHouse.sol#288) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions

Redundant expression "this (contracts/utils/Context.sol#21)" inContext (contracts/utils/Context.sol#15-25)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#redundant-statements

SteakHouse.setHarvestFee(uint256) (contracts/SteakHouse.sol#159-162) uses literals with too many digits:
	- require(bool)(_harvestFee <= 1000000) (contracts/SteakHouse.sol#160)
SteakHouse.deposit(uint256,uint256) (contracts/SteakHouse.sol#231-256) uses literals with too many digits:
	- pendingWithdrawFee = _amount * withdrawFee / 1000000 (contracts/SteakHouse.sol#242)
SteakHouse.safeRewardTransfer(address,uint256) (contracts/SteakHouse.sol#288-303) uses literals with too many digits:
	- pendingHarvestFee = _amount * harvestFee / 1000000 (contracts/SteakHouse.sol#290)
SteakHouse.safeRewardTransfer(address,uint256) (contracts/SteakHouse.sol#288-303) uses literals with too many digits:
	- pendingHarvestFee = steakTokenBalance * harvestFee / 1000000 (contracts/SteakHouse.sol#295)
SteakHouse.slitherConstructorVariables() (contracts/SteakHouse.sol#17-304) uses literals with too many digits:
	- harvestFee = 200000 (contracts/SteakHouse.sol#53)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#too-many-digits

deposit(uint256,uint256) should be declared external:
	- SteakHouse.deposit(uint256,uint256) (contracts/SteakHouse.sol#231-256)
withdraw(uint256,uint256) should be declared external:
	- SteakHouse.withdraw(uint256,uint256) (contracts/SteakHouse.sol#259-272)
emergencyWithdraw(uint256) should be declared external:
	- SteakHouse.emergencyWithdraw(uint256) (contracts/SteakHouse.sol#275-284)
renounceOwnership() should be declared external:
	- Ownable.renounceOwnership() (contracts/utils/Ownable.sol#55-58)
transferOwnership(address) should be declared external:
	- Ownable.transferOwnership(address) (contracts/utils/Ownable.sol#64-68)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#public-function-that-could-be-declared-external
contracts/SteakHouse.sol analyzed (6 contracts with 75 detectors), 81 result(s) found
```