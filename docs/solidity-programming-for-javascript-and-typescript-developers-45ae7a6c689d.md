# 面向 Javascript 和 Typescript 开发人员的可靠性编程

> 原文：<https://medium.com/coinmonks/solidity-programming-for-javascript-and-typescript-developers-45ae7a6c689d?source=collection_archive---------2----------------------->

![](img/505bd3ec12d6d3d8af928b27fe9cb579.png)

Solidity logo

您一定听说过智能合同、令牌、分散式应用程序、NFTs、分散式金融、令牌等术语。Solidity 是构建上述术语的主要编程语言之一。

**那么什么是坚固性呢？**

Solidity 是一种面向对象的高级语言，用于实现**智能合约。**

**智能合约**是管理以太坊国家或任何其他区块链国家的账户行为的程序，solidity 可以与之进行交互。

Solidity 是静态类型的，支持继承、库和其他特性。

一个人可以用坚固来建造什么

使用 Solidity，您可以创建用于投票、众筹、盲目拍卖、令牌、NFT 和多签名钱包等用途的合同。

**注:**在深入研究 Solidity 编程之前，您应该对区块链及其工作原理有一个大致的了解，并且对以太坊区块链也有一个很好的了解

**坚固性代码结构**

Solidity 代码有点类似于 Javascript/Typescript，这并不牵强，因为 Javascript 是 Solidity 的影响之一。

Solidity 是针对以太坊虚拟机(EVM)构建的， **Solidity 是图灵完成**，不像比特币的脚本不是。

实体文件用。sol 扩展，例如 Auction.sol

```
// Solidity contract structure//license
//SPDX-License-Identifier: MIT// compiler versioning
pragma solidity ^0.8.0;// import statements
import '@openzeppelin/contracts/token/ERC721/ERC721.sol';// Contract declaration
contract NFT {
  // Solidity variables
  address public manager;
  uint private _counter; // contract constructor
  constructor() {
    manager = msg.sender;  
  } // functions
  function getNFT() external view returns(uint256) {
    return _counter;
  }}// Or //license
//SPDX-License-Identifier: MIT// compiler versioning
pragma solidity ^0.8.0;library Counters {
   // Solidity struct
   struct Counters {
     *uint256* _value;
   } *function* current(*Counter* *storage* *counter*) *internal* *view* returns      (*uint256*) {
     return counter._value;
   }
}// Or//license
//SPDX-License-Identifier: MIT// compiler versioning
pragma solidity ^0.8.0;*interface* IERC721 { *event* Transfer(*address* *indexed* *from*, *address* *indexed* *to*, *uint256*  *indexed* *tokenId*); *function* ownerOf(*uint256* *tokenId*) *external* *view* returns (*address* *owner*);}
```

实体文件(。sol)只能存放契约(契约{})抽象或非抽象、接口(接口{})或库(库{})。

**注意:所有*实体声明和指令必须以分号(；)，而花括号决定任意数量的指令或声明的开始和结束:如函数、修饰符、结构、枚举和契约本身。***

**密实度类型**

布尔值(bool)、整数(int/uint)、定点数(fixed/ufixed)、枚举、映射、结构和地址。

```
bool sold;
int num;
uint counter;
fixed dec;
ufixed dex;
address owner;
address payable manager;// Enum
enum FreshJuiceSize{ SMALL, MEDIUM, LARGE }
FreshJuiceSize choice;// mapping
mapping(string => string) names;// struct
*struct* MarketToken {
  *uint256* itemId;
  *address* nftContract;
  *uint256* tokenId;
  *address* *payable* seller;
  *address* *payable* owner;
  *uint256* price;
  *bool* sold;
}*mapping*(*uint256* => MarketToken) idToMarketToken;idToMarketToken[itemId] = MarketToken(
  itemId,
  nftContract,
  tokenId,
  *payable*(msg.sender),
  *payable*(*address*(0)),
  price,
  false
);
```

你可以在这里详细阅读

**稠度变量**

**状态变量——其值永久存储在合同存储器中的变量。**

