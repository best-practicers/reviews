## Failed Unit Test 13 message:

![](./images/failed_unit_test_13.png)

### Failing code:

*ETHmxMinter.test.ts*, test beginning at line 928 has the following lines:

> const amount = parseEther('10');
>
> const expected = parseEther('40');
>
> expect(await contract.ethmxFromEth(amount)).to.eq(expected);

Which calls the *ethmxFromEth()* function from *ETHmxMinter.sol*, which on line 356 has:

>uint256 amountOut = _ethmxCurve(amountETHIn, mp);

(I am assuming the math inside of *_ethmxCurve* gives *amountOut* a value of *20 ETHmx*)

After which, it checks the following conditional:

> "if (_inGenesis) {...}

That ends in

>amountOut.mul(2);

However, if it continues without going inside of the conditional, *ethmxFromEth()* ends with:

> return amountOut;

without multiplying by 2, which would return the *20 ETHmx* , rather than the actual *40 ETHmx* the test expected.

The cause of the error is because in Solidity, you cannot check a truthy value this way.

From the [Solditiy docs](https://docs.soliditylang.org/en/latest/control-structures.html):

>Note that there is no type conversion from non-boolean to boolean types as there is in C and JavaScript, so if (1) { ... } is not valid Solidity.