# DLT 互操作性和更多⛓️#3 ⛓️ —最大提取价值

> 原文：<https://medium.com/coinmonks/dlt-interoperability-and-more-%EF%B8%8F-3-%EF%B8%8F-maximal-extractable-value-42aa380ea56c?source=collection_archive---------16----------------------->

# 在这个系列中，我们分析了关于区块链和互操作性(以及两者)的论文。

本版涵盖了 2021 年 12 月关于跨域 MEV 的一篇论文

![](img/766bfaf1da118b880ec8fc267a9abf1c.png)

Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

➡️ **书名**:团结就是力量:跨领域最大可提取价值的形式化
➡️ **作者**:亚历山大·奥巴迪亚、阿莱霍·萨勒斯、拉克什曼·桑卡尔、塔伦·奇特拉、瓦伊巴夫·切拉尼和菲利普·黛安

➡️ **投稿:**

*   作者在几个区块链的范围内定义了最大可提取值
*   作者非正式地定义了领域概念。

💪**优点:**

*   重要问题:MEV 开始在跨区块链的环境中被开发，在那里开采意味着在区块链移动资产。
*   图 2:描绘了一个跨两个异质区块链的跨链套利机会，通过进行两个交易:在以太坊区块链上用 MATIC 交换 WETH(将以太坊上的 wet 桥接到多边形上的 wet)，并将 wet 换成多边形上的 WMATIC。这就是我们所说的[由两个本地事务](https://www.techrxiv.org/articles/preprint/A_Framework_to_Evaluate_Blockchain_Interoperability_Solutions/17093039)组成的跨链事务。
*   图 3:描绘了一个跨三个异质区块链的跨链套利机会，通过进行四个交易:在以太坊区块链用 MATIC 交换 WETH 在以太坊区块链与 USDC 交换天气；(将 USDC 与币安智能链连接起来)；将币安智能链上的 USDC 交换为 ETH，(将 ETH 桥接至 WETH)，并将 WETH 交换为多边形上的 WMATIC。这就是我们所说的[由三个本地事务](https://www.techrxiv.org/articles/preprint/A_Framework_to_Evaluate_Blockchain_Interoperability_Solutions/17093039)组成的跨链事务。

**😞局限性:**

*   作为一篇介绍性论文，没有任何限制可言

**🔥兴趣点:**

*   MEV，但是增加了一些复杂性。首先，事务排序发生在多个协议中，这意味着 MEV 操作者需要拥有不同协议中的节点。第二，我们交易者开始和结束的资产不一定相同。第三，由于桥接操作不是原子的，我们的跨链事务[需要额外的机制来确保操作](https://www.sciencedirect.com/science/article/abs/pii/S0167739X21004337)的原子性。通常在安全性和活跃度之间进行权衡(我们可以在更长的时间内完成传输，或者假设事务将完成并降低延迟)。
*   某个参与者的可提取性的定义是两个不同时间点的效用(以平衡的形式)的差异，考虑到一组行为(或交易)。现在，可以从一组区块链中获得的 MEV 对应于在几个区块链中通过一系列交易获得的余额的差异。嗯，更具体地说，这是在区块链中可以获得的利润，同时只操纵另一个(例如，重新安排交易)。我们可以看到，有可能组合这些操作，使得一个区块链中的动作序列将影响另一个的“初始状态”，并创建一种跨多个域传播的结果链。这意味着，你在多个连锁店中经营的利润可能比在每个连锁店中交易的利润更高。
*   作者说“我们有意允许同时影响多个域的动作之间的模糊区别，以允许将跨链通信协议、桥和域之间的其他交互建模为同时作用于多个域的它们自己的动作”——这是一个好主意，因为正式表示跨链交易可能相当麻烦(参见例如 Hermes:block chain inter operability 的容错中间件)。
*   跨领域的最大可提取价值是选择一组行动的问题，以使其输出最高的最终平衡。在几个系统中选择这些有一些挑战。首先，跨链状态的建模和表示(或者，至少，跨链的一致状态表示)。我们在我们的蹦极论文中解决了这个问题，据我们所知，这是第一个这样做的解决方案。之后，选择这些动作似乎就是一个 NP 完全问题。在这个领域还需要做更多的研究，事实是，桥梁越普遍，越安全，越便宜，MEV 的潜力就越大。
*   作者说“我们预计，鉴于 AMMs 和其他 MEV 加载技术在多个领域的部署，跨多个领域提取 MEV 的好处通常会超过共谋的成本”
*   人们不一定需要使用桥来最大化 MEV:在每个链上都有资金可能就足够了。
*   因此，我们可以说跨链 MEV 问题是 MEV 的推广(但是由于不同区块链、新的安全假设和不同的系统模型的组成，这要困难得多)。
*   有趣的是，作者认为国家的概念并不与任何特定的区块链联系在一起，但是并没有正式的描述。在我们正在进行的论文《蹦极》中，我们定义了任意状态的概念，它可以用来表示任何区块链中的信息。我们还定义了域的概念，作为某个参与者可以看到的全局状态的子集。随着任意状态，一个人可以构建我们所谓的区块链观点。从区块链参与者的角度来看，区块链视图是全局状态的子集，具有初始和最终时间戳。这可能是一个很好的结构来推理交叉链 MEV。
*   定序者/挖掘者相互勾结的跨链 MEV 可能会产生不利的后果:对该链的公平感减弱，结果是代币价值也降低。
*   交叉链 MEV 是一个新兴的研究领域。一定要在 MEV 上查一些好的参考资料:[https://arxiv.org/abs/2101.05511](https://arxiv.org/abs/2101.05511)；【https://ieeexplore.ieee.org/abstract/document/9519469;[https://arxiv.org/abs/2106.07371](https://ieeexplore.ieee.org/abstract/document/9519469?casa_token=PSCYOuQlyAkAAAAA:1bZZ_L_SaAfrt3P4NuLE2l3U6SHiPTH9mqEnXLwyqofCZXvkSDHzqz6WGAen3iZ_5cwoQ5NGKg)[；(关于更通用的区块链互操作性，另请参见](https://arxiv.org/abs/2106.07371)[https://dl.acm.org/doi/abs/10.1145/3471140](https://dl.acm.org/doi/abs/10.1145/3471140)和[https://www . techrxiv . org/articles/preprint/Do _ You _ Need _ a _ Distributed _ Ledger _ Technology _ inter operability _ Solution _/18786527/1](https://www.techrxiv.org/articles/preprint/Do_You_Need_a_Distributed_Ledger_Technology_Interoperability_Solution_/18786527/1))

**🚀它与我们在 Técnico Lisboa、INESC-ID 和 Blockdaemon 的工作有何关系？(观点是我自己的，不一定反映我的雇主的意见)**

*   当互联区块链的需求出现时，我们看到了一个新的研究领域:区块链互操作性。我们正在努力了解如何创建稳健、安全的解决方案以及新技术。在跨链的背景下研究 MEV 将允许令人兴奋的新方向。

🚀**这对我们的工作有什么启示？**

*   这项工作启发了我们，让我们思考应用层区块链互操作性的含义。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   【Capital.com】|[港加密借贷平台](https://coincodecap.com/crypto-lending-hong-kong)
*   [如何在 Uniswap 上交换加密？](https://coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 评论](https://coincodecap.com/a-ads-review)
*   [WazirX vs CoinDCX vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [本地比特币审核](/coinmonks/localbitcoins-review-6cc001c6ed56) | [加密货币储蓄账户](https://coincodecap.com/cryptocurrency-savings-accounts)
*   [什么是保证金交易](https://coincodecap.com/margin-trading) | [美元成本平均法](https://coincodecap.com/dca)
*   [支持卡审核](https://coincodecap.com/uphold-card-review) | [信任钱包 vs 元掩码](https://coincodecap.com/trust-wallet-vs-metamask)
*   [Exness 回顾](https://coincodecap.com/exness-review)|[moon xbt Vs bit get Vs Bingbon](https://coincodecap.com/bingbon-vs-bitget-vs-moonxbt)