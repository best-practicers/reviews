# Natspec
## Created by: Jolene Dunne

## Summary
* According to Natspec/Ethereum best practices, everything that is in the ABI should be covered by Natspec. I've therefore focused this review on items that appear in the ABI only.
* In general, there are very few Natspec comments and they are limited to only a couple of files. This project would be well served by taking the time to add more detailed annotations to all public interfaces.
* I have reviewed the abi.json and provided line numbers as well as one of three comments for the public events/functions
	* There is no Natspec comment
	* There exists a Natspec comment but it is sparse, usually 1-2 tags
	* The Natspec comment contains a reference to another more well-defined comment
* My recommendation is that lines with comment 1 or 2 above should be remediated, while 3 is optional
* Note that the below list is not exhaustive - the ABI was significant in size and most contracts were not documented. It would probably be easier from a remediation perspective to attempt to annotate the project as a whole rather than using the ABI as a reference as I tried to do.


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

### `contracts/`

#### `access/`

###### `Ownable.sol`
* L55 - event OwnershipTransferred does not have an associated NatSpec comment
* L90 - Comment exists on function renounceOwnership, but could make better use of tags
* L99 - Comment exists on function transferOwnership, but could make better use of tags

###### `OwnableUpgradeable.sol`
* L58 - event OwnershipTransferred does not have an associated NatSpec comment
* L98 - Comment exists on function renounceOwnership, but could make better use of tags
* L107 - Comment exists on function transferOwnership, but could make better use of tags

#### `exchanges/`

##### `ETHmxMinter/`

###### `ETHmxMinter.sol`
* L149 - function addLp does not have an associated NatSpec comment
* L155 - function mint does not have an associated NatSpec comment
* L251 - function pause does not have an associated NatSpec comment
* L255 - function recoverERC20 does not have an associated NatSpec comment
* L336 - function unpause does not have an associated NatSpec comment
* L342 - function ethmx does not have an associated NatSpec comment
* L346 - function ethmxMintParams does not have an associated NatSpec comment
* L357 - function ethmxFromEth does not have an associated NatSpec comment
* L389 - function ethmxFromEthtx does not have an associated NatSpec comment
* L399 - function ethtx does not have an associated NatSpec comment
* L403 - function ethtxMintParams does not have an associated NatSpec comment
* L413 - function ethtxAMM does not have an associated NatSpec comment
* L417 - function ethtxFromEth does not have an associated NatSpec comment
* L493 - function inGenesis does not have an associated NatSpec comment
* L507 - function liquidityPoolsAt does not have an associated NatSpec comment
* L517 - function lpRecipient does not have an associated NatSpec comment
* L521 - function lpShare does not have an associated NatSpec comment

##### `ETHtxAMM/`

###### `ETHtxAMM.sol`
* L211 - function pause does not have an associated NatSpec comment
* L258 - function unpause does not have an associated NatSpec comment
* L308 - function ethtx does not have an associated NatSpec comment

#### `libraries/`

###### `EnumerableMap.sol`

#### `oracles/`

###### `GasPrice.sol`

#### `rewards/`

###### `RewardsPool.sol`
* L125 - function pause does not have an associated NatSpec comment
* L161 - function unpause does not have an associated NatSpec comment

###### `LPRewardsAuto.sol`
* L323 - function pause does not have an associated NatSpec comment
* L368 - function unpause does not have an associated NatSpec comment

##### `ETHmxRewards/`

###### `ETHmxRewards.sol`
* L130 - function ethmx does not have an associated NatSpec comment
* L311 - function pause does not have an associated NatSpec comment
* L410 - function unpause does not have an associated NatSpec comment

##### `ETHmxRewardsManager/`

##### `LPRewards/`

###### `LPRewards.sol`
* L405 - function pause does not have an associated NatSpec comment
* L588 - function unpause does not have an associated NatSpec comment

##### `RewardsManager/`

##### `ETHtxRewardsManager/`

###### `ETHtxRewardsManager.sol`
* L164 - function ethtx does not have an associated NatSpec comment
* L168 - function ethtxAMM does not have an associated NatSpec comment

##### `mooniswap/`

#### `tokens/`

##### `ERC20/`

###### `ERC20.sol`
* L82 - Comment exists on function name, but could make better use of tags
* L90 - Comment exists on function symbol, but could make better use of tags
* L107 - Comment exists on function decimals, but could make better use of tags
* L114 - function totalSupply contains a reference to IERC20 - could use `@inheritdoc`
* L121 - function balanceOf contains a reference to IERC20 - could use `@inheritdoc`
* L139 - Comment exists on function transfer, but could make better use of tags
* L152 - function allowance contains a reference to IERC20 - could use `@inheritdoc`
* L169 - function approve contains a reference to IERC20 - could use `@inheritdoc`
* L192 - function transferFrom contains a reference to IERC20 - could use `@inheritdoc`
* L221 - Comment exists on function increaseAllowance, but could make better use of tags
* L248 - Comment exists on function decreaseAllowance, but could make better use of tags

###### `ERC20Upgradeable.sol`
* L94 - Comment exists on function name, but could make better use of tags
* L102 - Comment exists on function symbol, but could make better use of tags
* L119 - Comment exists on function decimals, but could make better use of tags
* L126 - function totalSupply contains a reference to IERC20 - could use `@inheritdoc`
* L133 - function balanceOf contains a reference to IERC20 - could use `@inheritdoc`
* L151 - Comment exists on function transfer, but could make better use of tags
* L164 - function allowance contains a reference to IERC20 - could use `@inheritdoc`
* L181 - function approve contains a reference to IERC20 - could use `@inheritdoc`
* L204 - function transferFrom contains a reference to IERC20 - could use `@inheritdoc`
* L233 - Comment exists on function increaseAllowance, but could make better use of tags
* L260 - Comment exists on function decreaseAllowance, but could make better use of tags

##### `ERC20TxFee/`

##### `ETHmx/`

###### `ETHmx.sol`
* L67 - function burn does not have an associated NatSpec comment
* L71 - function mintTo does not have an associated NatSpec comment
* L81 - function pause does not have an associated NatSpec comment
* L85 - function recoverERC20 does not have an associated NatSpec comment
* L94 - function setMinter does not have an associated NatSpec comment
* L99 - function unpause does not have an associated NatSpec comment
* L105 - function minter does not have an associated NatSpec comment
* L109 - function name does not have an associated NatSpec comment
* L113 - function symbol could use `@inheritdoc`

##### `ETHtx/`

###### `ETHtx.sol`
* L82 - function burn does not have an associated NatSpec comment
* L92 - function mint does not have an associated NatSpec comment
* L102 - function pause does not have an associated NatSpec comment
* L106 - function recoverERC20 does not have an associated NatSpec comment
* L121 - function setMinter does not have an associated NatSpec comment
* L126 - function unpause does not have an associated NatSpec comment
* L132 - function minter does not have an associated NatSpec comment
* L136 - function name does not have an associated NatSpec comment
* L140 - function symbol could use `@inheritdoc`





...
