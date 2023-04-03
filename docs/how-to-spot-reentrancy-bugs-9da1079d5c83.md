# 如何发现可重入性错误

> 原文：<https://medium.com/coinmonks/how-to-spot-reentrancy-bugs-9da1079d5c83?source=collection_archive---------17----------------------->

可重入可能是 solidity 智能契约中最常见和最著名的利用。

![](img/f464e7c7c2474f2068bb166a07e3229c.png)

Photo by [FLY:D](https://unsplash.com/@flyd2069?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cyber-attack?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

首先，如果您不熟悉这个漏洞，让我解释一下在这个代码示例中可重入攻击是如何发生的。

> 调用外部契约的主要危险之一是它们可以接管控制流。在重入攻击(也称为递归调用攻击)中，恶意契约在函数的第一次调用完成之前回调调用契约。这可能导致函数的不同调用以不期望的方式交互。

*<*[*【https://swcregistry.io/docs/SWC-107】*](https://swcregistry.io/docs/SWC-107)*>*

已经有很多关于可重入性的教程和文章，但是大多数都非常简单，只展示了一个特定的例子或者它的变体。

如果你看这段代码，你可以看到，如果有人在那里有一个余额，它读取余额并发送它。但是接收以太转发的过程将允许攻击者两次或更多次重新进入该功能并收回他们的余额。

对我来说，像这样的例子限制了可重入的范围。大多数人认为这是一个问题，当你发送以太。

长期以来的最佳实践是，停止发送乙醚使用*调用*函数，因为你转发你所有的气体，开始使用 *transfer()、send()* 函数。

自 2019 年 12 月起，随着天然气成本的降低，*调用*功能再次成为最佳选择。

**但是可重入性呢？**

消除可重入性错误的最简单的方法是使用 ***检查-效果-交互模式。*** 还记得我们上面的代码有一个可重入的 bug 吗？现在让我们用这个模式来修复它。

注意，现在余额在转移之前被修改了**，所以试图重入这个函数没有任何好处。**

在这种情况下，防止这种攻击的另一种方法是使用**重入防护。** *(Openzeppelin 对此有一个气体高效的实现，值得一查)。*

可重入性现在成为一个更重要的主题，因为如果越来越多的人开始再次采用 *call* 函数，这些攻击可能会变得更有可能。

现在，让我们回到本文的目的，如何在比我上面展示的代码更优雅、更复杂的代码中发现和防范重入攻击。

我们应该注意代码中的三个标志:

*   **在**之前:控制流程
*   **在**之前:创建并在之后使用的内存变量
*   **在**之后:存储写入

为了帮助您理解这些迹象，让我们使用一个著名的可重入性 bug 的例子，DAO hack。

第 6 行实际上是以太发送。

让我们看看在这段代码中可以发现哪些迹象。

1.  在第 3 行，我们有一个基于存储值的控制流**。**
2.  在第 5 行，我们在第 8 行的之前创建了一个变量**，并在之后使用。**
3.  在第 8 行，我们在存储写之后有一个

**如您所见，在这段代码中，我们可以发现可重入性错误的所有三个迹象。**

****Uniswap & ERC777****

**另一个非常著名的例子是 Uniswap & ERC777。**

**基本上，如果您将 ERC777 令牌放在 Uniswap 上，它们可以通过重入攻击被窃取。**

**让我们看看代码。**

**这个问题非常有趣，因为它没有显示出您之前提到的三个迹象中的任何一个，但是可重入性错误的真正原因是什么呢？**

*****剧透*** ，漏洞来自第 9 行。**

**如果你不知道 ERC777，没关系，对于这个例子你只需要知道这个契约的一个特性，**钩子**。**

**在任何 ERC777 传输中，都是这样的:**

1.  **打电话给代币的发送者**
2.  **执行转移**
3.  **打电话给代币的接收者**

**所以，由于 ERC777 钩子是在 实际传输之前 ***执行的，所以发送方被调用并可以执行代码。*****

**在 Uniswap 的例子中，当发送者被呼叫时，我们有这样的情况:**

*   **ETH 储备已经减少了。**
*   **令牌储备尚未增加。**
*   **发送方契约可以决定现在做什么。**

**当发送方契约被调用时，它可以通过再次调用 **tokenToEthOutput** 函数来重新进入 Uniswap 契约。**

**在第二次调用中，ETH 预留将会更低，但是令牌预留将会相同，并且使用 Uniswap 的公式来确定价格，ETH 价格将会更便宜。**

**攻击者可以重新进入契约，次数与以太网储备持续的次数一样多，或者直到你的令牌供应用完。**

****结论****

**这是对如何在更优雅和复杂的代码中发现可重入性错误的快速解释。**

**我希望每个人都喜欢。**

> **加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资**

# **另外，阅读**

*   **[如何在 FTX 交易所交易期货](https://coincodecap.com/ftx-futures-trading) | [OKEx vs 币安](https://coincodecap.com/okex-vs-binance)**
*   **[OKEx vs KuCoin](https://coincodecap.com/okex-kucoin) | [摄氏替代度](https://coincodecap.com/celsius-alternatives) | [如何购买 VeChain](https://coincodecap.com/buy-vechain)**
*   **[ProfitFarmers 回顾](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix 交易机器人](https://coincodecap.com/cornix-trading-bot)**
*   **[如何匿名购买比特币](https://coincodecap.com/buy-bitcoin-anonymously) | [比特币现金钱包](https://coincodecap.com/bitcoin-cash-wallets)**
*   **[瓦济里克斯 NFT 评论](https://coincodecap.com/wazirx-nft-review)|[Bitsgap vs Pionex](https://coincodecap.com/bitsgap-vs-pionex)|[Tangem 评论](https://coincodecap.com/tangem-wallet-review)**