**局部变量——v**其值在函数执行期间出现的变量。

**全局变量—** 全局名称空间中存在特殊变量，用于获取有关区块链的信息。

**变量示例**

```
// State Variables
contract SolidityState {
   uint public stateData;      // State variable
   constructor() public {
      stateData = 10;   // Using State variable
   }
}// Local Variables
contract SolidityLocal {
   function getResult() public view returns(uint){
      uint x = 1; // local variable
      uint y = 2;
      uint result = x + y;
      return result; //access the local variable
   }
}// Global Variables
contract SolidityGlobal {
   address payable public manager;      // State variable
   constructor() public {
      magager = payable(msg.sender);   
      /* msg.sender is a global variable, which holds the address of                     the address of the request sender */
   }
}
```

您应该已经注意到，Solidity 注释风格与 Javascript 注释风格相同//对于单行注释，和/**/对于多行注释。

同样，当声明 Solidity 变量时，你必须以一个类型开始，例如 unit，因为 Solidity 是静态类型的，不像 Javascript 是松散类型的

```
let name = "Raphael";
```

，或在变量名后添加变量类型的 Typescript

```
const name: string = “Nene”;
```

在变量类型之后，声明变量可见性(公共/私有)，然后是变量名。

注意:变量可见性应该用于状态变量，而不是局部变量。当你公开一个变量时，Solidity 自动为你的变量创建一个 getter 函数。

```
contract MyVariable {
  string public fullName = "Raphael Eyerin"; function setName(string memory _fullName) public {
     fullName = _fullName;  
  }
}
```

当这段代码被编译时，Solidity 将创建一个名为 fullName()的函数来访问 fullName 变量，所以如果你将变量声明为 public，就不需要创建 getter 函数。

**可靠性条件语句**

Solidity 条件语句类似于 Javascript 和 Typescript 的条件语句，但是 Solidity 没有 switch 语句。

示例 if、if-else 和 if-else if

```
// If Condition
contract ConditionTest {
   function test(uint a, uint b) external pure returns(string) {
      string ans = "A is greater";
      if(b > a) {
        ans = "B is greater";
      }
      return ans;
   }
}// If-Else Condition
contract ConditionTest {
   function test(uint a, uint b) external pure returns(uint) {
     if(b > a) {
        return b;
     } else {
        return a;
     }      
   }
}// If-Else If Condition
contract ConditionTest {
   function test(uint a, uint b) external pure returns(string) {
      string ans;
      if(a > 500) {
        ans = "I will give you 1000 wei";
      } else if (a > 250) {
        ans = "I will give you 500 wei";
      } else if (b > a) {
        ans = "I will give you 250 wei";
      } else {
        ans = "I will give you 100 wei";
      }      
      return ans;
   }
}
```

**实度循环**

同样，循环、while 循环和 do-while 循环的可靠性与 Javascript 相同

环

```
// for loop
contract SolidityTest {
  function makeAll(uint maxNum) external pure returns(uint) 
     uint sum;
     for (uint j = 0; j < maxNum; j++) {  //for loop example
       sum += j;        
     }
     return sum;
  }
}// While loop
contract SolidityTest {
  function makeAll(uint maxNum) external pure returns(uint) 
     uint sum;
     uint a = maxNum - 1; while(a > 0) {  //while loop example
       sum += j;
       a--;       
     }
     return sum;
  }
}
```

Do while 不常使用，但它也类似于 Javascript，你也可以在 Solidity (break/continue)中使用循环控制语句。

**坚固性功能**

这就是如何在 Solidity 中定义一个函数

```
function function-name(parameter-list) scope returns() {
   //statements
}function setName(string memory _name) public {
  name = _name;
}function getName() external returns(string) {
  return name;
}
```

它以 Javascript 这样的函数关键字开始，然后是函数名。Solidity 函数的右边看起来不同于 Javascript 函数，你必须声明函数的作用域，以及函数返回值的返回类型。Typescript 还在函数的右侧声明了函数返回类型，但使用了不同的语法

