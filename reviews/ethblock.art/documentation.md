# Documentation
## Created by: [kjr217](https://github.com/kjr217)

## Summary
* Address the issues provided in the file review section
* Lots of [natspec](https://docs.soliditylang.org/en/v0.7.5/natspec-format.html) missing and unorthodoxically used throughout.

## Scope
```
├── README.md
└── contracts
    ├── BArt.sol
    ├── BFactory.sol
    ├── BStyle.sol
    ├── ERC721Ref.sol
    ├── ERC721Style.sol
```

## File Review
### `README.md`
* Overall, readme is quite useful.
* In BArt section, supplyPerBlock and supplyPerStyle misspelling of `giver`, should be `given`?
* In BArt section, artToValue misspelling of `calculatin` should be `calculating`
* In BFactorysection , for the last 3 variable names in Store, make them consistent with the contract, i.e. in the contract they go by initials `scfb`, `psfb`, `asl`
* Flow charts
    * Helpful with outlining structure / functionality
    * Arrows in `Contracts` chart could be less hectic
    * `Contracts` chart missing functions
    * Flow charts would benefit from including the version so it is clear which model is current

---
### `contracts/`
#### `BArt.sol`
* Contract declaration - line 25 should include `@notice` tag.
* Contract declaration - No `@author` declared.
* `setContractURI()`, `setTokenURI()`, `burnToken()` - missing `@notice` and `@param` tags, for multiple parameters provide multiple param tags
* Should also provide the `@dev` tag describing the ownership of the function (onlyOwner) in `setContractURI()` and `burnToken()`

#### `BFactory.sol`
* Contract declaration - no `@title`, `@author` or `@notice` provided
* Struct variables in `Bp` should be defined.
* In all functions it is better to use `@notice` tags instead of `@dev` tags for describing what a function does, for most functions you have used `@dev` when you should have used @notice. `@dev` should be reserved for explaining extra details of a function.
* `@param` & `@notice` tags missing in several functions:
 - `burnArt()`, 
 - `remint()`, 
 - `canMintWithStyle()`, 
 - `collectStyleFees()`,
 - `collectCoins()`,
 - `collectBalance()`,
 - `transferTokensOwnership()`
* Missing `@return` tag in `calcArtPrice()` and `canMintWithStyle`
* Should provide an `@notice` to advice that `mintStyle()`, `burnArt()`, `remint()` and `mintArt()` is payable
* Floating `@notice` tags on line 250, line 278, line 340, notices should generally be attached to something, your use of it to define a few of the following functions will only apply the tag to the first function and not to the rest.
* All getters between line 280 to 302 are missing natspec tags, including `@return`, consider adding.
* All setters between line 304 to 366 should include `@notice` and `@param` natspec tags.

#### `BStyle.sol`
* Contract declaration - no `@title`, `@author` or `@notice` provided
* In all functions it is better to use `@notice` tags instead of `@dev` tags for describing what a function does, for most functions you have used `@dev` when you should have used @notice. `@dev` should be reserved for explaining extra details of a function.
* `@param` & `@notice` tags missing in several functions:
 - `setContractURI()`, 
 - `setBase()`, 
 - `setCanvas()`, 
 - `setToken()`,
 - `setStyleSupplyCap()`,
 - `setStyleFeeMul()`,
 - `setStyleFeeMin()`


#### `ERC721Ref.sol`
* Contract declaration - no `@title`, `@author` or `@notice` provided
* `@return` tag missing in `mint()`
* In all functions it is better to use `@notice` tags instead of `@dev` tags for describing what a function does, for most functions you have used `@dev` when you should have used @notice. `@dev` should be reserved for explaining extra details of a function.
* Floating `@notice` tags on line 65, line 94, notices should generally be attached to something, your use of it to define a few of the following functions will only apply the tag to the first function and not to the rest.
* All getters between line 67 to 92 are missing natspec tags, including `@return`, consider adding.
* No natspec tags provided for `contractURI()`

#### `ERC721Style.sol`
* Contract declaration - no `@title`, `@author` or `@notice` provided
* Floating `@notice` tags on line 59, line 80, line 107, line 119, notices should generally be attached to something, your use of it to define a few of the following functions will only apply the tag to the first function and not to the rest.
* In all functions it is better to use `@notice` tags instead of `@dev` tags for describing what a function does, for most functions you have used `@dev` when you should have used @notice. `@dev` should be reserved for explaining extra details of a function.
* All setters between line 60 to 78 should include `@notice` and `@param` natspec tags.
* All getters between line 82 to 105 are missing natspec tags, including `@return`, consider adding.
* `canvasURI` and `contractURI` missing `@return`, `@param` and `@notice` tags
