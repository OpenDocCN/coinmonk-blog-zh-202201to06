# 加密货币和区块链。那是什么？

> 原文：<https://medium.com/coinmonks/cryptocurrencies-and-blockchain-whats-that-de7e23f840a7?source=collection_archive---------50----------------------->

![](img/9a90c923ac976f8f7aba4c90c385214b.png)

Photo by [André François McKenzie](https://unsplash.com/@silverhousehd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每个人都在谈论加密，或者至少听到有人在谈论它。关于密码是什么，有一片迷雾，关于密码在社会中当前和未来的效用，有如此多的困惑和矛盾的观点。有人说所有的密码世界都是骗局，但另一方面，有人说密码是我们现在生活的最有前途的技术革命。

让我们对 crypto 做一个非常简单的介绍，但是在进入这个之前，让我们先来谈谈让一切成为可能的技术:**区块链**。

区块链，用最简单的解释来说，就是一本账簿。也就是说，双方之间发生的所有交易都被登记、存储。分类账记录了我们拥有的资产以及我们与它们进行的所有交易。人类一直使用分类账来处理与价值交换相关的一切事情，没有它们，所有的日常交易都是不可能的。

银行有自己的分类账来记录客户的所有交易，从 ATM 机的简单取款到网上商店的信用卡购买。那么，如果区块链是一本账簿，我们还需要区块链吗？我们已经有账本了。银行有自己的分类账来记录我们的资金支出和收入。要回答这个问题，我们先来谈谈**信托。**

# 我们(不)信任银行

当我们用信用卡买东西或使用 Bizum 支付债务时，我们就产生了新的交易。在每笔交易中，至少有两方:发送方和接收方。汇款人汇钱，收款人收到钱，但如果没有第三方保证交易可行(检查汇款人的账户中有足够的钱)并执行双方之间的交易(更新汇款人和收款人账户中的最终余额)，这是不可能的。所以在我们现在生活的世界里，我们需要信任第三方，我们需要中央集权，我们需要银行。

但是，如果我们不必信任银行呢？我们能建立一个银行无法控制交易的系统吗？我们能建立一个**不可信的**系统吗？这就是区块链解决的问题，它不是银行所有的总账，而是一个**分散的总账**。

区块链是一个分布式系统，其中所有参与者相互连接形成一个网络(通常通过互联网),并拥有整个分类账的副本。也就是说，每个人都可以访问系统中发生的所有事务。这似乎有点侵犯人们的隐私，但现实是，这并不是因为我们与网络的所有交互都由一个**钱包**(形式上是一系列字母数字)来表示，这个钱包与我们的个人数据无关(除非你有意分享)。这背后的想法是，每个人都知道每个人在任何给定时刻的账户状态，所以没有人可以在不注意到网络中其他参与者的情况下改变他们的余额。

从技术上来说，区块链是由一系列块组成的**，其中记录了从一开始系统中发生的所有事务。每次启动事务时，都会对其进行验证以检查其正确性，如果是肯定的，则将其附加到区块链。验证交易的过程包括**验证器**的参与，验证器是一组连接到网络的节点，它检查每一笔交易，并将交易中涉及的数量更新到区块链。由于一致的算法，节点之间的所有编排和通信都是可能的(参见[工作证明](https://www.wikiwand.com/en/Proof_of_work)和[利益证明](https://www.wikiwand.com/en/Proof_of_stake))。**

需要注意的是，一旦块被添加到区块链，它就保持不变，也就是说，它不能被怀有恶意的第三方事后更改(参见 [**双重花费问题**](https://en.wikipedia.org/wiki/Double-spending?oldformat=true) )。从某种意义上来说，这是可能的，这要归功于密码术，如果网络中的某个人改变了一个块的一个最小部分，则连接到被改变部分的所有块序列也将被改变，产生两个不一致的分类帐版本，并且证明了网络中的某个人对其余节点的不良意图。如果发生这种情况，支持较少的版本将被丢弃，而另一个版本将被保留。

从某种意义上说，区块链是不可信任的，我们不必信任像银行这样的第三方，即一个集中的实体，但现实是我们必须信任网络及其节点的独立性，以符合一个真正的分散系统。

# 第一个区块链，比特币

第一个区块链是中本聪在其[论文](https://bitcoin.org/bitcoin.pdf)中提出的**比特币区块链**。比特币区块链于 2009 年正式发布，第一笔交易于 1 月 12 日完成。因此，到目前为止，我们已经谈论了区块链和不需要可信任的第三方就能进行交易的能力，但是在区块链中我们能交易什么呢？这就引出了加密货币的定义。

一种**加密货币**是一种数字资产，由一系列字母数字字符(通常是一个令牌)表示，这些字符只在其对应的区块链中有值。**比特币**(或 BTC)是比特币区块链的本地令牌，其中 10 个是 2009 年 1 月 12 日在第一次加密交易中通过比特币网络发送的。当时，1 BTC 一文不值，但在撰写本文时，1 BTC 的价格已经达到了 6 万美元。

从那时到现在，发生了很多事情，在 Satoshi 的头脑中，一件疯狂的事情开始出现，现在是一种新兴的技术开始迫使**政府**采取立场，不管有没有**无银行**运动。

生态系统中不断涌现出许多新的区块链，市场上每天都有新的加密货币出现。在撰写本文时，加密生态系统的总市值超过 1.5 万亿美元，这证明了“加密的东西”不是最疯狂的头脑中转瞬即逝的概念，而是一个持续存在的现实。

# 但是等等…我们能更进一步吗？

区块链不仅仅是一个大型分布式账本，还是一个大型分布式计算机。在接下来的章节中，让我们深入了解**智能合约、以太坊、DeFi、stablecoins 的概念，以及加密的未来**。

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs Ngrave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)
*   [BlockFi vs 摄氏](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630) | [Hodlnaut 点评](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 点评](https://coincodecap.com/kucoin-review)
*   [Bitsgap 审查](/coinmonks/bitsgap-review-a-crypto-trading-bot-that-makes-easy-money-a5d88a336df2) | [Quadency 审查](/coinmonks/quadency-review-a-crypto-trading-automation-platform-3068eaa374e1) | [Bitbns 审查](/coinmonks/bitbns-review-38256a07e161)
*   [密码本交易平台](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c) | [Coinmama 审核](/coinmonks/coinmama-review-ace5641bde6e)