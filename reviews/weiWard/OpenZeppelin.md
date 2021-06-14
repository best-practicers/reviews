# OpenZeppelin
## Created by:

## Summary
* TLDR of the findings
* 

## Scope
```
├── README.md
└── contracts
    ├── access
        ├── Ownable.sol
        └── OwnableUpgradeable.sol
    ├── exchanges
        ├── ETHmxMinter
            ├── ETHMxMinter.sol
            └── ETHmxMinterData.sol
        ├── ETHtxAMM
            ├── ETHtxAMM.sol
            └── ETHtxAMMData.sol
    ├── libraries
            ├── EnumerableMap.sol
            ├── Sqrt.sol
            └── UintLog.sol
    ├── oracles
            └── GasPrice.sol
    ├── rewards
        ├── EthmxRewards
            ├── ETHmxRewards.sol
            └── ETHmxRewardsData.sol
        ├── ETHtxRewardsManager
            ├── ETHtxRewardsManager.sol
            └── ETHtxRewardsManagerData.sol  
        ├── LPRewards
            ├── LPRewards.sol
            └── LPRewardsData.sol    
        ├── RewardsManager
            ├── RewardsManager.sol
            ├── RewardsManagerAuto.sol
            └── RewardsManagerData.sol
        ├── mooniswap
            ├── MooniFactory.sol
            ├── Mooniswap.sol
            └── UniERC20.sol
        ├── FeeLogic.sol  
        ├── LPRewardsAuto.sol
        ├── ManagedRewardsPoolInstant.sol
        ├── RewardsPool.sol
        ├── RewardsPoolInstant.sol
        ├── ValuePerMoonV1.sol
        └── ValuePerUNIV2.sol   
    ├── tokens
        ├── ERC20
            ├── ERC20.sol
            └── ERC20Upgradeable.sol
        ├── ERC20TxFee
            ├── ERC20TxFee.sol
            └── ERC20TxFeeUpgradeable.sol     
        ├── ETHmx
            ├── ETHmx.sol
            └── ETHmxData.sol    
        └── ETHtx
            ├── ETHtx.sol
            └── ETHtxData.sol  
    └── Imports.sol
```

## File Review
### `README.md`

### `contracts/`

#### Recommendation to not have to copy & modify the `Ownable` and `OwnableUpgradeable` from OZ

The projects has been copying and modifying a lot OpenZeppelin's contracts. This is something that needs to be done very carefully and they did well document the modifications.

However, for the contracts `Ownable` and `OwnableUpgradeable`, there is a way to achieve what they want without having to copy nor modify the OZ contracts. Even though this has a higher cost in gas, it is almost negligible compared to the need to maintain a copy of a modified contract. It would also add some security, because the current modifications didn't take this into account:

I would recommend to not make copies of both Ownable contracts
And to replace what we have here (and on some other places):

https://github.com/weiWard/weiward-contracts/blob/main/contracts/exchanges/ETHtxAMM/ETHtxAMM.sol#L70

```
__Ownable_init_unchained(owner_);
```

By

```
__Ownable_init_unchained();
transferOwnership(owner_);
```

And that in all contracts that are trying to initialize with an owner different passed as parameter

This would work the same way for just a little more gas, but prevent to have modify OZ contracts.
this also add the check if  `owner_` is different of `address(0)`

#### Recommendation: No need for so many extends

In several contracts, we can see the contracts extending:

```
	Initializable,
	ContextUpgradeable,
	OwnableUpgradeable,
    PausableUpgradeable
```

and then in the initializer function:

```
function init(address owner_) public virtual initializer {
		__Context_init_unchained();
		__Ownable_init_unchained(owner_);
```

There shouldn't be a need to extend `Initializable` since `ContextUpgradeable`, `OwnableUpgradeable` and `PausableUpgradeable` already do it.

Also, if the previous recommendation to not modify `Ownable` is followed, there shouldn't be a need to extend `ContextUpgradeable`. Extending `OwnableUpgradeable` should be enough, with the use of `__Ownable_init()` in the constructor. This would would launch the chain that does the Context initialization.

And in the case `Ownable`is still modified, a lot of those contracts also extend `PausableUpgradeable` which could be used to init the context with a call to `__Pausable_init();`, before initializing `Ownable` with a call to `Unchained`, 

This allows for less extends in the contracts and cleaner code. 
I suppose this is all done to save the few ~200 gas this way of doing allows, but this seems again a lot of code & maintaining for so few gas saving


#### `/access/`


#### `<contract>.sol`

#### `<contract>.sol`

#### `<contract>.sol`

#### `<contract>.sol`

...
