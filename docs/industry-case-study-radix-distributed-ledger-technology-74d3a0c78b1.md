# 行业案例研究:基数分布式账本技术

> 原文：<https://medium.com/coinmonks/industry-case-study-radix-distributed-ledger-technology-74d3a0c78b1?source=collection_archive---------3----------------------->

以下帖子是锅炉区块链案例研究系列的下一期。上次，[我们分析了氦网络](/coinmonks/blockchain-case-study-helium-9f0acda05cbc)，这是一个提供分散式无线连接服务的创新项目。今天的焦点是 Radix，这是一个分布式账本技术项目，旨在服务于分散金融(DeFi)市场。

简而言之，我们对 Radix 的分析发现:

*   Radix 采用了一种独特的共识机制(Cerberus ),该机制利用了网络增强的分片功能
*   Radix 的架构显示了解决“区块链三难问题”和克服第一层(L1)协议可扩展性挑战的前景
*   Radix 在技术上的成功将取决于 mainnet 的最终版本能否提供网络的理论能力

# 背景:区块链三难困境

在过去的一年里，随着用户数量的持续增长超过最初的预期，以太坊等区块链遇到了严重的网络拥塞问题。高昂的天然气费用和缓慢的交易终结使得该网络更难使用，限制了 DeFi 和其他分散油田的发展。有许多解决以太坊问题的建议:值得注意的是，可选的第一层链、侧链、第二层解决方案，如乐观和 ZK-rollups，以及各种分片方法。但是，多个 L2 的同时增长使生态系统的攻击面呈指数级增长，如果 L1 从一开始就被设计为具有足够的能力，这可能会超过它的攻击面。2022 年 3 月中旬，以太坊团队负责人彼得·斯拉吉(Péter Szilágyi)在[发布了一条关于以太坊生态系统复杂性增长的微博](https://twitter.com/peter_szilagyi/status/1504887154761244673)。

Solana 和 Avalanche 等著名的替代 L1 试图通过完全转移到一个不同的区块链来扩展去中心化的活动，通过修改底层技术，在某些方面比以太坊扩展得更好。但替代 L1 通常无法实现分散网络的三大支柱之一，即众所周知的区块链三难困境。

![](img/323dd3ebc27275aa7a9796473214f583.png)

From Vitalik Buterin’s April 2021 article, “[Why Sharding is Great](https://vitalik.ca/general/2021/04/07/sharding.html)”

区块链三元悖论确定了去中心化账本的三个支柱:可伸缩性、安全性和去中心化。它指出，区块链可以使用“简单”的方法实现这三个属性中的两个，但在一个网络中实现所有三个属性是非常困难的，甚至是不可能的。Solana 是可扩展和安全的，但是被集中到 19 个“超级节点”中。它使用这些超级节点，因为运行一个完整的 Solana 节点需要普通消费者无法企及的强大计算机硬件。

对于一个吞吐量足以处理世界上所有分散交互的非共享区块链，运行一个完整节点所需的存储和处理能力几乎不可避免地导致集中到几个“超级节点”中。

# 区块链分片的麻烦在于

输入基数。Radix 是一种正在开发的分布式账本技术(DLT ),旨在解决上述区块链三难问题。值得注意的是，Radix 不是区块链，因为最终设计不包含全局排序或离散的网络范围“块”。基数事务被设计成短暂而简洁的，只在需要的时候持续，并且只在需要的时候接触尽可能多的网络参与者。

Radix 团队认为，基于区块链的分布式分类账架构中的致命设计缺陷阻碍了有效的扩展。

首先，考虑一下单一分类账中涉及的存储和消息复杂性。现有的区块链要求每个节点存储链的整个历史，随着成功网络上事务吞吐量的增长，这变得不可行。例如，比特币启动一个节点的存储需求目前为 [400GB](https://ycharts.com/indicators/bitcoin_blockchain_size) ，而以太坊为 [600GB](https://ycharts.com/indicators/ethereum_chain_full_sync_data_size) 。此外，在整体分类帐中，涉及所有对所有消息的单个共识步骤会导致消息延迟和所需的节点计算能力随着网络事务吞吐量的*平方*而增长。对于涉及多个全对全步骤的共识方法，延迟和计算要求随着吞吐量的立方增长，甚至更糟。请查看[区块链共识协议中的瓶颈](https://arxiv.org/pdf/2103.04234.pdf)，了解几种当代共识机制的复杂性分析。

分片方法试图通过将整体区块链分成更小的部分或分片来解决这个可伸缩性问题。Radix 声称，当前单片 L1 的分片提议将打破原子可组合性，原子可组合性是单片区块链确保链式事务的所有步骤一起成功或失败的能力。例如，原子可组合性已经在涉及快速贷款的创新套利方法中出现了用例。当常规分片方法将每个分片视为独立的区块链，并且难以在多个区块链之间进行通信或同步时，可以大致看出这种破损的原因。参见 Vitalik buter in 2019 年的[评论，证实分片将使原子可组合性变得“困难”(可以说事情从那以后并没有变得更好)。](https://ethresear.ch/t/cross-shard-defi-composability/6268/6)

![](img/a12916841023a141b4e6b29c29bc23cb.png)

An example sharding proposal for Ethereum, from “[Why Sharding is Great](https://vitalik.ca/general/2021/04/07/sharding.html)”: Radix points out ([and Vitalik confirms](https://ethresear.ch/t/cross-shard-defi-composability/6268/6)) that storing an essentially-independent blockchain on each shard would make it difficult or impossible to communicate synchronously across shards.

在概念层面上，针对存储和消息复杂性问题提出的修复方案主要涉及分割拥塞的 L1。但是 L1 的设计并不一定考虑到了分片。有效应用分片来提高区块链网络的可扩展性仍然是一个关键的行业挑战。

# 基数分片模型

Radix 提出了一种非正统的分片方法，据称有助于克服有效可伸缩性的挑战。虽然大多数分片方法采用单片区块链，并将其分成任意数量的更易于管理的链，但 Radix 的分片系统*将数据预分片为几乎无限数量的分片。确切地说，2^256 碎片已经在最后的设计中了。此外，每个碎片不再存储一个“独立的”区块链。Radix 碎片只存储最少量的数据，每个碎片对应一个比特币风格的未用事务输出(UTXO)。*

![](img/4b9550f781d655b8a6645fa156fa904c.png)

Figure 22 from the [Cerberus whitepaper](https://assets.website-files.com/6053f7fca5bf627283b582c2/608811e3f5d21f235392fee1_Cerberus-Whitepaper-v1.01.pdf): Each gray dot and trailing line represents a shard. Green dots represent ’up‘ states while orange dots represent ’down’ states.

Radix 关于 Cerberus 的白皮书使用粒子物理学术语描述了分片模型。UTXO 由“粒子”表示，如果 UTXO 没有被分配给粒子，则每个粒子处于“中性”状态；如果分配的 UTXO 是从事务的输出构建的，则处于“上升”状态；如果 UTXO 被用作另一个事务的输入而被破坏，则处于“下降”状态。每个碎片只包含一个粒子，活动粒子的有限“上”或“下”状态模型应该确保双重花费是不可能的。然后，通过析构一个或多个粒子上的“up”UTXOs，将它们转变为“down”状态，并消耗 UTXOs 以将其他粒子转变为“up”状态来创建事务:例如，这个新粒子可以代表 UTXO 的新所有者。

# Cerberus 共识机制

Radix 的分片模型摆脱了“块”或事务全局排序的概念。在正常的区块链中，直到包含相应数据的块被终结(或提交)，事务才成为最终的。相比之下，Radix 使用大规模分片的数据存储，其中的事务只接触受影响的分片。因此，事务可以并行进行，极大地提高了网络的潜在吞吐量。

Cerberus 是 Radix 设计的共识机制，它利用了增强的分片功能。Cerberus 以特定的方式安排熟悉的区块链原语，以确保并行事务处理。Cerberus 还允许动态验证器集，每个验证器集包含可调数量的节点。每个验证器集被分配给一些碎片集。

对 Cerberus 的基本理解可以建立在三个层次上。

首先，单个验证器集使用一些通用的区块链共识机制，在他们管理的单个碎片上进行共识。Cerberus 白皮书使用了 [HotStuff](https://arxiv.org/pdf/1803.05069.pdf) Byzantine 容错机制作为示例，但是任何满足一些基本要求的机制都应该足够了。

![](img/df9cfb93cda21fd5086a8b42469bc9c0.png)

Figure 3 from the Cerberus whitepaper: Local consensus, conducted by a validator set on a single shard. This local consensus can be achieved using any consensus mechanism capable of producing a [Quorum Certificate](https://en.wikipedia.org/wiki/Quorum_(distributed_computing)), e.g. HotStuff as described in the Cerberus whitepaper.

接下来，一组验证器集合并行操作几个碎片组。这一观点可与现有的区块链分割方案相媲美，在该方案中，一个铁板一块的区块链被分割成一套独立但本质上独立的账簿。如果验证器和碎片像在区块链架构中一样被捆绑在一起，它们将不能在组[碎片]之间自由移动:然而，使用 Radix 的碎片模型，验证器可以根据需要移动到不同的验证器集。

![](img/957fb668978ecec9df0173c5a266f9a4.png)

Figure 4 from the Cerberus whitepaper: Multiple Cerberus validator sets running parallel consensus across multiple shard sets.

最后，Cerberus 利用其分片模型支持的动态验证器/分片集，在其分片空间上大规模并行化一致性。验证器和碎片集根据需要在碎片空间中动态分配，以便在事务影响一些碎片组时达成一致。因此，Cerberus 能够并行执行不相关的事务，消除了现代区块链的一个关键可伸缩性限制，由于区块链固有的全局排序要求，该限制迫使事务等待其他不相关的事务。

![](img/aa292232f1be4283dbfbf627eeac597c.png)

Figure 20 from the Cerberus whitepaper: Cerberus consensus runs across shards as necessary to process transactions, and unrelated transactions can be processed in parallel because each emergent Cerberus instance only needs to touch the shards involved in its own transaction.

# 评估 Radix 的未来

Radix 的解决方案显然拥有*潜力*去做区块链无法为 DeFi 做的事情。然而，*不可否认的是*要实现最终基数设计的最小可行版本，需要多项技术突破。(更不用说一个成功的 L1 项目所需的营销和社区建设了。)

Radix 承认 mainnet 的当前版本远未完成。最终的设计目前计划于 2023 年发布[(或许是乐观的)。Radix 正在其 Cassandra 测试网络上测试和演示“分片冥府守门狗的一些可能实现”，但并不保证这些努力最终会成功。](https://learn.radixdlt.com/article/what-is-the-radix-roadmap)

例如，Jepsen(一个受人尊敬的分布式系统验证团队)最近进行的压力测试突出了几个令人关注的问题。Jepsen [的报告](https://jepsen.io/analyses/radix-dlt-1.0-beta.35.1)分析了 Radix 的 Olympia mainnet 的七个月测试，在此期间，Jepsen 发现了 11 个安全错误，包括“过时、中止和中间读取；承诺交易的部分或全部损失；…不确定交易的活性问题；以及单节点故障期间的性能下降”。

Jepsen 的报告对 Radix 当前网络的功能提出了质疑。然而，当考虑 Jepsen 的结果时，一些额外的上下文点是有帮助的。首先，压力测试中发现的错误似乎很严重，可以修复，并且主要是由于实现。没有一个失败的功能是为了成为“第一”，因为它们已经在现有的区块链得到了证明。第二，该报告源自 Radix Olympia mainnet，并不反映最终的 Radix 设计(如上所述)。与此相关的是，Jepsen 没有反驳最终设计的任何计划功能。最终的设计特性——最重要的是静态预分片和并行一致性——是 Radix 真正的创新之处。

锅炉区块链研究团队需要额外的时间来完全理解 Cerberus 和 Radix 最终设计的内部工作原理。该项目的几个组件很复杂，包括静态预分片、并行共识和动态验证器集。彻底了解所有组件对于全面了解 Radix 的工作原理至关重要。理解基数的过程类似于让 web2“本地人”加入比特币:这需要一种相当不同的思维方式，最初可能看起来违反直觉。

在结束之前，还有三点值得强调:

1.  Radix 无疑是该研究团队见过的最复杂的 L1 设计，但即使是最终的设计也应该没有完全分片和“L2”版本的以太坊或类似的现有区块链复杂。
2.  我们的团队对 Radix 达到声称的生产能力的能力持谨慎乐观态度，因为我们没有发现任何硬分析*否定*最终设计的可行性。我们注意到实现和执行是另一回事。如果 Radix 要接管世界上的分散活动，它必须在现有解决方案建立足够的竞争护城河，使 Radix 无法实现网络效应之前做到这一点。
3.  要全面了解 Radix 及其在 DLT 空间中的位置，需要 a)进一步研究其他扩展解决方案，以便与 Radix 进行对等比较，以及 b)详细分析 Cerberus 本身的内部工作方式。

***

撰稿人:陈楚翔，威尔·德莱尼，哈里斯·哈桑，德凡·帕克，马克斯·蒙卡斯特

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [CoinDCX 评论](/coinmonks/coindcx-review-8444db3621a2) | [加密保证金交易交易所](https://coincodecap.com/crypto-margin-trading-exchanges)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [Bookmap 评论](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   [如何在 FTX 交易所交易期货](https://coincodecap.com/ftx-futures-trading) | [OKEx vs 币安](https://coincodecap.com/okex-vs-binance)
*   [CoinLoan 评论](https://coincodecap.com/coinloan-review) | [YouHodler 评论](/coinmonks/youhodler-4-easy-ways-to-make-money-98969b9689f2) | [BlockFi 评论](https://coincodecap.com/blockfi-review)
*   [XT.COM 评论](https://coincodecap.com/profittradingapp-for-binance) | [币安评论](https://coincodecap.com/xt-com-review)