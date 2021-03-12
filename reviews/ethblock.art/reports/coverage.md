$:~/coding/blockart-contracts$ npx hardhat coverage

Version
=======
> solidity-coverage: v0.7.16

Instrumenting for coverage...
=============================

> BArt.sol
> BFactory.sol
> BStyle.sol
> ERC721Ref.sol
> ERC721Style.sol
> test/MockProxyRegistry.sol

Compilation:
============

Compiling 21 files with 0.7.3
contracts/test/MockProxyRegistry.sol: Warning: SPDX license identifier not provided in source file. Before publishing, consider adding a comment containing "SPDX-License-Identifier: <SPDX-License>" to each source file. Use "SPDX-License-Identifier: UNLICENSED" for non-open-source code. Please see https://spdx.org for more information.

openzeppelin-solidity/contracts/introspection/ERC165.sol:24:5: Warning: Visibility for constructor is ignored. If you want the contract to be non-deployable, making it "abstract" is sufficient.
    constructor () internal {
    ^ (Relevant source part starts here and spans across multiple lines).

openzeppelin-solidity/contracts/token/ERC721/ERC721.sol:93:5: Warning: Visibility for constructor is ignored. If you want the contract to be non-deployable, making it "abstract" is sufficient.
    constructor (string memory name_, string memory symbol_) public {
    ^ (Relevant source part starts here and spans across multiple lines).

openzeppelin-solidity/contracts/access/Ownable.sol:26:5: Warning: Visibility for constructor is ignored. If you want the contract to be non-deployable, making it "abstract" is sufficient.
    constructor () internal {
    ^ (Relevant source part starts here and spans across multiple lines).

contracts/BFactory.sol:27:1: Warning: Contract code size exceeds 24576 bytes (a limit introduced in Spurious Dragon). This contract may not be deployable on mainnet. Consider enabling the optimizer (with a low "runs" value!), turning off revert strings, or using libraries.
contract BlockArtFactory is Ownable {
^ (Relevant source part starts here and spans across multiple lines).

Compilation finished successfully

Network Info
============
> HardhatEVM: v2.1.1
> network:    hardhat

web3-shh package will be deprecated in version 1.3.5 and will no longer be supported.
web3-bzz package will be deprecated in version 1.3.5 and will no longer be supported.


Token deployed to: 0xc6e7DF5E7b4f2A278906862b61205850344D4e7d
  BlockArt
    ✓ Cant mint from Bart directly
    1) Cant change tokenURI from Bart directly
(node:3089) UnhandledPromiseRejectionWarning: Error: missing argument: passed to contract (count=1, expectedCount=2, code=MISSING_ARGUMENT, version=contracts/5.0.12)
    at Logger.makeError (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/logger/src.ts/index.ts:205:28)
    at Logger.throwError (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/logger/src.ts/index.ts:217:20)
    at Logger.checkArgumentCount (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/logger/src.ts/index.ts:276:18)
    at /home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/src.ts/index.ts:159:12
    at step (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:48:23)
    at Object.next (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:29:53)
    at /home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:23:71
    at new Promise (<anonymous>)
    at __awaiter (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:19:12)
    at populateTransaction (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:138:12)
    at Contract.<anonymous> (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/src.ts/index.ts:339:33)
    at step (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:48:23)
    at Object.next (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:29:53)
    at fulfilled (/home/marius/coding/blockart-contracts/node_modules/@ethersproject/contracts/lib/index.js:20:58)
(node:3089) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). (rejection id: 22)
(node:3089) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
    2) Cant change contractURI from Bart directly

  BlockStyle
    ✓ Cant mint from BStyle directly


  2 passing (4s)
  2 failing

  1) BlockArt
       Cant change tokenURI from Bart directly:
     AssertionError: Expected an exception but none was received
      at expectException (node_modules/@openzeppelin/test-helpers/src/expectRevert.js:25:10)

  2) BlockArt
       Cant change contractURI from Bart directly:

      Wrong kind of exception received
      + expected - actual

      -too many arguments: passed to contract (count=1, expectedCount=0, code=UNEXPECTED_ARGUMENT, version=contracts/5.0.12)
      +revert

      at expectException (node_modules/@openzeppelin/test-helpers/src/expectRevert.js:20:30)



------------------------|----------|----------|----------|----------|----------------|
File                    |  % Stmts | % Branch |  % Funcs |  % Lines |Uncovered Lines |
------------------------|----------|----------|----------|----------|----------------|
 contracts/             |     20.9 |     9.09 |     19.7 |     20.9 |                |
  BArt.sol              |       25 |      100 |       25 |       25 |       33,38,42 |
  BFactory.sol          |    12.96 |     3.57 |     9.09 |    12.96 |... 371,372,373 |
  BStyle.sol            |    13.33 |        0 |     12.5 |    13.33 |... 74,76,80,84 |
  ERC721Ref.sol         |        5 |        0 |     12.5 |        5 |... 6,90,91,101 |
  ERC721Style.sol       |    63.33 |       25 |    53.85 |    63.33 |... 115,116,126 |
 contracts/test/        |        0 |      100 |        0 |        0 |                |
  MockProxyRegistry.sol |        0 |      100 |        0 |        0 |             24 |
------------------------|----------|----------|----------|----------|----------------|
All files               |    20.79 |     9.09 |     19.4 |    20.79 |                |
------------------------|----------|----------|----------|----------|----------------|

> Istanbul reports written to ./coverage/ and ./coverage.json
Error in plugin solidity-coverage: ❌ 2 test(s) failed under coverage.

For more info run Hardhat with --show-stack-traces
