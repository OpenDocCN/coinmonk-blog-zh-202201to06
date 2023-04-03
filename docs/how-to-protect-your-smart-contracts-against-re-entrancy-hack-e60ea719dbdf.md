# 如何保护你的智能合同免受黑客入侵！

> 原文：<https://medium.com/coinmonks/how-to-protect-your-smart-contracts-against-re-entrancy-hack-e60ea719dbdf?source=collection_archive---------26----------------------->

![](img/a79d0666212a03e14cd7d3c0683933ca.png)

内容

*   什么是再入攻击？
*   黑客如何能够执行再入攻击？
*   他们为什么能做到这一点？
*   如何防止重入攻击？

**什么是再入攻击？**

重入，顾名思义，意味着重复地重新进入或重新调用函数，在 Defi 的情况下，我们可以说重入攻击重复地调用智能契约中的函数，以耗尽目标契约或钱包中的资金。

**假设情景**

想象一下，一名黑客假扮成银行客户，将资金存入银行的流动性池——无意中存入了自己的账户。这位黑客随后继续提取他的存款，但让我们盲目地假设银行的后端代码有一个错误，无法在提取时更新客户的帐户。也就是说，在执行转移函数之前，他们不能更新他们的余额。银行方面的这一错误将允许我们假设的黑客返回并一次又一次地调用函数“取款”，直到他们处于耗尽银行流动性池的边缘。

请注意，这是假设，可能永远不会发生在现实世界中，但我非常希望你抓住重入攻击是如何工作的。

一次又一次地返回调用该函数“撤回”的过程就是这种攻击得名“重入”的原因。

同样的逻辑也适用于智能契约中的可重入攻击。攻击者契约基本上是重复调用目标契约的一个函数，目的是耗尽资金。

**黑客是如何做到这一点的？**

攻击者编写一个契约，通过首先伪装成用户或存款人来与目标契约进行交互，这意味着他们的契约将具有调用另一个契约中的“撤回”的函数、一个回退函数以及一个可以命名为“排出”、“攻击”等的函数，而另一个函数所做的正是它所命名的。它不断地从目标账户中提取资金。

**他们为什么能够做到这一点？**

有效的问题。攻击者之所以能够做到这一点，可能是由于目标契约方面的两个原因或错误。首先，目标契约有一个修改器，在转移资金到野外之前更新你的契约状态。简单地说，在释放资金之前，首先更新你的余额。我不知道你是否注意到了这一点，但传统银行往往会在交易成功之前就快速借记你的账户，如果交易失败，他们会将你的钱退回。借方提醒是他们先主动更新他们的余额，然后你才能决定重新进入取款功能。

这也是你应该对你的智能合同做的，总是在执行前首先更新余额。

上述函数直到执行结束时才更新余额。这使得合同容易受到重入攻击。

**在上面的代码中如何防止重入**

这个函数在执行结束前更新契约的状态，这是防止重入攻击的简单方法。

你的智能合约可能受到损害的另一个原因是，当你使用像**调用这样的低级方法时。值**。如果你熟悉在智能合约中发送以太网，你会知道有三种发送以太网的方式；通过使用‘呼。“值”、“传输”和“发送”。最好和最安全的方法是使用“转移”。这是因为 transfer 和 sends 方法不同于 call。“value”使用标准的 gas 级别— 2300，并在交易失败时抛出异常，但 **call.value** 允许无限量的 gas，这就是为什么接收器可以不断操纵和触发其回退功能来接收以太网。

注意，这三个函数被标记为 sendEther。这仅仅是假设。还要注意，三个函数中的函数体是不同的。第一种使用**发送**的方法，第二种使用**调用。值**，而第三个发送器函数使用**传输**。作为防止重入攻击的最佳实践，请始终使用 transfer 方法。

总之，为了防止智能契约中的重入，我们强调了两个简单的方法，一个是在执行之前总是更新契约的状态，另一个是避免使用 call 之类的低级调用。价值。

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [有哪些交易信号？](https://coincodecap.com/trading-signal) | [Bitstamp vs 比特币基地](https://coincodecap.com/bitstamp-coinbase) | [买索拉纳](https://coincodecap.com/buy-solana)
*   [ProfitFarmers 回顾](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix Trading Bot](https://coincodecap.com/cornix-trading-bot)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [MyConstant 点评](https://coincodecap.com/myconstant-review) | [8 款最佳摇摆交易机器人](https://coincodecap.com/best-swing-trading-bots)
*   [MXC 交易所评论](/coinmonks/mxc-exchange-review-3af0ec1cba8c) | [Pionex vs 币安](https://coincodecap.com/pionex-vs-binance) | [Pionex 套利机器人](https://coincodecap.com/pionex-arbitrage-bot)