```
let name: string = "";
public function getName(): string {
   return name; 
}
```

在 Solidity 中调用函数也类似于在 Javascript 中调用函数的方式

```
// Calling getName() function
string name = getName();
```

函数可见性类型

Solidity 有四种功能可见性类型:**私有、公共、外部和内部。**函数可见性允许我们轻松地保护契约的某些部分，而不必编写太多的自定义逻辑。

**私有:**私有函数只能被主契约本身调用。尽管这不是默认设置，但通常最好保持函数的私有性，除非需要一个可见性更高的作用域。

**public:** 可以从所有潜在方调用公共函数。除非另有说明，否则默认情况下所有函数都是公共的

**外部:**外部函数只能从第三方调用。不能从主合同本身或从它派生的任何合同中调用它。

外部函数的好处是它们可以更高效，因为它们的参数不需要复制到内存中。因此，在可能的情况下，最好保持逻辑只需要由`external`函数的外部方访问。

**内部:**一个内部函数可以被主契约本身以及任何派生的契约调用。与`private`函数一样，尽可能保留函数`internal`通常是个好主意。

Solidity 函数可以有一个**视图，或者纯**属性，**视图函数**是只读函数，确保状态变量在调用后不能被修改，而**纯函数**不读取或修改状态变量，只使用传递给函数的参数或其中存在的局部变量返回值。

功能在坚固性上也可以重载。

功能概述

```
*// SPDX-License-Identifier: MIT* 
pragma solidity ^0.8.10;  
contract FunctionTest {
   string private name;
   uint age;
   address manager; constructor() {
     // call internal function
     setOwner(msg.sender);
   }

   // external view function
   function getName() external view returns(string) {
     return name;
   }

   // external view function
   function setOwner(address _manager) intenal {
     manager = _manager;
   } // Public function
   function setAge(uint _age) public (string) {
     age = _age;
   } // Pure function
   function getResult() **public** pure returns(uint product, uint sum)
   {              
      uint num1 = 2;
      uint num2 = 4; product = num1 * num2; 
     sum = num1 + num2;
   } // function overloading in Solidity
   function getSum(uint a, uint b) public pure returns(uint){      
      return a + b;
   } function getSum(uint a, uint b, uint c) 
   public pure returns(uint) {      
      return a + b + c;
   }}
```

功能修饰符

修饰符是可以在函数调用之前和/或之后运行的代码。

修饰符可用于:

*   限制访问
*   验证输入
*   防范重入黑客攻击

例子

```
*// SPDX-License-Identifier: MIT* pragma solidity ^0.8.10; contract FunctionMod {     
  *// We will use these variables to demonstrate how to use*    
  *// modifiers.*     
  address public owner;     
  uint public x = 10;     
  bool public locked; constructor() {         
    *// Set the transaction sender as the owner  of the contract.*                
    owner = msg.sender;     
  }

  *// Modifier to check that the caller is the owner of*     
  *// the contract.*  

  modifier onlyOwner() {           
    require(msg.sender == owner, "Not owner");         
    *// Underscore is a special character only used inside*         
    *// a function modifier and it tells Solidity to
*         
    *// execute the rest of the code.*         
    _;  
  } *// Modifiers can take inputs. This modifier checks that the*     
  *// address passed in is not the zero address.* 

  modifier validAddress(address _addr) {         
    require(_addr != address(0), "Not valid address");         
    _;     
  }

  function changeOwner(address _newOwner) 
  public onlyOwner   validAddress(_newOwner) {         
    owner = _newOwner;     
  }}
```

你应该阅读更多关于可靠性函数的内容，并学习我在这篇文章中没有提到的东西。

**坚固性错误处理**

Solidity 中处理错误的方式不同于 Javascript 中处理错误的方式，Solidity 中有三个函数可用于处理错误:require、assert 和 revert。断言用于内部错误。

