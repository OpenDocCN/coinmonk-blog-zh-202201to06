# 固体中的函数状态可变性

> 原文：<https://medium.com/coinmonks/function-state-mutability-in-solidity-acb850eedccc?source=collection_archive---------3----------------------->

![](img/72cd41beb9275ffffc376fa52d7a0b14.png)

Photo by [Meagan Carsience](https://unsplash.com/@mcarsience_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

状态可变性是可靠性中的一个概念，它定义了函数的行为以及它们如何与存储在区块链上的数据进行交互。在本文中，您将了解不同的状态可变性修饰符，以及如何在编写优化的智能契约时应用它们。

solidity 中两个主要的状态可变性修改器是:

*   视角
*   纯的

**查看功能**

视图函数是只读函数，用关键字`***view***`声明。它们不会改变区块链的状态。这意味着用`***view***`关键字声明的函数不能包含可能修改状态变量或存储在区块链上的数据的代码。

另外，`***view***`函数不能接收或发送以太，只能调用其他`**view**`或`***pure***`函数。有可能修改区块链状态的`***view***`函数将抛出一个错误，并且无法编译。同样，当编译器检测到一个只读取而不写入区块链的函数时，它会建议您将该函数的状态可变性设置为`***view***`。

下面的 ***合同 A*** 中的例子演示了 ***视图结果*** 函数如何从状态中读取数据( ***num1*** 和 ***num2*** )但不修改数据。

```
pragma solidity 0.8.10;contract A { // Declaring state variables uint num1 = 5; uint num2 = 10; // View function to calculate product of 2 numbers function viewResult() public view returns(uint product){ // Expression that reads state product = num1 * num2;
  }}
```

输出:

```
product = 50
```

**纯函数？**

将函数声明为`***pure***`会限制该函数改变存储在区块链上的数据或与之交互。标记为`***pure***`的函数既不读取也不写入区块链。它们不能接收或发送以太，不能使用`***msg***`的成员或`***block***`的成员，只能调用其他`***pure***`函数。

如果您的契约包含不读取或修改状态的函数，编译器将发出警告，并建议您指定状态可变性。可以忽略此警告，代码仍然可以编译。但是，最好总是将其设置为`***pure***` ***。***

下面的 ***合同 B*** 中的例子演示了 ***addNum*** 函数既不从状态读取数据也不向状态写入数据。

```
pragma solidity 0.8.10;contract B { // Pure function that calculates sum of 2 numbers function addNum(uint num1, uint num2) public pure
  returns(uint sum){ // Expression that computes data passed in as parameters
  // and does not read or modify state sum = num1 + num2; }}
```

输出:

```
sum = 15
```

**为什么要将函数标记为视图或纯函数？**

***Gas 优化:*** Gas consumption 仅适用于触发交易时，以及修改状态时触发交易。标记为`***view***`或`***pure***`的函数不修改状态，因此不消耗 gas，除非从外部契约调用它们。

**其他函数状态可变性修饰符**

除了`***view***`和`***pure***`，功能状态可变性还可以是`***payable***`或**不可支付。**

**应付功能**

用`***payable***`关键字声明一个函数允许函数发送和接收以太。试图通过未标记为`***payable***`的函数发送或接收以太网将导致交易被拒绝。

因此，如果您的智能合约需要通过某个函数发送或接收以太，则必须将该函数标记为`***payable***`。

下面的 ***存款*** 功能允许其他合约向 ***合约 C*** 发送乙醚。

```
pragma solidity 0.8.10;contract C {
  uint balance = 0;// *Payable function that allows other contracts*
// *to send ether to this contract*. function deposit () payable public{
    balance += msg.value;
  } }
```

**非付费功能**

***非应付*** 在当前 solidity 版本中不是关键字，而是在函数没有被显式定义为`***payable***`时默认的状态可变性修饰符。 ***不可支付*** 未明确定义为`***view***`或`***pure***`的函数最适合于可能读取和修改状态变量的函数。 ***非付费*** 功能的主要限制是它们不能接收或发送以太网。

```
pragma solidity 0.8.10;contract D { uint count = 0;// *non-payable function that reads and modifies state*.function increment() public returns(uint){
    count += 1;
    return count;  
}}
```

上面 ***合同 D*** 中的 ***增量*** 函数演示了 ***非应付*** 函数如何通过访问声明的 ***计数*** 变量从 state 中读取数据。它还说明了该函数如何潜在地通过在每次调用函数*增量时将 ***计数*** 的值加 1 来修改状态。*

****如果你觉得这很有帮助，请关注、分享并展示一些❤️👏。****

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[创造并出售你的第一个 NFT](https://coincodecap.com/create-nft) | [密码交易机器人](https://coincodecap.com/best-crypto-trading-bots)*
*   *[如何在 CoinDCX 上购买柴犬(SHIB)币？](https://coincodecap.com/buy-shiba-coindcx)*
*   *[CBET 评论](https://coincodecap.com/cbet-casino-review) | [库科恩 vs 比特币基地](https://coincodecap.com/kucoin-vs-coinbase) | [拜比特 vs 比特币基地](https://coincodecap.com/bybit-vs-coinbase)*
*   *[折叠 App 回顾](https://coincodecap.com/fold-app-review) | [本地比特币回顾](/coinmonks/localbitcoins-review-6cc001c6ed56) | [Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt)*
*   *[加密保证金交易交易所](/coinmonks/crypto-margin-trading-exchanges-428b1f7ad108) | [赚取比特币](/coinmonks/earn-bitcoin-6e8bd3c592d9) | [Mudrex 投资](https://coincodecap.com/mudrex-invest-review-the-best-way-to-invest-in-crypto)*
*   *[WazirX vs CoinDCX vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)*
*   *[比斯勒评论](https://coincodecap.com/bitsler-review)|[WazirX vs coin switch vs coin dcx](https://coincodecap.com/wazirx-vs-coinswitch-vs-coindcx)*
*   *[7 大副本交易平台](https://coincodecap.com/copy-trading-platforms) | [BuyCoins 点评](https://coincodecap.com/buycoins-review)*
*   *[XT.COM 评论](https://coincodecap.com/profittradingapp-for-binance)币安评论 |*