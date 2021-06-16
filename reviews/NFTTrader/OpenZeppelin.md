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

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Four` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155One.sol`

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155One` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Six.sol`

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Six` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Three.sol`

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Three` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC1155Two.sol`

### Note:

L5: Imported `Counters.sol` from OpenZeppelin, but never implemented in the contract code.

Contract `ERC1155Two` on L7:
* Correctly inherits the `ERC1155` from its respective solidity file.

`constructor()` L14:
* Assuming provided JSON is acceptable URI, passes it correctly to `ERC1155` constructor on L14.

### `contracts/ERC20Four.sol`

Contract `ERC20Four` on L5:
* Correctly inherits the `ERC20` from its respective solidity file.

`constructor()` L6:
* Correctly passes strings to `ERC20` constructor on L6.

### `contracts/ERC20One.sol`

Contract `ERC20One` on L5:
* Correctly inherits the `ERC20` from its respective solidity file.

`constructor()` L6:
* Correctly passes strings to `ERC20` constructor on L6.

### `contracts/ERC20Three.sol`

Contract `ERC20Three` on L5:
* Correctly inherits the `ERC20` from its respective solidity file.

`constructor()` L6:
* Correctly passes strings to `ERC20` constructor on L6.

### `contracts/ERC20Two.sol`

Contract `ERC20Two` on L5:
* Correctly inherits the `ERC20` from its respective solidity file.

`constructor()` L6:
* Correctly passes strings to `ERC20` constructor on L6.

### `contracts/ERC721Four.sol`

Contract `ERC721Four` on L7:
* Correctly inherits the `ERC721` from its respective solidity file.
* Correctly implements `Counters` on L8.

`constructor()` L11:
* Correctly passes strings to `ERC721` constructor on L11.

### `contracts/ERC721One.sol`

Contract `ERC721One` on L7:
* Correctly inherits the `ERC721` from its respective solidity file.
* Correctly implements `Counters` on L8.

`constructor()` L11:
* Correctly passes strings to `ERC721` constructor on L11.

### `contracts/ERC721Three.sol`

Contract `ERC721Three` on L7:
* Correctly inherits the `ERC721` from its respective solidity file.
* Correctly implements `Counters` on L8.

`constructor()` L11:
* Correctly passes strings to `ERC721` constructor on L11.

### `contracts/ERC721Two.sol`

Contract `ERC721Two` on L7:
* Correctly inherits the `ERC721` from its respective solidity file.
* Correctly implements `Counters` on L8.

`constructor()` L11:
* Correctly passes first string, `"ERC721Two"` to `ERC721` constructor on L11.
* Second string, `"One"` might be supposed to be `"Two"` on L11.

### `contracts/Pausable.sol`

### Note:

OpenZeppelin has a [`Pausable` contract](https://docs.openzeppelin.com/contracts/2.x/api/lifecycle), so perhaps creating a new one is unnecessary?

Contract `BatchSwap` on L6:
* Correctly inherits the `Ownable` contract on L6.

function `setPauseStatus()` on L13:
* Correctly adds `onlyOwner` modifier on L13.

### `contracts/TradeSquads.sol`

### Note:

Can `increment()` be used instead of `++`?

Contract `TradeSquads` on L11:
* Correctly inherits the `ERC721`, `Ownable` from their respective solidity files on L11.
* Correctly implements `SafeMath` on L15.
* Correctly implements `Counters` on L16.
* Correctly implements `Strings` on L17.
* Cannot find documentation to prove `Counters` was used correctly on L32.
* Cannot find documentation to prove `Counters` was used correctly on L33.

Struct `Series` on L35:
* Cannot find documentation to prove `Counters` was used correctly on L36.

Mapping `hierarchyCounter` on L61:
* Correctly maps to `Counters.Counter` on L61.

`constructor()` L65:
* Correctly strings to `ERC721` constructor on L66-69.
* Cannot find documentation if usage of `Counters` as a type is correct on L74.
* Correctly calls function `increment()` from `Counters` on L75.
* Cannot find documentation if usage of `Counters` as a type is correct on L76.

Function `awardItem()` on L127:
* Correctly calls function `increment()` from `Counters` on L134.
* Correctly calls function `increment()` from `Counters` on L135.
* Correctly calls function `toString()` from `Strings` on L139.
* Correctly calls function `increment()` from `Counters` on L144.
* Correctly calls function `increment()` from `Counters` on L146.
* Correctly calls function `div()` from `SafeMath` on L148.
* Correctly calls function `mod()` from `SafeMath` on L156.
* Correctly calls function `add()` from `SafeMath` on L157.
* Correctly calls function `increment()` from `Counters` on L158.
* Correctly calls function `mod()` from `SafeMath` on L163.
* Correctly calls function `mod()` from `SafeMath` on L166.
* Correctly calls function `sub()` from `SafeMath` on L177.
* Correctly calls function `add()` from `SafeMath` on L185.
* Correctly calls function `increment()` from `Counters` on L186.
* Correctly calls function `toString()` from `Strings` on L192.

Function `setClaimVal()` on L196:
* Correctly adds `onlyOwner` modifier on L196.

Function `setClaimer()` on L200:
* Correctly adds `onlyOwner` modifier on L200.

Function `setDeltaHierarchy()` on L204:
* Correctly adds `onlyOwner` modifier on L204.

Function `setRangeNumber()` on L209:
* Correctly adds `onlyOwner` modifier on L209.

Function `setRange()` on L214:
* Correctly adds `onlyOwner` modifier on L214.

Function `setTraitNumber()` on L220:
* Correctly adds `onlyOwner` modifier on L220.

Function `setTrait()` on L225:
* Correctly adds `onlyOwner` modifier on L225.

Function `addSeries()` on L236:
* Correctly adds `onlyOwner` modifier on L236.
* Correctly calls function `increment()` from `Counters` on L238.
* Correctly calls function `Counters.Counter()` from `Counters` on L239.

Function `setSupply()` on L242:
* Correctly adds `onlyOwner` modifier on L242.

Function `handleSeries()` on L247:
* Correctly adds `onlyOwner` modifier on L247.

Function `assetTrait()` on L251:
* Correctly calls function `mod()` from `SafeMath` on L255.
* Correctly calls function `mod()` from `SafeMath` on L259.
* Correctly calls function `add()` from `SafeMath` on L260.
* Correctly calls function `mod()` from `SafeMath` on L267.
* Correctly calls function `mod()` from `SafeMath` on L270.
* Correctly calls function `sub()` from `SafeMath` on L281.
* Correctly calls function `add()` from `SafeMath` on L290.
* Correctly calls function `mod()` from `SafeMath` on L295.
* Correctly calls function `mod()` from `SafeMath` on L300.
* Correctly calls function `sub()` from `SafeMath` on L311.
* Correctly calls function `mod()` from `SafeMath` on L321.
* Correctly calls function `add()` from `SafeMath` on L323.

Function `getVaultBalance()` on L343:
* Correctly adds `onlyOwner` modifier on L343.

Function `sendVaultBalance()` on L347:
* Correctly adds `onlyOwner` modifier on L347.