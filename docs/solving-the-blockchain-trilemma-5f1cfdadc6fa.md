# 解决区块链三难困境

> 原文：<https://medium.com/coinmonks/solving-the-blockchain-trilemma-5f1cfdadc6fa?source=collection_archive---------41----------------------->

![](img/89a9c4399bb642928b25feb837055ecd.png)

bored Ape Yacht Club(BAYC)的元宇宙土地销售“Otherdeed”成为一个热门事件，不仅是因为它在 NFT 的蓝筹股人气，也是因为薄荷期间过高的汽油费，支付约 5 ETH(14，000 美元)的汽油费，以从 55，000 块可供出售的土地中分得一杯羹。在此期间，它的铸造价格为 305 枚猿币(4575 美元)。

在 EVM 链的另一端，Solana 停止生产区块，原因是来自机器人的大量事务，达到每秒 600 万次事务和来自铸造 NFT 的 100 Gbps 流量，导致网络中断并重新启动网络。

这肯定收到了各种用户在各自链上的负面反馈。在这篇文章中，我们分享了我们对发生了什么以及如何通过理解区块链三元悖论来解决这些问题的见解。

![](img/d8fa1593599db8754eb03b80cf6df75f.png)

*Blockchain Transaction issues from Ethereum and Solana*

这两个问题都可以从链的利用区块空间的共识中找到根源。区块空间是交易建立、验证和完成的媒介，在区块链上创建记录。它是为任何区块链网络的心跳提供动力的商品。 ***区块空间市场*** 有以下组成部分:

🔹**用户:**请求将他/她的交易包含在区块链上的块空间

🔹**交易费:**用户为交易进行验证并计入区块空间所支付的金额(也可以是矿工的服务费)

🔹**挖掘器:**产生块，并包括要跨网络节点验证和完成的块空间中的事务。这些可以是一个单独的矿工或一组矿工(采矿池)

🔹 **Mempool:** 一个空间，未验证或挂起的事务就在这里，等待矿工验证

以太坊和索拉纳使用块空间的方式有所不同:

![](img/da9fee5fb1f682d44d1690528529141f.png)

如果没有适当的步骤来解决这个问题，Crypto 将很难扩展。但是我们能追求什么步骤呢？

🔹*我们增加块空间了吗？*但这让任何人都可以成为区块链上的一个节点(可扩展性与去中心化问题)

🔹*我们是否删除事务规则以降低块空间需求？*这可能会导致一些黑客/漏洞问题(可扩展性与安全性问题)

🔹*中央操作数据库是为了提高速度而构建的吗？*但是，由一个中央实体来运营该链会产生交易方风险，如透明度(安全性和可扩展性与分散化问题)

要理解这其中的复杂性，重要的是理解 ***区块链三难***

