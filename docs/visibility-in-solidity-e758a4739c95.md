# 固体中的可见性

> 原文：<https://medium.com/coinmonks/visibility-in-solidity-e758a4739c95?source=collection_archive---------2----------------------->

![](img/cff874a2eb8f1553bf88afebd6154a9c.png)

在 Solidity 中，您可以控制谁可以访问合同中的函数和状态变量，以及它们如何与它们交互。这个概念被称为可见性。

函数的可见性可以设置为`external`、`public`、`internal`或`private`，而状态变量只有三种可能的可见性修饰符；`public`、`internal`或`private`。关键字`external`不适用于状态变量。

**外部**

外部函数只能从声明它们的契约外部调用。

**公开**

契约内外的各方都可以访问公共函数和变量。当没有指定可见性时，函数的默认可见性是`public`。

**内部**

用`internal`关键字声明的函数和变量只能在声明它们的契约中访问，尽管它们可以从派生的契约中访问。当不指定可见性时，状态变量具有默认值`internal`。

**私人**

用`private`关键字声明的函数只能在声明它们的契约中访问。私有函数也是唯一不能被其他函数继承的函数。

***注意* :** 将函数或变量的可见性设置为`private`并不会使其在区块链上不可见。它只是限制它对契约中函数的访问。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)获取每日[加密新闻](http://coincodecap.com/)

## 另外，阅读

*   [复制交易](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c) | [加密税务软件](/coinmonks/crypto-tax-software-ed4b4810e338)
*   [网格交易](https://coincodecap.com/grid-trading) | [加密硬件钱包](/coinmonks/the-best-cryptocurrency-hardware-wallets-of-2020-e28b1c124069)
*   [密码电报信号](http://Top 4 Telegram Channels for Crypto Traders) | [密码交易机器人](/coinmonks/crypto-trading-bot-c2ffce8acb2a)
*   [最佳加密交易所](/coinmonks/crypto-exchange-dd2f9d6f3769) | [印度最佳加密交易所](/coinmonks/bitcoin-exchange-in-india-7f1fe79715c9)
*   [面向开发人员的最佳加密 API](/coinmonks/best-crypto-apis-for-developers-5efe3a597a9f)
*   最佳[密码借贷平台](/coinmonks/top-5-crypto-lending-platforms-in-2020-that-you-need-to-know-a1b675cec3fa)
*   杠杆代币的终极指南