```
*// SPDX-License-Identifier: MIT* 
pragma solidity ^0.8.10;  
contract Error {
  uint num;
  uint256 balance; // Assert
  function testAssert(uint _num) public {         
    *// Assert should only be used to test for internal errors
    num =* _num;
    /* If the  pass a function parameter other than zero in this    function it will revert to its initial state
   */               
    assert(num == 0);     
  } // Revert 
  function testRevert(uint num) public {         
    *// Revert is useful when the condition to check is complex.    num =* _num;           
    if (num <= 10) {             
      revert("Input must be greater than 10");
    }
  } // Require
  function testRequire(uint256 _amount) public {
     uint oldBalance = balance;         
     uint newBalance = balance + _amount;

     *// balance + _amount does not overflow if balance + _amount >=  balance*         
    require(newBalance >= oldBalance, "Overflow");

    balance = newBalance;          
    assert(balance >= oldBalance);
  } // Custom error handling
  error InsufficientBalance(uint balance, uint withdrawAmount); function testCustomError(uint _withdrawAmount) public view {
     // address(this).balance is basically the contract balan
     uint bal = address(this).balance;

     // if you try to witdraw more than the contract balance it will throw an error.       
     if (bal < _withdrawAmount) {             
       revert InsufficientBalance({balance: bal, withdrawAmount:   _withdrawAmount});         
     }     
  }
}
```

**坚固性继承**

您应该将可靠性契约视为 Javascript 类

```
// A Soidity contract
contract Test {
  // Variables
  address private manager; // constructor funtion
  constructor() {
    manager = msg.sender;
  } // contract functions
  function getManager() external view returns(address) {
    return manager;
  }
}// Javascript class
class Test { 
  // constructor function
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }

  // class methods
  function getWidth() {
    return this.width;
  }
}
```

要继承 Solidity 中的一个合同，您必须在将继承它的合同中导入该合同，然后使用 **(is)** 关键字来继承该合同或接口

```
// IERC721Storage.sol
interface IERC721Storage {
  *function* name() *external* *view* returns (*string* *memory* *_name*);
  *function* symbol() *external* *view* returns (*string* *memory* *_symbol*);
}// ERC721Storage.sol 
import './IERC721.sol';contract ERC721Storage is IERC721 {
   *string* *private* _name;
   *string* *private* _symbol; *constructor*(*string* *memory* *named*, *string* *memory* *symbolified*) {
     _name = named;
     _symbol = symbolified;
   } *function* name() *external*  *view* returns(*string* *memory*) {
     return _name;
   }

   *function* symbol() *external*  *view* returns(*string* *memory*) {
     return _symbol;
   }
}// you can also inherit a class or an abstract class
```

读到这里，你一定同意我的观点，Solidity 和 Javascript 代码是相似的，所以作为一名对区块链及其工作原理有相当理解的 Javascript 开发人员，学习 Solidity 编程应该没什么大不了的。

