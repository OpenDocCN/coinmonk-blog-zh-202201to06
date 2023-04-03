# 燃料网络入门—区块链路线图

> 原文：<https://medium.com/coinmonks/get-started-with-fuel-network-blockchain-roadmap-f3f5042c8f99?source=collection_archive---------8----------------------->

![](img/22e285c2a82173ca5f999a1bc900d209.png)

Photo by [Emir Anık](https://www.pexels.com/tr-tr/@emir-anik-45418356/) on [Pexels](https://www.pexels.com/)

约翰·阿德勒是 Celestia 和燃料网络的创始人。Celestia 是一个正在开发中的区块链，Fuel Network 是第一个在以太坊 Mainnet 上运行的乐观 Rollup，所以只能转移简单的支付令牌，没有智能合约。这两个项目将在不久的将来合作。

[](https://fuel.network/) [## 燃料网络

### Fuel 是下一代区块链开发人员体验，为以下方面提供了巨大的性能改进…

燃料网络](https://fuel.network/)  [## Celestia 规格

### “虚拟侧链”的 App(应用程序)别名 Celestia 应用程序是将其所有数据发布到…

celestiaorg.github.io](https://celestiaorg.github.io/celestia-specs/latest/specs/architecture.html) [](https://github.com/FuelLabs) [## 燃料实验室

### 燃料实验室正在建造燃料，世界上最快的模块化执行层。📝燃料协议的规格和…

github.com](https://github.com/FuelLabs) 

最近在区块链生态系统中讨论最多的话题之一是模块化架构。这实际上意味着区块链目前使用的整体架构是分散的，但仍然可以互操作。
使用多年的比特币、以太坊等区块链，都是单片架构。区块链用整体式建筑实现了三个基本要素的结合；

操作是在系统中进行的，其任务是执行、计算。

对于共识任务，列出了系统中执行的流程。
通过数据可用性任务，系统中的交易数据以可访问的方式存储。

这三个基本要素出现在同一个系统中的事实限制了该系统的潜力。当节点试图同时做许多事情时，组成系统的结构实际上会遇到瓶颈。

[](/@buraktahtacioglu/celestia-data-availability-as-a-service-blockchain-roadmap-15e624c9af23) [## Celestia(数据可用性即服务)—区块链路线图

### 区块链是执行状态机复制(SMR)的分布式网络。SMR 有三个基本阶段:数据…

medium.com](/@buraktahtacioglu/celestia-data-availability-as-a-service-blockchain-roadmap-15e624c9af23) 

另一方面，将与模块化架构一起工作的区块链将这些元素彼此分离；
在执行层，进行链外计算和运算，进行事务处理。汇总用于此任务。

结算层包括汇总层和执行层。
在共识层，交易被列出，交易的数据以可访问的方式被存储。

与单片架构相反，在模块化架构中，相同的节点不执行许多不同的任务，因此降低了系统的负载。

像 Celestia 这样的模块化区块链被设计成仅充当共识层。在以太坊主网上部署(结算)时，汇总(执行)可以将其数据发送到 Celestia(数据可用性)。
易拉宝在以太坊主网上运行，存款和取款都在以太坊上进行，不要错过以太坊巨大的网络效应。它还通过将其数据发送到 Celestia 而不是以太坊，节省了将数据发送到以太坊的成本。它只向以太坊发送欺诈证明或有效性(零知识)证明。

[](/coinmonks/get-started-with-layerzero-blockchain-roadmap-9f8f3ec88e27) [## LayerZero 入门——区块链路线图

### 到 2022 年，可以说区块链和加密货币已经实现了真正的产品市场契合，除了…

medium.com](/coinmonks/get-started-with-layerzero-blockchain-roadmap-9f8f3ec88e27) 

由于数据可用性抽样技术，发送到 Celestia 的交易数据可以很容易地进行审计。检查数据的存在是很重要的，因为对于最简单的例子，乐观汇总验证器需要检查数据来检测带有欺诈证据的无效事务。类似地，如果 zk-Rollup 事务的数据不可访问，就无法知道谁拥有该 Rollup 中的什么。

 [## 具有数据可用性抽样的分叉选择规则

### Tendermint 在诚实的 2/3 投票权假设下提供终结性。这是几个“BFT”共识之一…

celestiaorg.github.io](https://celestiaorg.github.io/celestia-specs/latest/rationale/fork_choice_das.html)  [## ZK-汇总

### 等离子体是建筑可伸缩性方法的名称，这种方法将第 2 层块放在以太坊的顶部…

docs.ethhub.io](https://docs.ethhub.io/ethereum-roadmap/layer-2-scaling/zk-rollups/) 

数据可用性采样技术允许节点验证该块的内容已经发布，而无需下载整个块的数据。为了验证其他区块链的数据是否在单片区块链中发布，节点必须下载所有数据并且是完全节点。

 [## Celestia 规格

### 块是 Celestia 区块链的顶层数据结构。块头，这是完全下载的…

celestiaorg.github.io](https://celestiaorg.github.io/celestia-specs/latest/specs/data_structures.html) 

L2 操作员汇总验证器将汇总中的交易数据发送给 Celestia，并将证明发送给 Ethereum。Celestia 验证器将发送给它们的数据的可访问性证明发送到以太坊。

汇总合同确保 Celestia 中的数据可用。
依靠 Celestia over Ethereum 进行数据存储是一个重要的选择。Celestia 中会出现的问题可能会影响以太坊上的这个角色，但 Celestia 本身有安全措施来威慑砍杀等恶意行为者。

[](https://ethresear.ch/t/global-slashing-attack-on-eth2/6703) [## 对 ETH2 的全球砍杀攻击

### 这是一个非常可怕的攻击，一个开源开发者可以在 ETH2(或任何其他的利益相关网络)上进行攻击…

ethresear.ch](https://ethresear.ch/t/global-slashing-attack-on-eth2/6703) 

燃料网络被定义为执行层。换句话说，它是第一个也是唯一一个在以太坊主网上工作的乐观汇总，是无信任和无权限的。燃料团队的愿景是不同的，他们知道应该在可以运行智能合同的系统中进行扩展。

FuelVM 是一种类似于 EVM 的虚拟机。它与 EVM 的区别在于，它可以与 UTXO 一起运行智能合约，通过这种方式，系统可以并行批准交易。

[](https://www.investopedia.com/terms/u/utxo.asp) [## 什么是 UTXO 型号？

### 未用交易输出(UTXO)是一个技术术语，指的是在交易结束后剩余的数字货币量

www.investopedia.com](https://www.investopedia.com/terms/u/utxo.asp) 

由于以太坊的架构，在以太坊中，节点按顺序批准事务，而在 Fuel 中，节点可以并行批准事务。由于使用 UTXO 的操作的状态转换是显而易见的，所以不在同一状态上操作的操作 A 和 B 可以并行确认。

[](https://academy.horizen.io/technology/expert/utxo-vs-account-model/) [## UTXO 与客户模型

### 为了让数字货币变得有用，它必须是可转移的。区块链上的资金转移是由…

academy.horizen.io](https://academy.horizen.io/technology/expert/utxo-vs-account-model/) 

并行操作确保了 CPU 的充分效率。由于可以使用多个 CPU 内核来验证进程，系统的整体效率得到了提高。使用一个以上的 CPU 内核非常重要，因为虽然当今开发的 CPU 内核数量增加了，但单个内核提供的性能质量却没有提高。由于 EVM 和以太坊自身的架构，它们很难允许并行交易，所以它们更喜欢使用与 EVM 不兼容的架构。UTXO 模型也在 Cardano 等智能合约平台上进行了测试，但这大大限制了用户体验。

 [## Sway 编程语言

### Sway 是一种用于 Fuel 虚拟机(FuelVM)的领域特定语言(DSL ), Fuel VM 是一种区块链优化的 VM，设计用于…

fuellabs.github.io](https://fuellabs.github.io/sway/latest/) [](https://www.rust-lang.org/) [## 锈

### Rust 速度惊人，内存效率高:没有运行时或垃圾收集器，它可以支持关键性能…

www.rust-lang.org](https://www.rust-lang.org/)  [## 坚固性—坚固性 0.8.15 文件

### 部署合同时，您应该使用最新发布的 Solidity 版本。除了特殊情况，只有…

docs.soliditylang.org](https://docs.soliditylang.org/en/v0.8.15/) 

模块化建筑层正在迅速发展，可以看出这些发展项目是相辅相成的。燃料开发商表示，必要的优化和扩展应集中在执行部分，因为数据可用性部分的问题已经通过 Celestia 使用的数据可用性采样等技术得到了解决。

下一篇文章再见…

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [比斯勒点评](https://coincodecap.com/bitsler-review)|[WazirX vs coin switch vs coin dcx](https://coincodecap.com/wazirx-vs-coinswitch-vs-coindcx)
*   [7 大副本交易平台](https://coincodecap.com/copy-trading-platforms) | [BuyCoins 点评](https://coincodecap.com/buycoins-review)
*   XT.COM 评论 | [币安评论](https://coincodecap.com/xt-com-review)
*   [SmithBot 评论](https://coincodecap.com/smithbot-review) | [4 款最佳免费开源交易机器人](https://coincodecap.com/free-open-source-trading-bots)
*   [杠杆令牌](/coinmonks/leveraged-token-3f5257808b22) | [最佳密码交易所](/coinmonks/crypto-exchange-dd2f9d6f3769) | [Paxful 点评](/coinmonks/paxful-review-4daf2354ab70)
*   [加密套利](/coinmonks/crypto-arbitrage-guide-how-to-make-money-as-a-beginner-62bfe5c868f6)指南| [如何做空比特币](/coinmonks/how-to-short-bitcoin-568a2d0b4ae5)