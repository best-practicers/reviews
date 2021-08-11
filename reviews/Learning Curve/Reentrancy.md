# Learning-Curve audit : 

## summary 

This review by the Best Practicers covers Gitcoin KERNEL's Learning Curve on commit [61fea35](https://github.com/kernel-community/learning-curve/commit/61fea3584a920b33dab3753dd08cea1872284bdd).

# Reviews :

## reentrancy :

I firstly   analysed the higher level call graphs (credits to consensys surya) on the protocol to find the inter contract calls , specially focusing on  following access functions  ( based on the slither-vscode detection ):

## KernelFactory
- KernelFactory.batchDeposit() 
- KernelFactory.mint() 
- KernelFactory.register()

## LearningCurve:
- burn (). 
- mint().
-mintForAddress().


then following the list of the [best practices](https://github.com/best-practicers/resources/tree/main/reentrancy)  :

### ReentrancyGuards  / checks-effects-interaction pattern :
-  during the  analysis of KernelFactory and LearningCurve , i did found that on some places   check-effects-interaction  pattern has been used , but some functions needed  to implement them to avoid the hijacking of the external calls .for instance 
   -  for example KernelFactory.register()( L#173 - 180)  has  effected the change ( by sending the erc20 token) before doing the changes in the state ) so in absense of the  checks of which entity doing the call and non atomicity , there can be potential eavesdropping .
   -  also the  primitives being used here (block.number  , msg.sender) are insecure against the frontrunning attacks , openzeppelin provides certain functions (although appplicable only when you use the relayer with the GSN contracts) or implement simpke helper function [like](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Context.sol).
  
   -  similarly in mint function(L#288 - 290) , the mintForAddress is an external call , which can be dropped   in a way so as not to emit the LearnMintedFromCourse after getting the shares .

- an simpler check is to add the `nonReentrant` modifier to the functions to the openzeppelin( `import  @openzeppelin/contracts/utilities/ReentrancyGuard` ) , this will  insure atomicity of the call for an particualr external call .