> 这只是对 Solidity 的一个基本介绍，你应该多读一些关于 Solidity 及其开发工具的书，比如 [**【松露】**](https://trufflesuite.com/)**[**solcjs**](https://www.npmjs.com/package/solc)**[**web3js**](https://www.npmjs.com/package/web3)**[**meta mask**](https://metamask.io/)**[**hard hat**](https://hardhat.org/)********

> ****加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资****

## ****另外，阅读****

*   ****[3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://blog.coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)****
*   ****[莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)****
*   ****[Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://blog.coincodecap.com/bityard-reivew)****
*   ****[3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)****
*   ****最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)****
*   ****[BlockFi vs 摄氏](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630) | [Hodlnaut 点评](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 点评](https://blog.coincodecap.com/kucoin-review)****
*   ****[Bitsgap 审查](/coinmonks/bitsgap-review-a-crypto-trading-bot-that-makes-easy-money-a5d88a336df2) | [Quadency 审查](/coinmonks/quadency-review-a-crypto-trading-automation-platform-3068eaa374e1) | [Bitbns 审查](/coinmonks/bitbns-review-38256a07e161)****
*   ****[密码本交易平台](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c) | [Coinmama 审核](/coinmonks/coinmama-review-ace5641bde6e)****
*   ****[印度的加密交易所](/coinmonks/bitcoin-exchange-in-india-7f1fe79715c9) | [比特币储蓄账户](/coinmonks/bitcoin-savings-account-e65b13f92451)****
*   ****[OKEx vs KuCoin](https://blog.coincodecap.com/okex-kucoin) | [摄氏替代品](https://blog.coincodecap.com/celsius-alternatives) | [如何购买 VeChain](https://blog.coincodecap.com/buy-vechain)****
*   ****[币安期货交易](https://blog.coincodecap.com/binance-futures-trading)|[3 commas vs Mudrex vs eToro](https://blog.coincodecap.com/mudrex-3commas-etoro)****
*   ****[如何购买 Monero](https://blog.coincodecap.com/buy-monero) | [IDEX 评论](https://blog.coincodecap.com/idex-review) | [BitKan 交易机器人](https://blog.coincodecap.com/bitkan-trading-bot)****
*   ****[CoinDCX 评论](/coinmonks/coindcx-review-8444db3621a2) | [加密保证金交易交易所](https://blog.coincodecap.com/crypto-margin-trading-exchanges)****
*   ****[Bookmap 点评](https://blog.coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://blog.coincodecap.com/crypto-exchange-usa)****
*   ****[如何在 FTX 交易所交易期货](https://blog.coincodecap.com/ftx-futures-trading) | [OKEx vs 币安](https://blog.coincodecap.com/okex-vs-binance)****
*   ****[CoinLoan 评论](https://blog.coincodecap.com/coinloan-review) | [YouHodler 评论](/coinmonks/youhodler-4-easy-ways-to-make-money-98969b9689f2) | [BlockFi 评论](https://blog.coincodecap.com/blockfi-review)****
*   ****[XT.COM 评论](https://blog.coincodecap.com/profittradingapp-for-binance)币安评论 |****
*   ****[SmithBot 评论](https://blog.coincodecap.com/smithbot-review) | [4 款最佳免费开源交易机器人](https://blog.coincodecap.com/free-open-source-trading-bots)****
*   ****[比特币基地僵尸程序](/coinmonks/coinbase-bots-ac6359e897f3) | [AscendEX 审查](/coinmonks/ascendex-review-53e829cf75fa) | [OKEx 交易僵尸程序](/coinmonks/okex-trading-bots-234920f61e60)****
*   ****[如何在印度购买比特币？](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) | [瓦济克斯评论](/coinmonks/wazirx-review-5c811b074f5b)****
*   ****[隐料斗替代品](/coinmonks/cryptohopper-alternatives-d67287b16d27) | [HitBTC 审查](/coinmonks/hitbtc-review-c5143c5d53c2)****
*   ****[折叠 App 审核](https://blog.coincodecap.com/fold-app-review) | [Kucoin 交易机器人](/coinmonks/kucoin-trading-bot-automate-your-trades-8cf0ca2138e0) | [Probit 审核](https://blog.coincodecap.com/probit-review)****
*   ****[如何匿名购买比特币](https://blog.coincodecap.com/buy-bitcoin-anonymously) | [比特币现金钱包](https://blog.coincodecap.com/bitcoin-cash-wallets)****
*   ****[币安 vs FTX](https://blog.coincodecap.com/binance-vs-ftx) | [最佳(SOL)索拉纳钱包](https://blog.coincodecap.com/solana-wallets)****
*   ****[比诺莫评论](https://blog.coincodecap.com/binomo-review) | [斯多葛派 vs 3Commas vs TradeSanta](https://blog.coincodecap.com/stoic-vs-3commas-vs-tradesanta)****
*   ****[Capital.com 评论](https://blog.coincodecap.com/capital-com-review) | [香港的加密借贷平台](https://blog.coincodecap.com/crypto-lending-hong-kong)****
*   ****[如何在 Uniswap 上交换加密？](https://blog.coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 审查](https://blog.coincodecap.com/a-ads-review)****
*   ****[WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)****