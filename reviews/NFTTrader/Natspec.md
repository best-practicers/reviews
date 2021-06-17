# Natspec

Created by: Anthony Graignic
Date: 2021-06-17
Commit ID(NFTTrader.io): bc3cca51004b903e4e6e3495f5bf53875ea59fd6

Note: the code provided only included the 2 folders `contracts` containing all the Solidity files and a `test` folder containing a single test file called `001_deployment_test.js`. Providing a `package.json` while not mandatory would have facilitate the audit.

## Summary

- There is 0 valid Natspec provided for the `contracts`.
- However the code is not completely empty of comments, only the `BatchSwap.sol` provide comment in a non-NatSpec format but those comments are really not useful e.g. "//Interface" for `abstract contract ERC20Interface {` L12-13.
- Some comments and function documentation are provided for the tests e.g. from L317 to L322 for the `checkOwnershipOfERC721Tokens` function in `001_deployment_test.js`.
- Some comments were written in Italian in the `test/001_deployment_test.js`. All comments should be done in one unique language (preferably English)
- There is no formating of files e.g. [prettier](https://github.com/prettier-solidity/prettier-plugin-solidity/) and some lines can make up to 186 char which decrease the code readability.
- A FIXME was left in `CKBridge.sol` indicating that some feature is missing in that case, the Ownership management.

## File Review

As the contracts did not contain NatSpec documentation but poorly Javascript-like documentation. The file review will only concern the single file containing comments: `BatchSwap.sol`

#### `BatchSwap.sol`

Comments provided in the code are not useful e.g.
| Line numbers | Observation |
|---|---|
| L12-13 | Comment is not helpful"//Interface" for `abstract contract ERC20Interface {` & Missing NatSpec documentation |
| L18 | Missing NatSpec documentation `ERC721Interface` contract |
| L23 | Missing NatSpec documentation `ERC1155Interface` contract |
| L27 | Missing NatSpec documentation for `CPInterface` contract |
| L32 | Missing NatSpec documentation for `customInterface` contract |
| L36 | Missing NatSpec documentation for `PunkProxy` contract |
| L44 | Missing NatSpec documentation for `proxyTransferPunk` function |
| L50 | Missing NatSpec documentation for `changeCurrentProxyOwner` function |
| L55 | Missing NatSpec documentation for `recoverPunk` function |
| L63 | Missing NatSpec documentation for `BatchSwap` contract |
| L90 | Missing NatSpec documentation for `swapStruct` struct |
| L99 | Missing NatSpec documentation for `swapStatus` enum |
| L102 | Missing NatSpec documentation for `swapIntent` struct |
| L119 | Missing NatSpec documentation for `paymentStruct` struct |
| L133 | Missing NatSpec documentation for `swapEvent` event |
| L134 | Missing NatSpec documentation for `paymentReceived` event |
| L141 | Missing NatSpec documentation for `createSwapIntent` function |
| L197 | Missing NatSpec documentation for `closeSwapIntent` function |
| L273 | Missing NatSpec documentation for `cancelSwapIntent` function |
| L309 | Missing NatSpec documentation for `setCryptoPunkAddress` function |
| L314 | Missing NatSpec documentation for `registerPunkProxy` function |
| L320 | Missing NatSpec documentation for `claimPunkOnProxy` function |
| L326 | Missing NatSpec documentation for `setTradeSquadAddress` function |
| L331 | Missing NatSpec documentation for `setVaultAddress` function |
| L336 | Missing NatSpec documentation for `setDappRelation` function |
| L341 | Missing NatSpec documentation for `setWhitelist` function |
| L346 | Missing NatSpec documentation for `editCounterPart` function |
| L352 | Missing NatSpec documentation for `setPayment` function |
| L358 | Missing NatSpec documentation for `getPunkProxy` function |
| L363 | Missing NatSpec documentation for `getWhiteList` function |
| L368 | Missing NatSpec documentation for `getWeiPayValueAmount` function |
| L373 | Missing NatSpec documentation for `getSwapIntentByAddress` function |
| L378 | Missing NatSpec documentation for `getSwapStructSize` function |
| L386 | Missing NatSpec documentation for `getSwapStruct` function |
| L403 | Missing NatSpec documentation for `supportsInterface` function |

- "//Interface" for `abstract contract ERC20Interface {` or `struct swapStruct {` L89-90 in `BatchSwap.sol`
