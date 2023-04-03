# 使用宇宙软件开发工具包第 1 部分构建特定于应用的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8?source=collection_archive---------3----------------------->

![](img/908c76d7891996a807ba0ef651688ef3.png)

Photo by [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/blockchain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

分权赋予了更多的自主权和自由。好吧，这是系列的第 1 部分-*使用 Cosmos SDK 构建特定于应用的区块链。*在这里，我们将讨论**为什么会出现**、**如何出现**以及构建应用特定区块链背后的**动机。**

## **当前场景……**

随着加密趋势的发展，人们对加密交易更感兴趣，但并不完全了解底层技术是如何解决更大问题的。此外，大多数加密初创公司正在开发交易所、NFT 或元宇宙项目。尽管这些都是好项目，并且有完全不同的用例集，但我相信，还有许多其他存在的现实世界的问题可以通过分散化来解决。

好吧，让我从建立 dapp 背后的动机开始-

## **dapp 背后的动机……**

![](img/fe6e5727da7127729b294617d4373d0d.png)

Photo by [shawnanggg](https://unsplash.com/@shawnanggg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/restaurant?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

让我告诉你一个小事件。最近我参观了我所在地区的一家著名餐馆。它以味道闻名，通常会很拥挤。出于好奇，我问店主是否与在线送餐应用程序有关联。使用在线送货选项，他的销售额可以增加两倍。他的反应与我预期的相反。几个月前，他实际上已经在网上列出了他的餐馆，然而他在一个月内遭受了巨大的损失。据他称，食品配送公司给他各种借口(*)，比如订单处理从他那端延迟，公司因 covid 而亏损等。*)并只支付了他最初约定佣金的四分之一。

你看到这里的问题了吗？所有与基金相关的活动都由单一业务方处理(我称之为**集中发行**)。因此，供应商不信任在线快递公司。好吧，让我们理解分权在这里有多有帮助。如果与资金相关的活动被分散的网络所占据，任何一方都不会有任何违约的机会，信任问题将会在其中得到解决。

这个用例让我思考并实际尝试了这个挑战。

## **为什么特定应用区块链……**

![](img/21bfbc0de856f4197debcc60743b5d16.png)

Photo by [Kanchanara](https://unsplash.com/@kanchanara?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/ethereum?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

嗯，像**以太网**这样的通用虚拟机区块链有各种限制。让我指出这些-

*   **高额燃气费**。如果汽油费很高，我们的用例采用区块链不会太多。虽然随着即将到来的 Eth 2.0 升级(共识将从 POW 改为 POS **)** 、**、**ZK-up、乐观-up、等离子链和碎片，更多的性能改进将会出现，这可以降低燃气价格。但是无论如何，对于区块链的特定应用，应用利益相关者可以控制天然气价格。
*   智能合约都是由**同一个虚拟机**运行的。这意味着它们会争夺资源，这会严重限制性能。而在特定于应用程序的区块链中，该应用程序不会与其他应用程序竞争计算和存储。
*   为了避免**安全漏洞**，一个人应该在某个智能合同语言上有很高的专业知识。对于智能合约开发，也限制到某种语言。然而，当使用 cosmos sdk 在 Tendermint 上构建 dapp 时，可以使用他们自己选择的任何语言(共识层是去耦的，并且与应用层无关)。
*   应用程序的**治理**很有可能与区块链社区的治理不一致。而在应用程序特定的区块链，利益相关者拥有完全的控制权，可以通过提交建议和安排验证者之间的投票来决定链升级。

**为什么选择 Cosmos SDK…**

![](img/cb142f8a7d8d44e52cb349ec1b6f4786.png)

Photo by [Guillermo Ferla](https://unsplash.com/@gferla?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cosmos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Cosmos SDK 允许在 Tendermint 上构建安全的区块链应用程序。这种链由可组合的模块构建而成(**与单片设计**相反)。人们可以很容易地为 Cosmos SDK 创建自定义模块，并将其与内置模块集成，以开发特定于应用程序的区块链。由于 consensus engine layer tender mint core 在这里被解耦，因此人们可以轻松地专注于开发特定于用例的功能。PBFT + DPOS 达成共识的方式是强有力的，也是一个伟大的选择。此外，这种链带有块终结的概念，因此在任何事故的情况下，链将停止而不是分叉(链分裂)。此外，Cosmos SDK 已经用于构建许多已经投入生产的特定应用区块链，如 **Cosmos Hub、币安 chain、Terra、Kava 等**。

太好了，你已经走了这么远了:)。由于我们已经讨论了我们的用例，并决定采用应用特定的区块链，在下一部分，我们将重点放在我们项目的技术方面。

这里引用源代码- [*源代码*](https://github.com/Harry-027/deal)

系列
*[*Part-1*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*Part-2*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
*[*Part-3*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*Part-4*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc) ***[*Part-5*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3) ***

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   【T43 商业评论 | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)