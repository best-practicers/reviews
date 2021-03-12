# Testing
## Commit-SHA: [eeda149192144921c4ebbd74efa6d1f2c4e85cd8](https://github.com/adrianleb/blockart-contracts/commit/eeda149192144921c4ebbd74efa6d1f2c4e85cd8)
## Done by: [mariuspod](https://github.com/mariuspod)
### Reviewed by:

## Summary
* Very few code paths tested.
* Tests do not pass.
* API keys to Etherscan and Alchemy published in git repo (might become a problem if opensourced)
* Multiple vulnerabilities detected, slither report is attached.
* Testing coverage is at 20% which is very low.

## Recommendations
* Fix the tests
* Improve testing coverage, set your goal to 100%!
* Try to add slither into the CI/CD pipeline to fail early
* pass API keys via local ENV variables / files which are not persisted inside the repo to avoid unattended problems

## Testing reports

### Slither

[slither](https://github.com/crytic/slither) is a powerful vulnerability detector that has been used to analyze all solidity contracts.
Here are the reports:

* [main report](reports/slither-main.md)
* [human-summary](reports/slither-human-summary.md)

### Solidity test code coverage

With [solidity-coverage](https://hardhat.org/plugins/solidity-coverage.html) it's possible to test and improve on the testing code coverage:

* [coverage report](reports/coverage.md)

### Initial observations
* Tests only check for reverts
* Tests are for functions not in diagram
    * Diagram helps for understanding
    * Is diagram out of date?
* Access control for diagram

### Running tests
```
blockart-contracts$ yarn hardhat test test/sample-test.js 

Error HH8: There's one or more errors in your config file:

  * Invalid value {"chainId":1,"url":"https://eth-mainnet.alchemyapi.io/v2/eUPiqatfspumnJP7GuKwHwEZJUBtx-oC","accounts":["0x:)"]} for HardhatConfig.networks.mainnet - Expected a value of type HttpNetworkConfig.
```

* Should not be able to see their api key in `hardhat.config.js`


```
blockart-contracts$ yarn hardhat test test/sample-test.js 
yarn run v1.22.5
$ /home/carl/Documents/best-practicers/projects/blockart-contracts/node_modules/.bin/hardhat test test/sample-test.js


Token deployed to: 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
  BlockArt
    ✓ Cant mint from Bart directly
    1) Cant change tokenURI from Bart directly
(node:83029) UnhandledPromiseRejectionWarning: Error: missing argument: passed to contract (count=1, expectedCount=2, code=MISSING_ARGUMENT, version=contracts/5.0.8)

    2) Cant change contractURI from Bart directly

  BlockStyle
    ✓ Cant mint from BStyle directly


  2 passing (4s)
  2 failing

  1) BlockArt
       Cant change tokenURI from Bart directly:
     AssertionError: Expected an exception but none was received
      at expectException (node_modules/@openzeppelin/test-helpers/src/expectRevert.js:25:10)
      at Context.<anonymous> (test/sample-test.js:90:5)

  2) BlockArt
       Cant change contractURI from Bart directly:

      Wrong kind of exception received
      + expected - actual

      -too many arguments: passed to contract (count=1, expectedCount=0, code=UNEXPECTED_ARGUMENT, version=contracts/5.0.8)
      +revert
      
      at expectException (node_modules/@openzeppelin/test-helpers/src/expectRevert.js:20:30)
      at Context.<anonymous> (test/sample-test.js:94:5)
```