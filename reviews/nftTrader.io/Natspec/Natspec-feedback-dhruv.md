# Natspec documentation  auditing of NFTTrader 

                                        By Dhruv Malik

## Abstract : 
doing an manual review of Audit_NFTTrader.io contracts specification on bc3cca5  ,  primarily  on the following factors:

- Natspec  explanation of the  overall contract (author , general use case ) , functions   , events , interface and other important abstract data types for clearly explain the important characterstics of the working  ( like parameters  access control , working as well as consistency with the documentation , facts that an developer and the user  needs to know etc).

- whether  there is use of  documentation that is dynamic , using the process like `@inheritdocs` to show the relations between the inheirted functions and classes .

Natspec documentation feedback :

both Types of  natspec  standards  are  not defined with identifiers  for most  of the   contracts and the functions that are defined in the documentation (specially TradeSwap.sol and BatchSwap.sol ). except  there is some documentation of the functions and contracts in the Batchswap .

- so i did added some natspec documentations  from my side in order to give more clarity , these contracts are being stored in the  natspec-contracts-dhruv/  on the tradeSwap contracts , and then elaborating the functions used for the transfer  , instantiation of the assets  , with @dev specification defining the  potential use of the function for reading/ writing the details from the contracts , and whether there are certain issues ( security or general) that need to be  taken care of.
