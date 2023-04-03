# 区块链实际上是如何工作的？

> 原文：<https://medium.com/coinmonks/how-blockchain-actually-works-c2326a8462c6?source=collection_archive---------35----------------------->

这只是我们试图解决术语区块链的另一个日常故事。介绍性概念很容易随着一些技术概念的出现而萌芽。
所以，首要问题是区块链是如何工作的？幕后到底发生了什么？

## 有哪些区块？

为了理解区块链的工作原理，让我们先来理解术语区块链中的“区块”是什么。因此，块是散布在网络各处并与互联网连接(链接)在一起的大量信息。每个块负责存储已被记录和多次追踪的一组确定的数据。每个物理系统(计算机)都扮演着节点的角色，它们充当正在进行的事务抓取的见证。
现在的问题是，区块链实际上是如何执行其任务的？
现在让我们接触一下技术方面(嗯，一点也不专业)。
通常，区块链遵循‘共识’特征。每当数据写入中发生任何变化时，所有可用的块都表示同意或不同意，以便以多数继续进行。这和民主是一样的，因此有一点是肯定的，我们至少需要 3 个街区来确认公平的共识过程的发生。
共识机制的一些规则-
-没有节点比其他节点更有权威，
-当超过一半的节点同意时，共识就达成了

## 哈希法-

理解了共识之后，让我们来理解哈希 algo。
因此，我们知道，每当数据发生变化时，特定数据块的地址也会发生变化，因此其先前的链接会断开，从而破坏整个序列。因此，为了保护区块链最必要的特性——数据的安全性，这种机制非常重要。
已经发现，块的地址可以很容易地被追踪出来，因此需要保护第一道防线——块链中的“块地址”。仅仅为了这个，我们需要一些散列机制。它所做的是将散列数据与块数据相加，使其成为不可侵入的块地址。
这个过程叫做挖掘。挖掘者找出适当的散列，该散列可以与出现的数据进行映射，以释放一组确定的地址。
SHA-256 是最常用的哈希算法之一。它包含 64 个字符。

*好的哈希算法的某些特征是-*
-一种数学函数方式，
-计算速度快，
-几乎不可能逆转，
-产生很少的冲突，
-将 i/p 映射到 o/p

## 采矿-

最好的挖掘者是这样一个人，他提出了重要的散列，实现了在给定的时间内尽早用块数据生成所需类型的地址的承诺。这样的矿工在密码中得到奖励。在这里，我们遇到了加密货币的概念。
现在，同样清楚的是，区块链和加密货币不是同一个名词。相反，两者是相互依赖的。没有加密货币，区块链就无法存在；没有区块链，加密货币就没有价值。

在我们的下一篇博客文章中，我们将谈论加密货币。谢谢你的时间，在那之前继续链接块！！

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 commas vs . Pionex vs . Cryptohopper](https://coincodecap.com/3commas-vs-pionex-vs-cryptohopper)|[Bingbon Review](https://coincodecap.com/bingbon-review)
*   [加密复制交易平台](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c) | [如何在 WazirX 上购买比特币](/coinmonks/buy-bitcoin-on-wazirx-2d12b7989af1)
*   [货币评论](https://coincodecap.com/coinloan-review)|[Crypto.com 评论](/coinmonks/crypto-com-review-f143dca1f74c)
*   [如何在加拿大购买加密货币？](https://coincodecap.com/how-to-buy-cryptocurrency-in-canada)
*   [无聊猿游艇俱乐部(BAYC)评论](https://coincodecap.com/bored-ape-yacht-club-bayc-review)