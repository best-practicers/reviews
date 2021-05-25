# Ownership
## Created by: [shortdoom](https://github.com/shortdoom)

## Summary
* EthBlock.art uses implementation of openzeppelin Ownable access control for management of contract.
* From a user (both Creative Coder & Creator) perspective BFactory is an entity which proxy user call to minting functions. There is no way to call non-factory contracts directly, those are guarded by Ownable access control upon first initialization.
* Contract owner is responsible for setting pricing strategy and has the ability to change it.
* There are three additional access control modifiers defined inside of the BFactory contract. Those modifiers control management of Style (Creative Coder) and Art (Creator).
* Overall, the contract owner has too much unlocked power over the contract, and can render the whole contract not usable.
* Risks:
    * Pricing is dependant on parameters set by owner, can be changed at any time
    * URI can be changed at any time by owner
    * Contract owner has access to user variables

## Recommendations
* Writing tests, checking for changes of ownership after each action performed by Creative Coder or Creator which changes state of variables.
* Introducing lock feature for all variables which are not supposed to be changed (URI).
* Test ERC721 Interface with EthBlock.art contracts. transfer/transferFrom.
* Use OpenZeppelin Access Control Roles to manage roles more efficiently and transparently.
* Define `onlyOwner` (Contract owner) as separate from `owner` of Style or an Art. 

## Example Test Structure

```javascript
describe("EthBlock.art", async () => {
  });

  it("Mint styles", async function () {
    // Everyone can mint
    // Create Style1 supply for user1
    // Create Style2 supply for user2
    // List styles, delist styles, change styles
    // Call Getters
  });

  it("Mint Art with styles", async function() {
    // Check flags (isListed?)
    // Check access to styles of owners and non owners
    // Call Getters (from owner and non owner)
  });

  it("Transfer Art to _ser2, check ownership", async function() {
    // Check if ownership is transferred to
    // Check if new user can call owner functions
    // Check if old user cannot call owner functions
    // Check access to balances
  });
 
  it("Contract owner wrecks havoc", async function() {
    // Contract owner changes anything he can change after initialization (shouldn't!)
    // Contract owner tries to change variables assigned to users (shouldn't!)
  });
 
});
```

### BlockStyle and ERC721Style are relevant for Creative Coders

BlockStyle - created by Creative Coders and used in the creation of BlockArts

* onlyOwner - `setBase` and `setCanvas`, initial parameters for managing ERC721 part of app.

* Requires ownership to set parameters of Style for given Id.
        User needs to be an owner of a style to set `setCanvas`, `setToken`,
        `setStyleSupplyCap`, `setStyleFeeMul`, `setStyleFeemin`

*ERC721Style - Minting of an style by owner (Creative Coder)*

* Only owner (of Style) can mint
        
* Only owner (of Style) can `setCanvasURI`, `canvasURI` (This fails!)

* Setters & Getters are public

### BlockArt and ERC721Ref are relevant for Creators

BArt - minted by creators using a block number and BlockStyles.

* BArt is fully controlled by contract owner
* onlyOwner can `setContractURI`, `setTokenURI`, `burnToken`

*ERC721Ref - Minting of an NFT-piece using for Creator from blockNumber + Styles (from Creative Coder)*

* onlyOwner can mint new NFT-piece with owned Style
* onlyOwner can `setContractURI`

### BFactory - interface for minting of Styles and Art for all external users. Main contract for blockart.

* Everyone can mintArt for a fee using selected styleId
* Everyone can mintStyle for a fee setting `canvasURI`
* Getters are public

*Introduces three access control modifiers*
            
* onlyStyleListed - can `canMintWithStyle`
* onlyStyleOwner - can `collectStyleFees`
* onlyArtOwner - can `burnArt`, `remint`
        
**onlyOwner**

* collectCoins - transfer treasury to owner
* collectBalance - transfer contract balance to owner
* Manages pricing (Internal Constants Management)