区块链三元悖论是由*[***Vitalik Buterin***](https://coinmarketcap.com/alexandria/glossary/vitalik-buterin)提出的一个概念，提出了一组三个主要问题——去中心化、安全性和可伸缩性。这些问题是开发人员在构建区块链时遇到的，迫使他们最终牺牲一个“方面”作为折衷，以适应其他两个方面。*

*可伸缩性和分散性经常受到安全性的阻碍，但是安全性往往会受到提供可伸缩性的网络上的任何变化的损害。项目要么选择专注于两个问题，但三个问题的解决方案可能会导致加密货币和区块链的更大采用，以及该技术在各行业的广泛使用。*

*![](img/a7123d8a123ac7093606e765de9c903a.png)*

**Blockchain Trilemma**

***以太坊***

*以太坊是一个经过验证的安全和去中心化链，通过增加费用需求来控制垃圾邮件，但这导致了扩展困难。以下是一些可以解决扩展问题的选项:*

1.  ***切分** —切分是以太坊 2.0 的一部分，每个人都对此感到兴奋，并将于 2022 年推出。分片是通过创建新的链(称为“分片”)来水平分割数据库以分散负载和增加每秒事务的过程。以太坊 2.0 将创建 64 个新链作为“碎片”，每个链将与信标链并行运行。*
2.  ***易拉宝** —易拉宝是一种离线解决方案(不使用区块链网络的解决方案)。为了简化，他们在以太坊之外执行交易，将这些交易卷成一个，然后结算回以太坊。一些例子是 Arbitrum、乐观、ZKSync、STARKware 和 Metis*
3.  ***侧链** —这些是通过桥连接到以太坊的 EVM 兼容链。他们有自己的共识机制来执行交易。多边形就是一个例子*

*Roll-ups 正在成为以太坊扩展问题的主要解决方案之一，因为它们拥有开发人员可以轻松构建的工具，并通过用户对已启动应用的活动及其 TVL 性能快速增长。*

*![](img/40b92762e61a588dccf6eab9553200a0.png)*

*Total Value Locked in Optimism and Arbitrum*

*索拉纳*

***Solana 的每个块空间无限事务的问题，被僵尸程序利用导致验证程序耗尽内存和崩溃，可以通过 Solana 实验室宣布的以下方法修复:***

1.  ***QUIC——Solana 的核心协议在 QUIC 之上被重新实现，QUIC 是由 Google 建立的一个协议。一旦被采用，将会有更多的选择来适应和优化数据接收。***
2.  *****股权加权交易 QoS** — Solana 将阻止当前不加区别地接受交易的做法，转而整合股权加权交易处理***
3.  *****基于费用的执行优先级** —在这种模式下，用户将能够在执行交易并将其包含在块中时，指定除基本费用之外的额外费用***

***从某种意义上说，索拉纳将实施以太坊中现有的机制来控制无限制的交易***

***![](img/41105d7a0254ffa2004dbf17a57de041.png)***

*****多链*****

***多链为每个区块链的劣势扩展了机会，通过链之间的网络互联创建解决方案以进行交互，并为 dApps 提供可组合性。***

***为了理解多链，首先我们定义什么是交叉链。***

******交叉链*** 提供区块链网络之间的互连，允许信息和价值的交换:***

***🔹通过允许主链在另一个区块链中运行来承受主链的压力***

***🔹在链之间为用户提供各种 dApps***

***🔹通过利用每个区块链的容量增强可扩展性***

***cross-chain 的一个败笔是它的中间媒介 bridges，由于它们持有在链上桥接资产的资金，这些媒介容易受到各种黑客和诈骗的攻击。桥梁持有的资产越多，就越有动力去破坏桥梁。根据 Vitalik Buterin 的说法," c *ross-chain 活动具有反网络效应:虽然这种活动不多，但相当安全，但发生得越多，风险就越大，"****

***![](img/514f5809f22c961068f9e6596fa7adac.png)***

***Recent hacks from bridges***

*****多链**网络另一方面是将区块链层级结构的某一层模块化的网络，不仅支持快速链构建，还充当其他区块链的扩展层。简而言之，这是一个在母链中容纳各种区块链的结构。***

***火币研究院研究员 ***叶延伟*** 表示:*“即使面对区块链三难困境，多链网络在安全性、去中心化和可扩展性方面提供了更好的解决方案。而且，多链网络的生态模式和发展是整个区块链产业需要效仿的”。****

***以下是多链协议的一些示例:***

1.  *****Cosmos** — Cosmos 是区块链的一个生态系统，可以使用内部区块链通信(IBC)协议进行扩展和互操作。一些在 Cosmost 建造的区块链是 Terra，Omosis，Akash 和 Juno。***
2.  ***波尔卡多特——波尔卡多特使用副链连接各种区块链，以便相互通信。Polkadot 内置的区块链使用了底层模块化框架，允许用户插入他们需要的功能，同时也允许他们根据需要进行更改。一些副链的例子是 Moonbeam、Polkadex 和 Acala。***
3.  *****第 0 层** —第 0 层是最近出现的令人兴奋的多链功能协议之一，被称为“Omnichain”。LayerZero 使用链上超轻节点跨链连接 dApps，以中链的成本效益实现轻节点的安全性。***

***![](img/afc1be5cc95d212f1a43160147fde741.png)***

***Multi-chain platforms***

***已经开发了扩展解决方案来满足加密货币采用的需求，但仍有创新想法有待发现。最终， ***多链*** 成为了可组合性和互联性的有利趋势，创造了一个可扩展的生态系统，同时保持了安全性和分散性。沿着这条道路，我们看到了一个全链的未来，连接各种现有的链，而用户甚至不会注意到他们正在使用区块链技术。这一领域的创新通常非常迅速，您有时不会注意到，我们很高兴成为其中的一员。***

***喜欢我们的见解吗？通过我们的社交渠道关注我们:***

*****推特:**[https://twitter.com/EverseHQ](https://twitter.com/EverseHQ)***

*****领英:**[https://www.linkedin.com/company/everse-capital/?viewAsMember=true](https://www.linkedin.com/company/everse-capital/?viewAsMember=true)***

*****参考文献*****

***[https://www . the guardian . com/technology/2022/may/02/yuga-labs-致歉-售后虚拟土地崩溃-以太坊](https://www.theguardian.com/technology/2022/may/02/yuga-labs-apologises-after-sale-of-virtual-land-crashes-ethereum)***

***[https://coin telegraph . com/news/Solana-experies-7-outage-in-2022-as-bots-invasive-the-network](https://cointelegraph.com/news/solana-suffers-7th-outage-in-2022-as-bots-invade-the-network)***

***[https://www . the guardian . com/technology/2022/may/02/yuga-labs-致歉-售后-虚拟土地-崩溃-以太坊](https://www.theguardian.com/technology/2022/may/02/yuga-labs-apologises-after-sale-of-virtual-land-crashes-ethereum)***

***[https://Solana . com/news/04-30-22-Solana-mainnet-beta-outage-report-mitigation](https://solana.com/news/04-30-22-solana-mainnet-beta-outage-report-mitigation)***

***[https://www . coin desk . com/tech/2022/05/01/Solana-goes-dark-for-bots-swarm-candy-machine-NFT-minting-tool/](https://www.coindesk.com/tech/2022/05/01/solana-goes-dark-for-7-hours-as-bots-swarm-candy-machine-nft-minting-tool/)***

***[https://Solana . com/news/04-30-22-Solana-mainnet-beta-outage-report-mitigation](https://solana.com/news/04-30-22-solana-mainnet-beta-outage-report-mitigation)***

***https://research.paradigm.xyz/ethereum-blockspace***

***[https://www . ledger . com/academy/what-is-the-区块链-tri lema](https://www.ledger.com/academy/what-is-the-blockchain-trilemma)***

***[https://ethereum.org/en/developers/docs/scaling/](https://ethereum.org/en/developers/docs/scaling/)***

***[https://research.paradigm.xyz/ethereum-blockspace](https://research.paradigm.xyz/ethereum-blockspace)***

***[https://ethereum.org/en/upgrades/shard-chains/](https://ethereum.org/en/upgrades/shard-chains/)***

***[https://coin telegraph . com/explained/what-a-directed-acyclic-graph-in-crypto currency-how-do-Dag-work](https://cointelegraph.com/explained/what-is-a-directed-acyclic-graph-in-cryptocurrency-how-does-dag-work)***

***[https://101 block chains . com/区块链-可扩展性-解决方案/](https://101blockchains.com/blockchain-scalability-solutions/)***

***[https://finance . Yahoo . com/news/multi-chain-networks-key-区块链-013000762.html](https://finance.yahoo.com/news/multi-chain-networks-key-blockchain-013000762.html)***

***[https://www . business wire . com/news/home/20220330005301/en/LayerZero-Labs-Raises-1.35 亿创建全链条加密网络](https://www.businesswire.com/news/home/20220330005301/en/LayerZero-Labs-Raises-135-Million-to-Create-Omnichain-Crypto-Networks)***