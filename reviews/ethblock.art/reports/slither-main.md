```bash
$:~/coding/blockart-contracts$ slither .
'npx hardhat compile' running
Nothing to compile

INFO:Detectors:
BlockArtFactory.collectCoins() (contracts/BFactory.sol#265-270) sends eth to arbitrary user
	Dangerous calls:
	- address(msg.sender).transfer(_amount) (contracts/BFactory.sol#269)
BlockArtFactory.collectBalance() (contracts/BFactory.sol#273-276) sends eth to arbitrary user
	Dangerous calls:
	- address(msg.sender).transfer(_amount) (contracts/BFactory.sol#275)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#functions-that-send-ether-to-arbitrary-destinations
INFO:Detectors:
BlockArtFactory.mintArt(address,uint256,uint256,string) (contracts/BFactory.sol#104-128) performs a multiplication on the result of a division:
	-sf = msg.value.sub(msg.value.div(sfm).mul(100)) (contracts/BFactory.sol#123)
BlockArtFactory.calcArtPrice(uint256,uint256) (contracts/BFactory.sol#164-203) performs a multiplication on the result of a division:
	-priceDiff = priceCeil.sub((blockDiff.mul(priceCeil.div(dutchLength)))) (contracts/BFactory.sol#187-188)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#divide-before-multiply
INFO:Detectors:
Reentrancy in BlockArtFactory.mintArt(address,uint256,uint256,string) (contracts/BFactory.sol#104-128):
	External calls:
	- _blockArt.mint(to,blockNumber,styleId,msg.value,metadata) (contracts/BFactory.sol#116)
	State variables written after the call(s):
	- psfb[blockNumber] = msg.value (contracts/BFactory.sol#118)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-1
INFO:Detectors:
BlockArtFactory.canMintWithStyle(uint256) (contracts/BFactory.sol#227-248) contains a tautology or contradiction:
	- diff < 0 (contracts/BFactory.sol#245)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#tautology-or-contradiction
INFO:Detectors:
BlockArtFactory.mintArt(address,uint256,uint256,string) (contracts/BFactory.sol#104-128) ignores return value by _blockArt.mint(to,blockNumber,styleId,msg.value,metadata) (contracts/BFactory.sol#116)
ERC721._mint(address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#333-344) ignores return value by _holderTokens[to].add(tokenId) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#339)
ERC721._mint(address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#333-344) ignores return value by _tokenOwners.set(tokenId,to) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#341)
ERC721._burn(uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#356-374) ignores return value by _holderTokens[owner].remove(tokenId) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#369)
ERC721._burn(uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#356-374) ignores return value by _tokenOwners.remove(tokenId) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#371)
ERC721._transfer(address,address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#387-402) ignores return value by _holderTokens[from].remove(tokenId) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#396)
ERC721._transfer(address,address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#387-402) ignores return value by _holderTokens[to].add(tokenId) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#397)
ERC721._transfer(address,address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#387-402) ignores return value by _tokenOwners.set(tokenId,to) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#399)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#unused-return
INFO:Detectors:
BlockArt.constructor(string).contractURI (contracts/BArt.sol#28) shadows:
	- ERC721Ref.contractURI() (contracts/ERC721Ref.sol#100-102) (function)
BlockStyle.constructor(string,string).baseURI (contracts/BStyle.sol#25) shadows:
	- ERC721.baseURI() (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#158-160) (function)
BlockStyle.constructor(string,string).contractURI (contracts/BStyle.sol#25) shadows:
	- ERC721Style.contractURI() (contracts/ERC721Style.sol#125-127) (function)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#local-variable-shadowing
INFO:Detectors:
BlockArtFactory.constructor(address,address)._artsAddr (contracts/BFactory.sol#67) lacks a zero-check on :
		- artsAddr = _artsAddr (contracts/BFactory.sol#68)
BlockArtFactory.constructor(address,address)._stylesAddr (contracts/BFactory.sol#67) lacks a zero-check on :
		- stylesAddr = _stylesAddr (contracts/BFactory.sol#69)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#missing-zero-address-validation
INFO:Detectors:
Reentrancy in BlockArtFactory.burnArt(uint256) (contracts/BFactory.sol#131-143):
	External calls:
	- _ba.burnToken(tokenId) (contracts/BFactory.sol#139)
	State variables written after the call(s):
	- coinsBalance = coinsBalance.add(msg.value) (contracts/BFactory.sol#140)
Reentrancy in ERC721Ref.mint(address,uint256,uint256,uint256,string) (contracts/ERC721Ref.sol#43-63):
	External calls:
	- _safeMint(to,newId) (contracts/ERC721Ref.sol#59)
		- returndata = to.functionCall(abi.encodeWithSelector(IERC721Receiver(to).onERC721Received.selector,_msgSender(),from,tokenId,_data),ERC721: transfer to non ERC721Receiver implementer) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#441-447)
		- (success,returndata) = target.call{value: value}(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#119)
	External calls sending eth:
	- _safeMint(to,newId) (contracts/ERC721Ref.sol#59)
		- (success,returndata) = target.call{value: value}(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#119)
	State variables written after the call(s):
	- _setTokenURI(newId,metadata) (contracts/ERC721Ref.sol#60)
		- _tokenURIs[tokenId] = _tokenURI (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#413)
Reentrancy in ERC721Style.mint(address,uint256,uint256,uint256,string) (contracts/ERC721Style.sol#41-57):
	External calls:
	- _safeMint(to,newId) (contracts/ERC721Style.sol#51)
		- returndata = to.functionCall(abi.encodeWithSelector(IERC721Receiver(to).onERC721Received.selector,_msgSender(),from,tokenId,_data),ERC721: transfer to non ERC721Receiver implementer) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#441-447)
		- (success,returndata) = target.call{value: value}(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#119)
	External calls sending eth:
	- _safeMint(to,newId) (contracts/ERC721Style.sol#51)
		- (success,returndata) = target.call{value: value}(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#119)
	State variables written after the call(s):
	- _setCanvasURI(newId,canvas) (contracts/ERC721Style.sol#56)
		- _scu[id] = uri (contracts/ERC721Style.sol#111)
	- _setStyleFeeMin(newId,feeMin) (contracts/ERC721Style.sol#55)
		- _sfmi[id] = amount (contracts/ERC721Style.sol#77)
	- _setStyleFeeMul(newId,feeMul) (contracts/ERC721Style.sol#54)
		- _sfmu[id] = amount (contracts/ERC721Style.sol#72)
	- _setStyleSupplyCap(newId,cap) (contracts/ERC721Style.sol#53)
		- _ssc[id] = cap (contracts/ERC721Style.sol#62)
	- _setCreator(newId,to) (contracts/ERC721Style.sol#52)
		- _stc[id] = who (contracts/ERC721Style.sol#67)
Reentrancy in BlockArtFactory.mintArt(address,uint256,uint256,string) (contracts/BFactory.sol#104-128):
	External calls:
	- _blockArt.mint(to,blockNumber,styleId,msg.value,metadata) (contracts/BFactory.sol#116)
	State variables written after the call(s):
	- coinsBalance = coinsBalance.add(msg.value.sub(sf)) (contracts/BFactory.sol#127)
	- scfb[styleId] = scfb[styleId].add(sf) (contracts/BFactory.sol#126)
Reentrancy in BlockArtFactory.mintStyle(address,uint256,uint256,uint256,string) (contracts/BFactory.sol#211-224):
	External calls:
	- _blockStyle.mint(to,cap,feeMul,feeMin,canvas) (contracts/BFactory.sol#221)
	State variables written after the call(s):
	- coinsBalance = coinsBalance.add(msg.value) (contracts/BFactory.sol#223)
Reentrancy in BlockArtFactory.remint(uint256,string) (contracts/BFactory.sol#146-156):
	External calls:
	- _blockArt.setTokenURI(tokenId,metadata) (contracts/BFactory.sol#153)
	State variables written after the call(s):
	- coinsBalance = coinsBalance.add(msg.value) (contracts/BFactory.sol#154)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-2
INFO:Detectors:
Reentrancy in BlockArtFactory.burnArt(uint256) (contracts/BFactory.sol#131-143):
	External calls:
	- _ba.burnToken(tokenId) (contracts/BFactory.sol#139)
	Event emitted after the call(s):
	- Burn(msg.sender,tokenId) (contracts/BFactory.sol#142)
Reentrancy in BlockArtFactory.remint(uint256,string) (contracts/BFactory.sol#146-156):
	External calls:
	- _blockArt.setTokenURI(tokenId,metadata) (contracts/BFactory.sol#153)
	Event emitted after the call(s):
	- ReMint(msg.sender,tokenId) (contracts/BFactory.sol#155)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-3
INFO:Detectors:
Address.isContract(address) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#26-35) uses assembly
	- INLINE ASM (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#33)
Address._verifyCallResult(bool,bytes,string) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#171-188) uses assembly
	- INLINE ASM (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#180-183)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#assembly-usage
INFO:Detectors:
Different versions of Solidity is used in :
	- Version used: ['>=0.6.0<0.8.0', '>=0.6.2<0.8.0', '^0.7.3']
	- ^0.7.3 (contracts/BArt.sol#18)
	- ^0.7.3 (contracts/BFactory.sol#18)
	- ABIEncoderV2 (contracts/BFactory.sol#19)
	- ^0.7.3 (contracts/BStyle.sol#18)
	- ^0.7.3 (contracts/ERC721Ref.sol#18)
	- ^0.7.3 (contracts/ERC721Style.sol#18)
	- ^0.7.3 (contracts/test/MockProxyRegistry.sol#1)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/access/Ownable.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/introspection/ERC165.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/introspection/IERC165.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#3)
	- >=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721.sol#3)
	- >=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Enumerable.sol#3)
	- >=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Metadata.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Receiver.sol#3)
	- >=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Context.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Counters.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/EnumerableMap.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/EnumerableSet.sol#3)
	- >=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Strings.sol#3)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#different-pragma-directives-are-used
INFO:Detectors:
Pragma version^0.7.3 (contracts/BArt.sol#18) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version^0.7.3 (contracts/BFactory.sol#18) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version^0.7.3 (contracts/BStyle.sol#18) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version^0.7.3 (contracts/ERC721Ref.sol#18) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version^0.7.3 (contracts/ERC721Style.sol#18) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version^0.7.3 (contracts/test/MockProxyRegistry.sol#1) necessitates a version too recent to be trusted. Consider deploying with 0.6.11
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/access/Ownable.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/introspection/ERC165.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/introspection/IERC165.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#3) is too complex
Pragma version>=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721.sol#3) is too complex
Pragma version>=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Enumerable.sol#3) is too complex
Pragma version>=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Metadata.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/token/ERC721/IERC721Receiver.sol#3) is too complex
Pragma version>=0.6.2<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Context.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Counters.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/EnumerableMap.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/EnumerableSet.sol#3) is too complex
Pragma version>=0.6.0<0.8.0 (node_modules/openzeppelin-solidity/contracts/utils/Strings.sol#3) is too complex
solc-0.7.3 is not recommended for deployment
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-versions-of-solidity
INFO:Detectors:
Low level call in Address.sendValue(address,uint256) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#53-59):
	- (success) = recipient.call{value: amount}() (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#57)
Low level call in Address.functionCallWithValue(address,bytes,uint256,string) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#114-121):
	- (success,returndata) = target.call{value: value}(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#119)
Low level call in Address.functionStaticCall(address,bytes,string) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#139-145):
	- (success,returndata) = target.staticcall(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#143)
Low level call in Address.functionDelegateCall(address,bytes,string) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#163-169):
	- (success,returndata) = target.delegatecall(data) (node_modules/openzeppelin-solidity/contracts/utils/Address.sol#167)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#low-level-calls
INFO:Detectors:
Parameter BlockStyle.setStyleSupplyCap(uint256,uint256)._id (contracts/BStyle.sol#60) is not in mixedCase
Parameter BlockStyle.setStyleSupplyCap(uint256,uint256)._cap (contracts/BStyle.sol#60) is not in mixedCase
Parameter BlockStyle.setStyleFeeMul(uint256,uint256)._id (contracts/BStyle.sol#68) is not in mixedCase
Parameter BlockStyle.setStyleFeeMul(uint256,uint256)._value (contracts/BStyle.sol#68) is not in mixedCase
Parameter BlockStyle.setStyleFeeMin(uint256,uint256)._id (contracts/BStyle.sol#79) is not in mixedCase
Parameter BlockStyle.setStyleFeeMin(uint256,uint256)._value (contracts/BStyle.sol#79) is not in mixedCase
Variable ERC721Ref._contractURI (contracts/ERC721Ref.sol#35) is not in mixedCase
Variable ERC721Style._contractURI (contracts/ERC721Style.sol#33) is not in mixedCase
Parameter MockProxyRegistry.setProxy(address,address)._address (contracts/test/MockProxyRegistry.sol#20) is not in mixedCase
Parameter MockProxyRegistry.setProxy(address,address)._proxyForAddress (contracts/test/MockProxyRegistry.sol#20) is not in mixedCase
Parameter ERC721.safeTransferFrom(address,address,uint256,bytes)._data (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#245) is not in mixedCase
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#conformance-to-solidity-naming-conventions
INFO:Detectors:
Redundant expression "this (node_modules/openzeppelin-solidity/contracts/utils/Context.sol#21)" inContext (node_modules/openzeppelin-solidity/contracts/utils/Context.sol#15-24)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#redundant-statements
INFO:Detectors:
Reentrancy in BlockArtFactory.collectStyleFees(uint256) (contracts/BFactory.sol#253-262):
	External calls:
	- address(msg.sender).transfer(_amount) (contracts/BFactory.sol#260)
	Event emitted after the call(s):
	- StyleFeeCollected(msg.sender,styleId,_amount) (contracts/BFactory.sol#261)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities-4
INFO:Detectors:
getPsfb(uint256) should be declared external:
	- BlockArtFactory.getPsfb(uint256) (contracts/BFactory.sol#300-302)
styleArtSupply(uint256) should be declared external:
	- ERC721Ref.styleArtSupply(uint256) (contracts/ERC721Ref.sol#75-77)
tokenToStyle(uint256) should be declared external:
	- ERC721Ref.tokenToStyle(uint256) (contracts/ERC721Ref.sol#79-82)
tokenToBlock(uint256) should be declared external:
	- ERC721Ref.tokenToBlock(uint256) (contracts/ERC721Ref.sol#84-87)
tokenToValue(uint256) should be declared external:
	- ERC721Ref.tokenToValue(uint256) (contracts/ERC721Ref.sol#89-92)
getStyleSupplyCap(uint256) should be declared external:
	- ERC721Style.getStyleSupplyCap(uint256) (contracts/ERC721Style.sol#82-90)
getCreator(uint256) should be declared external:
	- ERC721Style.getCreator(uint256) (contracts/ERC721Style.sol#92-95)
getStyleFeeMul(uint256) should be declared external:
	- ERC721Style.getStyleFeeMul(uint256) (contracts/ERC721Style.sol#97-100)
getStyleFeeMin(uint256) should be declared external:
	- ERC721Style.getStyleFeeMin(uint256) (contracts/ERC721Style.sol#102-105)
renounceOwnership() should be declared external:
	- Ownable.renounceOwnership() (node_modules/openzeppelin-solidity/contracts/access/Ownable.sol#54-57)
transferOwnership(address) should be declared external:
	- Ownable.transferOwnership(address) (node_modules/openzeppelin-solidity/contracts/access/Ownable.sol#63-67)
supportsInterface(bytes4) should be declared external:
	- ERC165.supportsInterface(bytes4) (node_modules/openzeppelin-solidity/contracts/introspection/ERC165.sol#35-37)
balanceOf(address) should be declared external:
	- ERC721.balanceOf(address) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#106-109)
name() should be declared external:
	- ERC721.name() (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#121-123)
symbol() should be declared external:
	- ERC721.symbol() (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#128-130)
tokenURI(uint256) should be declared external:
	- ERC721.tokenURI(uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#135-151)
tokenOfOwnerByIndex(address,uint256) should be declared external:
	- ERC721.tokenOfOwnerByIndex(address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#165-167)
totalSupply() should be declared external:
	- ERC721.totalSupply() (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#172-175)
tokenByIndex(uint256) should be declared external:
	- ERC721.tokenByIndex(uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#180-183)
approve(address,uint256) should be declared external:
	- ERC721.approve(address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#188-197)
setApprovalForAll(address,bool) should be declared external:
	- ERC721.setApprovalForAll(address,bool) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#211-216)
transferFrom(address,address,uint256) should be declared external:
	- ERC721.transferFrom(address,address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#228-233)
safeTransferFrom(address,address,uint256) should be declared external:
	- ERC721.safeTransferFrom(address,address,uint256) (node_modules/openzeppelin-solidity/contracts/token/ERC721/ERC721.sol#238-240)
Reference: https://github.com/crytic/slither/wiki/Detector-Documentation#public-function-that-could-be-declared-external
INFO:Slither:. analyzed (21 contracts with 72 detectors), 92 result(s) found
```