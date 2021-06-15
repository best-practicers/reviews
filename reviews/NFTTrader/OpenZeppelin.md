# OpenZeppelin
## Created by: [Roberto Cantu](https://github.com/RCantu92)

## Summary
* TLDR of the findings

## File Review

### `contracts/AXBridge.sol`

Contract `AXBridge` on L11:
* Correctly inherits the `Ownable` contract on L11.
* Correctly adds `onlyOwner` modifier on L12.

### `contracts/BatchSwap.sol`

### Note:

L13-L30: Created own version of ERC20, ERC721, and ERC1155 interfaces rather than using OpenZeppelin's interfaces for the same ERC standards. Does not have full functionality of the OpenZeppelin interfaces, so perhaps that is why they did not utilize them, but they could have.

Contract `BatchSwap` on L63:
* Correctly inherits the `Ownable`, `Pausable`, `IERC721Receiver`, `IERC1155Receiver` modifier from their respective solidity files.

* Correctly implements `Counters` on L79.

* Correctly implements `SafeMath` on L80.

Function `createSwapIntent()` L141:
* Correctly adds `whenNotPaused` modifier on L141.
* Correctly implement `add()` from *SafeMath* on L144.

Function `closeSwapIntent()` L197:
* Correctly adds `whenNotPaused` modifier on L197.
* Correctly implement `add()` from *SafeMath* on L202.
* Correctly implement `add()` from *SafeMath* on L204.
* Correctly implement `add()` from *SafeMath* on L205.

Function `setCryptoPunkAddress()` L309:
* Correctly adds `onlyOwner` modifier on L309.

Function `setTradeSquadAddress()` L326:
* Correctly adds `onlyOwner` modifier on L326.

Function `setVaultAddress()` L331:
* Correctly adds `onlyOwner` modifier on L331.

Function `setDappRelation()` L336:
* Correctly adds `onlyOwner` modifier on L336.

Function `setWhitelist()` L341:
* Correctly adds `onlyOwner` modifier on L341.

Function `setPayment()` L352:
* Correctly adds `onlyOwner` modifier on L352.
* Correctly adds `whenNotPaused` modifier on L352.
* Could add `mul()` from `SafeMath` on L354 (?)

Function `onERC721Received()` L394:
* Correctly creates function based on `onERC721Received()` from `IERC721.sol` on L394.

Function `onERC1155Received()` L397:
* Correctly creates function based on `onERC1155Received()` from `IERC1155.sol` on L397.

Function `onERC1155BatchReceived` L400:
* Correctly creates function based on `onERC1155BatchReceived()` from `IERC1155.sol` on L400.

### `contracts/BatchVault.sol`

Contract `BatchVault` on L7:
* Correctly inherits the `Ownable`, `Pausable` from their respective solidity files.

Function `getVaultBalance()` L17:
* Correctly adds `onlyOwner` modifier on L17.
* Correctly adds `whenNotPaused` modifier on L17.

Function `sendVaultBalance()` L22:
* Correctly adds `onlyOwner` modifier on L22.
* Correctly adds `whenNotPaused` modifier on L22.

### `contracts/CKBridge.sol`

### `contracts/ERC1155Five.sol`

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Five` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Four.sol`

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Four` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155One.sol`

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155One` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Six.sol`

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Six` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Three.sol`

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Three` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Two.sol`

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Two` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/Pausable.sol`

Contract `BatchSwap` on L6:
* Correctly inherits the `Ownable` contract on L6.

function `setPauseStatus()` on L13:
* Correctly adds `onlyOwner` modifier on L13.