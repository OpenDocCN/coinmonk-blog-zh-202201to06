# 真正的初学者指南—以太坊(第一部分)

> 原文：<https://medium.com/coinmonks/a-truly-beginners-guide-ethereum-part-1-bf2e246d7ae8?source=collection_archive---------55----------------------->

## 窥视以太。

![](img/72b1ce907df2304cdba89649ebcf08d2.png)

Photo by [Solen Feyissa](https://unsplash.com/es/@solenfeyissa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我告诉您智能合约、令牌、NFT 和 stablecoins 几乎完全相同，会怎么样？你理解了一个，你就理解了所有人。不要再试图跟上本周区块链的新发明。从创新的角度来看，它们是独特的，服务于特定的目的，但从教育的角度来看，它们都是一样的。

在这个由 3 部分组成的系列中，我将解释什么是以太坊，什么是 T2 智能合约，以及如何快速理解明天出现的区块链新技术。

# 以太坊 vs 比特币

在我们解释这些新技术之前，我们必须先了解以太坊，以及它与比特币的不同之处。如果你想要更高层次的解释，我已经写了一个关于比特币的[系列](/@flapjackslappack/seriously-what-is-bitcoin-3a758aa4d3c9)。目前，我们可以将比特币总结为一个巨大的共享银行账户，个人拥有共享账户中特定交易的控制权。当比特币用户“收到比特币”时，他们只是交易中的接收者，并被授予交易下一步走向的唯一权力。交易中的比特币数量可能会有所不同。当你“发送比特币”时，你使用密钥从数学上证明你有权发送比特币，然后你授予其他人对该交易的唯一控制权。事务只是四处移动，与其他事务合并成更大的事务，或者分解成更小的事务。

归根结底，你的总体比特币投资组合就是你控制了多少交易，你“拥有”的比特币数量就是所有这些交易的总余额。如果到目前为止这还没有意义，回去看看我的比特币系列，我保证它很短，会有帮助。

![](img/83073765a185937e7c6ee2b9253a2c29.png)

Photo by [Kenny Eliason](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 交易与账户

你可能一直想知道为什么比特币不使用账户。银行用账户，脸书用账户，Medium 用账户，看起来很简单。与其用钱包(我在[这篇文章](/coinmonks/cryptocurrency-wallets-what-are-they-32ce0461eb66)中解释)来记录所有这些交易，不如有一个账户，当你发送或接收比特币时，你的账户余额分别下降或上升，这不是更简单吗？嗯……有些人决定让这成为现实，并称之为**以太坊**。

以太坊是一种类似比特币的区块链技术，但有一些主要区别。首先，它使用账户而不是汇总交易。你仍然有一个私钥/公钥对，但是当有人给你发送以太(以太坊加密货币)时，你不必跟踪那个交易。相反，你的账户余额会随着你收到的汇款而增加。如果你是发送以太网的人，你证明你可以像比特币一样使用密钥控制你的账户，如果矿工们都同意你有资金进行这笔交易，他们会从你的账户中扣除这笔钱，并将其添加到接收者的账户中。这本身是一个概念上的改进，但是以太坊带来了更大的功能上的改进。

![](img/003797c39fa04f2cd4144d7960688e86.png)

Photo by [Nenad Novaković](https://unsplash.com/es/@dvlden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 可编程区块链

让我们考虑一个场景，我们想开始用比特币支付孩子的每月零花钱。我们制作一个比特币密钥对，从交易所购买一堆比特币。我们不想一下子全给孩子，因为这是零用钱。相反，我们编写了一个非常基本的计算机程序，在每个月的第一天，它会代表我们向我们的孩子发送一笔小额比特币交易，作为他们的零用钱。在这一点上，这可能不是必要的，但如果这是比特币本身的一个特征，难道不是很方便吗？

在以太坊区块链中，除了余额，账户还可以附加一个程序。我们为比特币编写的这个津贴程序实际上可以上传到以太坊区块链(假设我们的孩子同意用以太代替比特币支付)。现在孩子可以拿到零花钱了，我们也不用担心停电或电脑死机了。每个月的第一天，您的孩子会收到他们的津贴，作为从您上传的程序到他们帐户的交易。如果程序开始耗尽乙醚发送，您可以购买更多并发送到此程序以补充乙醚。

这里有一个警告:一个人**或者**一个程序可以控制一个账户，**不能同时控制两者**。您将使用您的个人以太坊帐户，并创建一个附加了该程序的新帐户。但是一旦这样做了，程序帐户将永远按照程序运行，你不能再访问它或编辑它。

他们为什么要这样做？请记住，区块链技术被设计为在没有中央权威的情况下执行任务，而历史上需要一个中央权威。通过使我们的程序永久化，无论谁使用它们都不必担心它们会改变。如果他们的零花钱突然逐月变化，我们的孩子可能不会起诉我们，但我们的庭院设计师或房东可能会。由于程序是永久的，每个使用程序的人都可以相信它永远不会改变。

![](img/07fad586bf17ae1e609295b0b0a0041f.png)

Photo by [Cytonn Photography](https://unsplash.com/@cytonn_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们刚刚描述的是一个**智能合约:**一个由代码而不是人控制的账户。我们的例子是一个儿童津贴智能合同，但可能性是无限的。区块链技术本身，就像我们看到的比特币一样，可以轻松处理基本交易。但所有这些与加密货币相关的新技术都只是人们想出来的新程序，并随后附加到以太坊账户上。什么是 NFT？一份精明的合同。什么是 Stablecoins？一份精明的合同。什么是代币？一份精明的合同。

老实说，比特币确实有能力做一些比简单交易更复杂的事情，但仅仅是勉强。以太坊真的接受了这个想法，并付诸实践。和生活中的大多数事情一样，你做的东西越复杂，出现问题的可能性就越大。以太坊也不例外，在下一部分我会解释这些问题，以及以太坊如何避免这些问题。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Capital.com 评论](https://coincodecap.com/capital-com-review) | [香港的加密借贷平台](https://coincodecap.com/crypto-lending-hong-kong)
*   [如何在 Uniswap 上交换加密？](https://coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 审查](https://coincodecap.com/a-ads-review)
*   [WazirX vs CoinDCX vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [本地比特币评论](/coinmonks/localbitcoins-review-6cc001c6ed56) | [加密货币储蓄账户](https://coincodecap.com/cryptocurrency-savings-accounts)
*   什么是融资融券交易