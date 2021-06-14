# OpenZeppelin
## Created by: [Roberto Cantu](https://github.com/RCantu92)

## Summary
* TLDR of the findings

## File Review

### `contracts/AXBridge.sol`

Contract *AXBridge* on L11:
* Correctly inherits the *Ownable* contract on L11.
* Correctly adds *onlyOwner* modifier on L12.

### `contracts/BatchSwap.sol`

Contract *BatchSwap* on L63:
* Correctly inherits the *Ownable*, *Pausable*, *IERC721Receiver*, *IERC1155Receiver* modifier from their respective solidity files.

* Correctly implements *Counters* on L79.

* Correctly implements *SafeMath* on L80.

Function *createSwapIntent()* L141:
* Correctly adds *whenNotPaused* modifier on L141.
* Correctly implement *add()* from *SafeMath* on L144.

Function *closeSwapIntent()* L197:
* Correctly adds *whenNotPaused* modifier on L197.
* Correctly implement *add()* from *SafeMath* on L202.
* Correctly implement *add()* from *SafeMath* on L204.
* Correctly implement *add()* from *SafeMath* on L205.

Function *setCryptoPunkAddress()* L309:
* Correctly adds *onlyOwner* modifier on L309.

Function *setTradeSquadAddress()* L326:
* Correctly adds *onlyOwner* modifier on L326.

Function *setVaultAddress()* L331:
* Correctly adds *onlyOwner* modifier on L331.

Function *setDappRelation()* L336:
* Correctly adds *onlyOwner* modifier on L336.

Function *setWhitelist()* L341:
* Correctly adds *onlyOwner* modifier on L341.

Function *setPayment()* L352:
* Correctly adds *onlyOwner* modifier on L352.
* Correctly adds *whenNotPaused* modifier on L352.
* Could add *mul()* from *SafeMath* on L354 (?)

Function *onERC721Received()* L394:
* Correctly creates function based on *onERC721Received()* from *IERC721.sol* on L394.

Function *onERC1155Received()* L397:
* Correctly creates function based on *onERC1155Received()* from *IERC1155.sol* on L397.

Function *onERC1155BatchReceived* L400:
* Correctly creates function based on *onERC1155BatchReceived()* from *IERC1155.sol* on L400.

### `contracts/Pausable.sol`

Contract *BatchSwap* on L6:
* Correctly inherits the *Ownable* contract on L6.

function *setPauseStatus()* on L13:
* Correctly adds *onlyOwner* modifier on L13.