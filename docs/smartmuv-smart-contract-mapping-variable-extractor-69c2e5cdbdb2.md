# SmartMuv:智能合同映射变量提取器

> 原文：<https://medium.com/coinmonks/smartmuv-smart-contract-mapping-variable-extractor-69c2e5cdbdb2?source=collection_archive---------36----------------------->

![](img/31f7b1ec600d9db945f560e814d903d0.png)

在 solidity 或 Ethereum 智能合约中，映射就像一个散列表。它用于将数据存储为键-值对，其中键可以是任何内置数据类型，而不是引用类型，而值可以是任何类型。在以太坊中，映射主要用于唯一地址与相关值类型的关联。

映射数据结构在智能合约中起着相当重要的作用。今天，当每个人都使用 ERC20 标准发行他们的代币时，其中保存用户余额的数据结构是映射数据结构。不仅令牌契约，其他智能契约也使用映射数据结构来保存与用户相关的数据。在许多用例中，smart contact 开发人员或所有者需要映射变量数据，例如，他们可能需要将所有余额迁移到另一个 *gas 优化的*版本的 smart contract，或者他们可能只想从映射变量中获取一些统计数据

为了获得用于迁移的智能合同数据或做出决策，需要期待映射变量的提取。

## 有什么问题？

嗯，映射是(key，value)结构，其中值是根据每个键存储的。在 solidity 中，值是根据键的散列存储的，因为散列是不可逆的，所以很难恢复映射键，除非你通过使用[硬编码的源代码得到它。](https://ethereum.stackexchange.com/questions/15337/can-we-get-all-elements-stored-in-a-mapping-in-the-contract)但是使用代码来跟踪映射键应该很麻烦，因为你必须为每个映射变量编写代码(特定的循环),这只会增加你的代码长度。此外，它仅在部署智能合同之前适用。那么，那些已经部署的合同呢？

这仅仅意味着一旦映射被创建和部署，DApps 开发者就无法知道映射的内容是什么。

## [SmartMuv](https://smartmuv.app/)

SmartMuv 只需点击几次**，即可提供映射键及其值的完整列表。首先，它分析您的契约，并为您提供一个映射变量列表，告诉您它是否是可提取的。然后在提取时，它会为您提供完整的映射键列表及其相关值。该工具提供了一种非常简单的方法来跟踪您的重要映射变量，并在许多场景中帮助开发人员和 DApps 所有者，如迁移、升级、业务决策的成本估计。**

**参考资料:**

**更多信息和支持[https://smartmuv.app/](https://smartmuv.app/)**

> ***加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资***

# **另外，阅读**

*   **[Bookmap 评论](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)**
*   **最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)**
*   **[新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)**
*   **[红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)**
*   **[投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)**