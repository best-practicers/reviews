# Testing :
by [@GrandGarcon]().

##  Review summary :
the contracts are being reviewed from the hash commit : 

- commands for  creating the build , running the tests are not defined by the repo , thus adding quite a lot of redundant information , thus there needs to be definion of the 



## review process : 

- for running the tests for both versions  initially using  `npx hardhat test`( for both steakhouse v1 and v2), i  found that the trace of the tests are being not shown , instead  majority of  them were logs , thus 

thus resolving the issues , we found that following two tests are  failing 


```

1) SteakHouse
       With ERC/LP token added to the field
         should give proper STEAKs allocation to each pool:
     AssertionError: Expected "1366" to be equal 1333
      at Context.<anonymous> (test/SteakHouse.test.js:277:61)
      at processTicksAndRejections (node:internal/process/task_queues:96:5)

  1) SteakHouseV2
       With ERC/LP token added to the field
         should not distribute STEAKS if no one deposits:
     AssertionError: Expected "3901" to be equal 4001
      at Context.<anonymous> (test/SteakHouseV2.test.js:176:55)
      at runMicrotasks (<anonymous>)
      at processTicksAndRejections (node:internal/process/task_queues:96:5)
```


thus manually analysing  the tests :

- for the version 1 , the calculation of finding the allocation (L#256 - 277) logic needs to be  troubleshooted to find out whether the tests logic is not conforming to the standards or the vice versa .

  - but after doing the  checks of the logic and the contract , seems that the issues had been concerning the   incompatible version of the hardhat that has been creating issues of incorrect evaluation / representation of results in the assertions . thus upgrade the dependencies of the functions 


- also  in the tests , the  logs about the block  details are not necessary , and  negates the description of the assertions during  running the `npx hardhat test`command , its primarily due to the fact that in the test ,  for getting the time , the getTime function tries to return the block timestamp  , which in fact calls the function to display the time . thus an better alterantive is to  us another function , like [provider.getBlock](https://docs.ethers.io/v5/api/providers/provider/#Provider-getBlock). 


-  also for the test coverage  , there can be integration of  hardhat plugin solidity-coverage for testing the reachablity of the contracts .
   -  during coverage tests ,  some of the contracts compile size was bigger than the current limit on the mainnet (24kb) : both SteakHouse v1 and v2 , xSTEAK and iFUSD are having large contract size , thus need refactoring in their codebase , as being explained in the 


now  further  analysing the tests from the persepective of the [best practices](https://docs.onflow.org/dapp-deployment/contract-testing/#testing-requirements):  

  - in the SteakHouseV2 : the function like collect() function is not being tested  in  the script .
  - should also check some of the  integrated tests as being defined in the [testing of Masterchef contracts](https://github.com/sushiswap/sushiswap/blob/canary/test/MasterChefV2.test.ts).
  - 






















 



