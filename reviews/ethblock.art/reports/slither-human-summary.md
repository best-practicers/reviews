```bash
$:~/coding/blockart-contracts$ slither . --print human-summary
'npx hardhat compile' running
Compiling 21 files with 0.7.3
Compilation finished successfully

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


INFO:Printers:
Compiled with Builder
Number of lines: 736 (+ 1894 in dependencies, + 26 in tests)
Number of assembly lines: 0
Number of contracts: 5 (+ 15 in dependencies, + 1 tests) 

Number of optimization issues: 23
Number of informational issues: 42
Number of low issues: 13
Number of medium issues: 12
Number of high issues: 2

Use: Openzeppelin-Ownable, Openzeppelin-SafeMath, Openzeppelin-ERC721
ERCs: ERC721, ERC165

+-----------------+-------------+---------------+------------+--------------+--------------------+
|       Name      | # functions |      ERCS     | ERC20 info | Complex code |      Features      |
+-----------------+-------------+---------------+------------+--------------+--------------------+
|     BlockArt    |      68     | ERC165,ERC721 |            |      No      |                    |
| BlockArtFactory |      37     |               |            |      No      |    Receive ETH     |
|                 |             |               |            |              |      Send ETH      |
|                 |             |               |            |              | Tokens interaction |
|                 |             |               |            |              |    AbiEncoderV2    |
|    BlockStyle   |      77     | ERC165,ERC721 |            |      No      |                    |
+-----------------+-------------+---------------+------------+--------------+--------------------+
INFO:Slither:. analyzed (21 contracts)

```