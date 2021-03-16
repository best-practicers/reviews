# Reentrancy

## By: [Kevin Keaveney](https://github.com/kkeaveney)

## Summary
*  The contracts use modifiers throughout to control access. The checks, effects, and interactions pattern
   has been applied when making external calls to untrusted contracts to prevent reentrancy attacks

### Recommendations
*  The Openzeppelin Reentrancy modifier can be applied when making external calls
*  BFactory.sol - state variables are updated after blockArt.mint, this doesn't relate to reentrancy that uses ether
   but the checks, effects and interactions pattern could be applied to maintain state.    


## Scope
```
└── contracts
    ├── BArt.sol
    ├── BFactory.sol
    ├── BStyle.sol
    ├── ERC721Ref.sol
    ├── ERC721Style.sol
           
```

## File Review
### `contracts/`
#### `BArt.sol`

* No external transfers from the contract. Any external functions can only be called by the owner


#### `BFactory..sol`

* The following functions update local state before an external transfer call, preventing possible reentrancy attacks
* collectStyleFees, the onlyStyleOwner modifier restricts access
* collectCoins & collectBalance(), called by the contract owner only



#### `BStyle..sol`

* No external transfers from the contract. External function visibility is restricted to the owner or an address that _isApprovedOrOwner


#### `ERC721Ref.sol`

* No external transfers from the contract, mint is an external function that can only be called by the owner, all function calls from mint are ERC721 compliant

#### `ERC721Style.sol`

* No external transfers from the contract, mint is an external function that can only be called by the owner, all function calls from mint are ERC721 compliant