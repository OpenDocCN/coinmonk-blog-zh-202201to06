# 在 Hyperledger Fabric 上阅读 5 篇论文

> 原文：<https://medium.com/coinmonks/5-papers-to-read-on-hyperledger-fabric-a0504c5a685?source=collection_archive---------49----------------------->

![](img/737a34552426522825cc6d3f9a32e8e2.png)

Photo by [Mel Poole](https://unsplash.com/@melpoole?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/fabric?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

1.  **将一个具有经典工作负载的基准移植到区块链:Hyperledger Fabric 上的 TPC-C(**[**arXiv**](https://arxiv.org/pdf/2112.11277.pdf)**)**

**作者:** [阿提拉·克莱尼克](https://arxiv.org/search/?searchtype=author&query=Klenik%2C+A)，[伊姆雷·科奇斯](https://arxiv.org/search/?searchtype=author&query=Kocsis%2C+I)

**摘要:**总部位于区块链的分布式账本技术(DLT)的许多跨组织合作应用并不以合作模式层面的创新为目标:本质上相同的“业务”由各方进行，但这次没有可信任的记账中心方。迁移到 DLT 预计会对性能产生负面影响，但一些 DLT(如 Hyperledger Fabric)被认为在性能方面更适合此类用例。然而，尽管有些令人惊讶，但 DLT 的应用程序级性能基准的持续缺乏，对“经典”工作负载的跨 DLT 比较以及对“数据块链化”的性能影响的评估仍然缺乏支持。我们展示了 Hyperledger Fabric 的经典 TPC-C 基准的完整端口的设计和基于 Hyperledger Caliper 的开放实现，以及将原始数据库模式转换为智能合同数据模型的结构化方法。还包括对影响大规模性能评估设计的工作负载特征的初步测量。

**2。在 Hyperledger Fabric 中评估区块链应用需求及其满意度(**[**arXiv**](https://arxiv.org/pdf/2111.15399.pdf)**)**

**作者:** [萨多克·本·图米亚](https://arxiv.org/search/?searchtype=author&query=Toumia%2C+S+B)，[克里斯蒂安·白尔杰](https://arxiv.org/search/?searchtype=author&query=Berger%2C+C)，[汉斯·p·赖泽](https://arxiv.org/search/?searchtype=author&query=Reiser%2C+H+P)

**摘要:**与集中式解决方案相比，区块链应用可以提供更好的容错性、完整性、可追溯性和透明性。尽管有这些好处，很少有企业转向基于区块链的应用程序。行业担心当前的区块链实施不能满足他们的要求，例如在可扩展性、吞吐量或延迟方面。Hyperledger Fabric (HLF)是一种许可的区块链基础设施，旨在满足企业需求，并提供高度模块化和精心设计的架构。在本文中，我们通过主要关注性能和弹性特征，调查和分析了区块链应用程序在底层基础设施方面的需求。随后，我们讨论 Fabric 的当前设计在多大程度上满足这些要求。我们进一步评估了 Hyperledger Fabric 2.2 的性能，模拟了不同的用例场景，比较了单订单和多订单服务的性能，并对混合工作负载进行了评估

**3。使用 Hyperledger Fabric 区块链技术的物联网系统防篡改保护(**[**【arXiv】**](https://arxiv.org/pdf/2109.07074.pdf)**)**

**作者:** [阿德南](https://arxiv.org/search/?searchtype=author&query=Iftekhar%2C+A)，[崔晓晖](https://arxiv.org/search/?searchtype=author&query=Cui%2C+X)

**摘要:**自动化和工业物联网(IoT)设备日益增多。随着物联网设备数量的增长，它们生成的数据量也将增长。在不久的将来，高效管理这些快速扩展的物联网设备和海量数据，使其可供所有授权用户使用，而不损害其完整性将变得至关重要。另一方面，记录了许多信息安全事件，增加了对对策的要求。尽管迄今为止针对敌对第三方的防护措施已经司空见惯，但运营商和各方已经看到对数据篡改检测和阻止的需求不断增长。区块链技术以其隐私性、不变性和去中心化的特性而闻名。作为物联网平台，单板计算机变得越来越强大，同时也变得越来越实惠。这些单板计算机正在自动化工业中获得牵引力。这项研究重点关注物联网-区块链集成的范式，其中区块链节点在物联网平台上自主运行。它使系统能够在没有人干预的情况下进行机器对机器的交易，并对物联网设备进行直接访问控制。本文假设读者熟悉 Hyperledger Fabric 的基本操作，并关注集成的实际方法。为区块链的新手提供了基本的介绍

**4。了解 Hyperledger Fabric 的可扩展性(**[**【arXiv】**](https://arxiv.org/pdf/2107.09886.pdf)**)**

**作者:**

**摘要:**区块链系统的快速发展导致人们越来越有兴趣了解和比较区块链的规模表现。在本文中，我们重点分析 Hyperledger Fabric v1.1 的性能，这是最流行的许可区块链系统之一。先前的工作已经深入分析了 Hyperledger Fabric v0.6，但是新版本的系统经历了显著的变化，需要进行新的分析。现有的系统基准测试工作范围有限:一些只考虑小型网络，另一些只考虑部分系统的可伸缩性，而不是整个系统。我们对 Hyperledger Fabric v1.1 版进行了全面的大规模性能分析。我们扩展了现有的基准测试工具，在许多服务器上进行实验，同时扩展系统的所有重要组件。我们的结果表明，Fabric v1.1 的可伸缩性瓶颈在于执行和订购阶段之间的通信开销。此外，我们表明，扩展用于订购阶段的 Kafka 集群不会影响总体吞吐量。

**5。区块链机器:Hyperledger Fabric 的附网硬件加速器(**[**arXiv**](https://arxiv.org/pdf/2104.06968.pdf)**)**

**作者:**哈里斯[贾瓦德](https://arxiv.org/search/?searchtype=author&query=Javaid%2C+H)、[杨楫](https://arxiv.org/search/?searchtype=author&query=Yang%2C+J)、[纳塔尼亚·桑托索](https://arxiv.org/search/?searchtype=author&query=Santoso%2C+N)、[莫希特·乌帕德哈耶](https://arxiv.org/search/?searchtype=author&query=Upadhyay%2C+M)、[孙达拉拉奥·莫汉](https://arxiv.org/search/?searchtype=author&query=Mohan%2C+S)、[陈诚·胡](https://arxiv.org/search/?searchtype=author&query=Hu%2C+C)、[戈登·布雷布纳](https://arxiv.org/search/?searchtype=author&query=Brebner%2C+G)

**摘要:**在本文中，我们展示了 Hyperledger Fabric(最流行的许可区块链之一)如何受益于网络连接加速。Fabric 的可扩展性和峰值性能主要受限于其数据块验证/提交阶段的瓶颈。我们提出了区块链机器，一个硬件加速器和一个硬件友好的通信协议，作为验证者对等体。它可以适应应用程序及其智能合约，并面向带有网络连接 FPGA 加速卡的服务器。区块链机器直接从网络接口检索硬件中的区块及其事务，然后通过可配置的高效区块级和事务级管道进行验证。然后，验证结果被传送到执行非瓶颈操作的主机 CPU。从我们与 Fabric v1.4 LTS 集成的实现中，我们观察到，与纯软件验证器对等体相比，块验证的速度提高了 12 倍，提交吞吐量高达 68，900 tps。我们的工作提供了一个加速平台，将促进对许可区块链的硬件加速的进一步研究。

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [有哪些交易信号？](https://coincodecap.com/trading-signal) | [Bitstamp vs 比特币基地](https://coincodecap.com/bitstamp-coinbase) | [买索拉纳](https://coincodecap.com/buy-solana)
*   [ProfitFarmers 回顾](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix Trading Bot](https://coincodecap.com/cornix-trading-bot)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [my constant Review](https://coincodecap.com/myconstant-review)|[8 款最佳摇摆交易机器人](https://coincodecap.com/best-swing-trading-bots)
*   [MXC 交易所评论](/coinmonks/mxc-exchange-review-3af0ec1cba8c) | [Pionex vs 币安](https://coincodecap.com/pionex-vs-binance) | [Pionex 套利机器人](https://coincodecap.com/pionex-arbitrage-bot)
*   [我的密码交易经验](/coinmonks/my-experience-with-crypto-copy-trading-d6feb2ce3ac5) | [比特币基地评论](/coinmonks/coinbase-review-6ef4e0f56064)