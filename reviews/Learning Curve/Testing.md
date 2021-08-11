# Testing
## Created by: [@michaelbnewman](https://github.com/michaelbnewman)

## Review Comments (Summary)
* Make a `requirements.txt` file for use with `pip install -r requirements.txt`.
* Make a gitignored `.envrc` file to source the environment variables.
* Use Alchemy rather than Infura to make mainnet forking more accessible to learners.
* Explain (if possible) why tests-mainnet is generating the error `Locally compiled and on-chain bytecode do not match!`
* Include code coverage report as part of tests for better reference on completeness.
* Prioritize which missing sections in coverage to tackle next, and keep working towards 100%.

## Review Process (Notes)

```bash
$ lsb_release -a | grep Description
Description:	Ubuntu 20.04.2 LTS

$ python3 --version
Python 3.8.10

$ git clone https://github.com/michaelbnewman/learning-curve

$ cd learning-curve

# Confirm current commit hash
$ git log --pretty=oneline | head --lines=1
c2dbf17fa2a369a4350355709eb5adebfeaf07e8 Remove another pytest cache and add to gitignore

$ python3 -m venv .venv

$ source .venv/bin/activate

# Clear old brownie settings so its a fresh install
$ test -e "${HOME}/.brownie" && rm -f -r "${HOME}/.brownie"

$ pip install "eth-brownie==1.14.6"

$ pip freeze > requirements.txt

# Assuming nvm installed: https://github.com/nvm-sh/nvm
$ nvm use v14.17.3  # lts/fermium

$ npm install -g ganache-cli

$ ganache-cli --version
Ganache CLI v6.12.2 (ganache-core: 2.13.2)

$ brownie test tests -s
tests/test_operation_unit.py::test_full PASSED
tests/test_unit_kf.py::test_create_courses PASSED
tests/test_unit_kf.py::test_create_malicious_courses PASSED
tests/test_unit_kf.py::test_register PASSED
tests/test_unit_kf.py::test_register_malicious PASSED
tests/test_unit_kf.py::test_mint PASSED
tests/test_unit_kf.py::test_mint_malicious PASSED
tests/test_unit_kf.py::test_mint_diff_checkpoints PASSED
tests/test_unit_kf.py::test_redeem PASSED
tests/test_unit_kf.py::test_redeem_malicious PASSED
tests/test_unit_kf.py::test_redeem_diff_checkpoints PASSED
tests/test_unit_kf.py::test_verify PASSED
tests/test_unit_kf.py::test_verify_malicious PASSED
tests/test_unit_kf.py::test_mint_lc_not_initialised PASSED
tests/test_unit_lc.py::test_init PASSED
tests/test_unit_lc.py::test_init_malicious PASSED
tests/test_unit_lc.py::test_mint PASSED
tests/test_unit_lc.py::test_burn PASSED
======================== 18 passed in 138.55s (0:02:18) ========================
Terminating local RPC client...

$ export WEB3_INFURA_PROJECT_ID=""  # fill between quotes with your API key

$ export ETHERSCAN_TOKEN=""  # fill between quotes with your API key

$ brownie test tests-mainnet --network=mainnet-fork -s
Launching 'ganache-cli --port 8545 --gasLimit 12000000 --accounts 10 --hardfork istanbul --mnemonic brownie --fork https://mainnet.infura.io/v3/${WEB_INFURA_PROJECT_ID} --chainId 1'...
# Freezes here. Since I have a free level Infura account, it doesn't have access to archive node data, so mainnet forking will not work.

# Try again with alchemy:
# This replaces Infura mainnet with Alchemy mainnet
$ export ALCHEMY_API_KEY=""  # fill between quotes with your API key
$ brownie networks delete mainnet
$ brownie networks add "Ethereum" "mainnet" host="https://eth-mainnet.alchemyapi.io/v2/${ALCHEMY_API_KEY}" chainid=1 explorer="https://api.etherscan.io/api"


$ brownie test tests-mainnet --network=mainnet-fork -s
============================================================== warnings summary ===============================================================
tests-mainnet/test_mainnet_kf.py::test_batch_success
tests-mainnet/test_mainnet_kf.py::test_register_diff_batches
tests-mainnet/test_mainnet_kf.py::test_mint
tests-mainnet/test_mainnet_kf.py::test_mint_diff_checkpoints
tests-mainnet/test_mainnet_kf.py::test_redeem
tests-mainnet/test_mainnet_kf.py::test_redeem_diff_checkpoints
tests-mainnet/test_operation_mainnet.py::test_full_mint
tests-mainnet/test_operation_mainnet.py::test_full_redeem
  /home/mike/Documents/finances/cryptocurrencies/ethereum/kernel/best-practicers/repos/learning-curve/.venv/lib/python3.8/site-packages/brownie/network/contract.py:1221: BrownieCompilerWarning: 0x19D3364A399d251E894aC732651be8B0E4e85001: Locally compiled and on-chain bytecode do not match!
    warnings.warn(

tests-mainnet/test_mainnet_kf.py::test_mint
tests-mainnet/test_mainnet_kf.py::test_mint_diff_checkpoints
tests-mainnet/test_mainnet_kf.py::test_redeem
tests-mainnet/test_mainnet_kf.py::test_redeem_diff_checkpoints
tests-mainnet/test_operation_mainnet.py::test_full_mint
tests-mainnet/test_operation_mainnet.py::test_full_redeem
  /home/mike/Documents/finances/cryptocurrencies/ethereum/kernel/best-practicers/repos/learning-curve/.venv/lib/python3.8/site-packages/brownie/network/contract.py:1221: BrownieCompilerWarning: 0x9f51F4df0b275dfB1F74f6Db86219bAe622B36ca: Locally compiled and on-chain bytecode do not match!
    warnings.warn(

-- Docs: https://docs.pytest.org/en/stable/warnings.html
================================================= 10 passed, 14 warnings in 373.66s (0:06:13) =================================================
Terminating local RPC client...

# Redo test with coverage report:
# https://eth-brownie.readthedocs.io/en/stable/tests-coverage.html
$ brownie test tests --coverage
================================================================== Coverage ===================================================================


  contract: BasicERC20 - 65.3%
    BasicERC20.mint - 100.0%
    Context._msgSender - 100.0%
    ERC20.approve - 100.0%
    ERC20.balanceOf - 100.0%
    ERC20.transfer - 100.0%
    ERC20.transferFrom - 100.0%
    ERC20._transfer - 83.3%
    ERC20._approve - 75.0%
    ERC20._mint - 75.0%
    ERC20.allowance - 0.0%
    ERC20.decimals - 0.0%
    ERC20.decreaseAllowance - 0.0%
    ERC20.increaseAllowance - 0.0%
    ERC20.name - 0.0%
    ERC20.symbol - 0.0%
    ERC20.totalSupply - 0.0%

  contract: KernelFactory - 70.6%
    Address.functionCall - 100.0%
    Address.isContract - 100.0%
    Counters.current - 100.0%
    Counters.increment - 100.0%
    KernelFactory.createCourse - 100.0%
    KernelFactory.getCurrentBatchTotal - 100.0%
    KernelFactory.getNextCourseId - 100.0%
    KernelFactory.getUserCourseEligibleFunds - 100.0%
    KernelFactory.register - 100.0%
    KernelFactory.verify - 100.0%
    SafeERC20.safeTransfer - 100.0%
    SafeERC20.safeTransferFrom - 100.0%
    KernelFactory.mint - 83.3%
    KernelFactory.getEligibleAmount - 76.4%
    Address.functionCallWithValue - 75.0%
    SafeERC20._callOptionalReturn - 75.0%
    Address._verifyCallResult - 62.5%
    KernelFactory._verify - 50.0%
    KernelFactory.getUserCourseFundsRemaining - 50.0%
    KernelFactory.redeem - 20.0%
    KernelFactory.batchDeposit - 0.0%
    KernelFactory.getBlockRegistered - 0.0%
    KernelFactory.getCurrentBatchId - 0.0%

  contract: LearningCurve - 58.7%
    Address.functionCall - 100.0%
    Address.isContract - 100.0%
    Context._msgSender - 100.0%
    ERC20.approve - 100.0%
    ERC20.balanceOf - 100.0%
    ERC20.totalSupply - 100.0%
    LearningCurve.doLn - 100.0%
    LearningCurve.getBurnableForReserveAmount - 100.0%
    LearningCurve.initialise - 100.0%
    LearningCurve.mintForAddress - 100.0%
    PRBMathUD60x18.ln - 100.0%
    SafeERC20.safeTransfer - 100.0%
    SafeERC20.safeTransferFrom - 100.0%
    PRBMathUD60x18.log2 - 91.7%
    Address.functionCallWithValue - 75.0%
    ERC20._approve - 75.0%
    ERC20._burn - 75.0%
    ERC20._mint - 75.0%
    LearningCurve.burn - 75.0%
    LearningCurve.mint - 75.0%
    SafeERC20._callOptionalReturn - 75.0%
    Address._verifyCallResult - 62.5%
    PRBMath.mostSignificantBit - 41.2%
    ERC20._transfer - 0.0%
    ERC20.allowance - 0.0%
    ERC20.decimals - 0.0%
    ERC20.decreaseAllowance - 0.0%
    ERC20.increaseAllowance - 0.0%
    ERC20.name - 0.0%
    ERC20.symbol - 0.0%
    ERC20.transfer - 0.0%
    ERC20.transferFrom - 0.0%

======================================================= 18 passed in 404.96s (0:06:44) ========================================================

```
