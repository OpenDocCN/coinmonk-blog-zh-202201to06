# 拜占庭将军和现代分布式系统

> 原文：<https://medium.com/coinmonks/the-byzantine-generals-and-modern-distributed-systems-ba8fdc12d067?source=collection_archive---------15----------------------->

## 一个关于围城和现代分布式系统通信困难的感人故事

![](img/d505044739041842e06fbe1892c89fc0.png)

Photo by [Tim Schmidbauer](https://unsplash.com/@timschmidbauer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 历史题外话

君士坦丁堡在古典时代曾被称为拜占庭，它已经遭受了多次围攻(如此之多，以至于他们的名单在维基百科上有了自己的页面！).包围这座城市的将军们面临着决定是否进攻的问题。为了就是否进攻达成共识，将军们可以交换消息，而且必须处理好他们中间可能出现叛徒的问题。这种(虚构的)场景已被选为分布式系统(如区块链)可能存在的弱点的范例:区块链只有在就下一个要添加的块达成共识时才会演化其状态，并且必须在考虑故障节点、注入虚假消息的粗略节点和缓慢网络的情况下达成共识:这是一种拜占庭故障场景。

## 狂野互联网中的交流

“分布式系统”只是我们对组件部署的名称，在这种方式下，连接它们的通信信道(部分)在您的*管辖区*之外:这意味着:您无法依赖谁将传播您的消息，您可以假设有人可能会窃听它们，可能会发生一些恶意代理将坏消息注入您的流量中，等等

当然，这种通用场景适用于互联网上的任何*通信，所以这是工程师和计算机科学家多年来学会应对的事情。有趣的是，这种天生不可靠的交流方式正是上面例子中的将军们不得不应对的。*

在[1]中，作者将拜占庭将军和他们的通信问题作为分布式系统的范例，并提供一些方法让他们在现代互联网中合作和协调他们的努力。这是如此重要，以至于表达[拜占庭故障](https://en.wikipedia.org/wiki/Byzantine_fault)指的是分布式系统中由不完善的通信引起的故障。

## 区块链和将军们

设计分布式系统中最具破坏性的方法之一是区块链，其目的是通过分布式事务数据库来表示价值:这种方法必须考虑拜占庭故障以及在同步数据库副本的过程中如何依赖它们，同时允许每个节点(潜在地)添加更多事务，目的是达到**拜占庭容错** ( **BFT** )(参见？还是将军)。

可以使用不同的算法来实现 BFT，并且可以部署具有不同 BFT 算法的相同区块链。

研究它们的一个很好的起点可以是 Hyperledger 锯齿，它可以运行各种一致的算法，包括实用的拜占庭容错(PBFT)和运行时间证明(PoET)，让用户根据特定的要求以最合适的方式设计区块链的性能。

查看我在 Logrocket 博客上的这篇文章，了解更多关于不同算法和一些测试的深入讨论: [Hyperledger 锯齿波:一个温和的介绍](https://blog.logrocket.com/hyperledger-sawtooth-introduction/)

# 参考

1.  *莱斯利·兰波特，罗伯特·肖斯塔克和马歇尔·皮斯。1982.拜占庭将军的问题。ACM Trans 程序。郎。系统。4，3(1982 年 7 月)，382-401 页。DOI:https://DOI . org/10.1145/357172.357176*

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [有哪些交易信号？](https://coincodecap.com/trading-signal) | [Bitstamp vs 比特币基地](https://coincodecap.com/bitstamp-coinbase) | [买索拉纳](https://coincodecap.com/buy-solana)
*   [ProfitFarmers 点评](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix Trading Bot](https://coincodecap.com/cornix-trading-bot)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [my constant Review](https://coincodecap.com/myconstant-review)|[8 款最佳摇摆交易机器人](https://coincodecap.com/best-swing-trading-bots)
*   [MXC 交易所评论](/coinmonks/mxc-exchange-review-3af0ec1cba8c) | [Pionex vs 币安](https://coincodecap.com/pionex-vs-binance) | [Pionex 套利机器人](https://coincodecap.com/pionex-arbitrage-bot)