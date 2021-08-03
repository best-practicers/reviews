# Access Control
## Created by: [Dhruv Malik](https://github.com/dhruvmalik007)

## Summary
In general, there has been  good emphasis on adding the  modifiers in order to avoid the general  possible attacks. However, additional access control is needed  to avoid the  attack vector created from the critical function `swapIntent()`


## Scope

```
├── Docs.docx
└── contracts/
```

## File Review (based on the details being presented  concerning)

###  `docs.docx`
- nothing much mentioned regarding the  diagrams for the workflow of the projects . will be greate to make an diagram in showing the workflow of how the users on dapp will be interacting . 

###  2. `contracts/`

-   most important condition for using the  role based access  and security identifiers ( `ownable , pausable` ) are being extensively being used  for handling the  tradeSwap , batchVault and batchSwap. 
- thus using the tools like consensys surya , i visualised the functions  conditions and possiblity whether the states of the write functions (specially the set function corresponding to the set methods in the batchswap) , 

### `AXBridge.sol`

- Overall its  simply single function  ( but indeed important to be  exeucted to change the bridge access to AxleCore or other interoperable contract for the crosschain asset swap) this needs to be controlled by onlyOwner , but also possible , the an be better upgradablity pattern be created , with  possiblity to even add the [accessControl patterns like in openzeppelin](https://docs.openzeppelin.com/contracts/4.x/api/access).

### `Batchswap.sol`

- Overall, looks good. Functions that need the `onlyOwner` modifier have it.
- for conditional modifier , there needs to be some more in order to have more robust checks in insuring the certain indirect issues.
  - checking that whether `_punkContract` in `proxyTransferPunk()` is indeed following standards of  being similar contract as the actual cryptopunks contract , in order to avoid the attacks like [proxy upgrading](https://medium.com/nomic-labs-blog/malicious-backdoors-in-ethereum-proxies-62629adf3357). 
  
  - for the `changeCurrentProxyOwner()` function , even if the  check  for the owner is fine ,   can also be simplified by adding `onlyowner`  type modifier from the OZ. 

  - in the `checkswapIntent()` , after assigning the required gas , the logic for assigning the ownership  to the  `_punkcontracts` from the tradeswap ( from _swapIntent.addressOne to _swapIntent.status) cna be created an atomised call from an imported function , so as to avoid attacks to the changing of the other primitives .  

#### `BatchVault.sol`

- batchVault is being perfectly secured by ownable and pausable