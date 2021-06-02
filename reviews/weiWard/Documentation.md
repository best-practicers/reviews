# Documentation

## Created by:

## Summary

- Address the issues provided in the file review section
- [natspec](https://docs.soliditylang.org/en/v0.7.5/natspec-format.html) tags are inconsistent, when comparing OpenZeppelin based contracts to 2021 weiWard LLC contracts
- Many contracts are missing full natspec coverage.

## Recommendations

- Apply changes found below.
- Add flow charts of how contracts interact with one another. Solidity Visual Developer and Surya are two popular Consensys Diligence-powered tools which provide visual analysis of smart contracts.

### `README.md`

- Recommend including high level explanation of platform and overview of smart contract structure; at minimum include brief outline of the smart contract interface (for swapping/staking)
- If there is an API to interact with the exchange functionality then it should be added, otherwise it may be useful to provide instructions on how to interface with the smart contracts directly
- Instructions for installing npm is unnecessary and should just be listed as a dev requirement
- Recommend adding links to platform, whitepaper, and deployed contracts on mainnet for convenience of devs and users who want more info
- Current test suit does not pass all tests

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

### `access/`

#### `Ownable.sol`

- Contract declaration - no @title, @author or @notice provided
- Recommend to use @notice tags instead of @dev tags for describing what a function does. @dev is reserved for extra details.
  - @dev would be ideal to replace the "NOTE:" comments that are present.
- @param missing for transferOwnership()
- @return missing for owner();
- Code ordering
  - Place onlyOwner modifier before constructor
  - Place view function(s) (owner()) last

#### `OwnableUpgradeable.sol`

- OpenZepplen \_\_gap variable declaration at bottom of contract should be ideally added to the top of contract
- Recommend to use @notice tags instead of @dev tags for describing what a function does. @dev is reserved for extra details.
  - @dev would be ideal to replace the "NOTE:" comments that are present in most contracts.
- Contract declaration - no @title, @author or @notice provided
- @param missing for:
  - \_\_Ownable_init();
  - \_\_Ownable_init_unchained()
  - transferOwnership()
- Place onlyOwner modifier before constructor

### `exchanges/`

### `ETHmxMinter/`

#### `ETHmxMinter.sol`

- no NatSpec tags present

#### `ETHmxMinterData.sol`

- N/A

#### `/ETHtxAMM`

#### `/ETHtxAMM.sol`

- no NatSpec tags present

#### `/ETHtxAMM.sol`

- N/A

#### `/Libraries`

#### `EnumerableMap.sol`

- Code ordering
  - Group AddressToUintMap struct declaration at top with other structs
- Recommend to use @notice tags instead of @dev tags for describing what a function does. @dev is reserved for extra details.
  - "Requirement: " tag for the following functions can be replaced with @param
    - \_at()
    - \_get()
    - at()
    - get()
  - "NOTE:" comments can be replaced with @dev

#### `Sqrt.sol`

- Missing NatSpec tags

#### `UintLog.sol`

- Missing NatSpec tags

#### `/Oracles`

#### `GasPrice.sol`

- Missing NatSpec tags

#### `/Rewards`

#### `/ETHmxRewards`

#### `EthmxRewards.sol`

- Missing NatSpec tags

#### `EthmxRewardsData.sol`

- N/A

#### `/ETHtxRewardsManager`

- N/A

#### `/LPRewards`

#### `LPRewards.sol`

- Rewriting requires, should create a modifier
  - require on line 370 and 387 are the same
  - require on line 488 and 538 are the same
- Missing NatSpec tags

#### `LPRewardsData.sol`

- N/A

#### `/mooniswap`

#### `MooniFactory.sol`

- Missing NatSpec tags

#### `Mooniswap.sol`

- Missing NatSpec tags
- Can move VirtualBalance library into its own file

#### `UniERC20.sol`

- Missing NatSpec tags

#### `/RewardsManager`

#### `RewardsManager.sol`

- Missing NatSpec tags

#### `RewardsManagerAuto.sol`

- Missing NatSpec tags

#### `RewardsManagerData.sol`

- N/A

#### `FeeLogic.sol`

- Missing NatSpec tags

#### `LPRewardsAuto.sol`

- Rewriting requires, should create a modifier
  - require on line 156,181,191,760 are the same
  - require on line 488 and 538 are the same
  - require on line 564 and 584 are the same
  - require on line 578 and 746 are the same
  - require on line 640 and 651 are the same
- 'WARNING: ' comments before functions can be made @dev comments
- Comment on line 522, 893 can be made a @dev tag
- Comment on line 928 is an extremely long one liner, needs to be split
- Missing NatSpec tags

#### `ManagedRewardsPoolInstant.sol`

- Missing NatSpec tags

#### `RewardsPool.sol`

- Can turn comments before the following functions into @dev
  - recoverUnstakedTokens
  - recoverUnsupportedERC20
- Missing NatSpec tags

#### `RewardsPoolInstant.sol`

- Can turn comments before the following functions into @dev
  - accruedRewardsPerToken
  - recoverUnredeemableRewards
- Missing NatSpec tags

#### `ValuePerMoonV1.sol`

- Missing NatSpec tags

#### `ValuePerMoonV2.sol`

- Missing NatSpec tags

#### `/tokens`

#### `/ERC20`

#### `ERC20.sol`

- Recommend to use @notice tags instead of @dev tags for describing what a function does. @dev is reserved for extra details.
  - @dev would be ideal to replace the "NOTE:" comments that are present.
  - "Requirement: " tags can be replaced with @params
- Missing most NatSpec tags

#### `ERC20Upgradable.sol`

- Recommend to use @notice tags instead of @dev tags for describing what a function does. @dev is reserved for extra details.
  - @dev would be ideal to replace the "NOTE:" comments that are present.
  - "Requirement: " tags can be replaced with @params
- OpenZepplen \_\_gap variable declaration at bottom of contract should be ideally added to the top of contract
- Missing most NatSpec tags

#### `/ERC20TxFee`

#### `ERC20TxFee.sol`

- @dev tags can be changed to @notice
- "Requirement: " tags can be replaced with @params
- Comment on line 56 can be made into a @dev
- Missing most NatSpec tags

#### `ERC20TxFeeUpgradeable.sol`

- @dev stagss can be changed to @notice
- "Requirement: " tags can be replaced with @params
- Comment on line 70 can be made into a @dev
- OpenZepplen \_\_gap variable declaration at bottom of contract should be ideally added to the top of contract
- Missing most NatSpec tags

#### `/ETHmx`

#### `/ETHmx.sol`

- Missing NatSpec tags

#### `/ETHmxData.sol`

- N/A

#### `/ETHtx`

#### `/ETHtx.sol`

- Place onlyMinter() modifier before constructor
- Missing NatSpec tags

#### `/ETHtxData.sol`

- N/A
