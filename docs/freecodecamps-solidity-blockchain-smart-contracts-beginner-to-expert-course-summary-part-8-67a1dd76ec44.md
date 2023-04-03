# FreeCodeCamp 的可靠性、区块链、智能合约初级到专家课程总结，第 8 部分

> 原文：<https://medium.com/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-8-67a1dd76ec44?source=collection_archive---------16----------------------->

## 让我们铸造一些 NFT！

![](img/f73c18aef2a1c79d98c589a3c2110a45.png)

[Patrick Collins](/@patrick.collins_58673); the Author of the Course

欢迎来到我总结的第 8 部分！我很高兴你在这里。我写这些文章是为了分享我从[这门课](https://www.youtube.com/watch?v=M576WGiDBdQ)中学到的东西。

查看该系列的前几部分:

1.  [第一部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-1-3539606eee0e):区块链介绍【第 0 课】
2.  [第二部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-2-da6e642efdea):介绍 Solidity，Remix IDE，创建你的第一个智能合同。[第 1、2、3 课]
3.  [第三部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-3-fea146841d9a):web 3 . py 介绍。
4.  [第四部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-4-d9bb72a4a6bf):布朗尼简介。
5.  [第五部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-5-d77a8c99bfc4):区块链中的随机性。
6.  [第 6 部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-6-24e1aaa177e7):布朗尼混合&令牌标准。
7.  [第 7 部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-7-f12e4ade52da) : DeFi 协议& Aave。

*注:如果你在寻找如何投资非金融资产的建议或策略，这篇文章可能会让你失望。*

每个人都听说过 NFTs。2021 年上半年，他们开始以疯狂的价格出售。他们使许多人成为百万富翁。在本文中，我将从开发人员的角度解释 NFTs。

**什么是 NFT？**

我喜欢帕特里克 T20 的比喻，即 NFT 就像口袋妖怪。有很多，但每一个都是独一无二的。它们可以互换。每一个都有不同的属性和战斗。即使有人创造了另一个力量和技能完全相同的皮卡丘，也不会是同一个皮卡丘。创造一个精确的副本是不够的。

类似地，当有人创造了一个精确的复制品，比如说，蒙娜丽莎。他们看起来一模一样，但事实并非如此。每幅画都有不同的创作者和历史。蒙娜丽莎的真迹永远是最珍贵的。没有人会把原件换成 1 比 1 的副本。

你可以把 NFT 想象成数字艺术品。但我更喜欢用口袋妖怪来类比，因为 NFT 不仅仅是一幅图像。他们有**元数据**。这意味着你可以传递属性，如统计数据给每个 NFT。它开启了在区块链的**【元宇宙】**或**游戏中使用它们的大量可能性。**

然而，对于我这个智能合约极客来说，NFT 就是 **ERC721s 令牌**。因此，我将向您展示如何使用 Solidity、Python 和 brownie 创建 NFT。

让我们开始吧！

# 第十一课:非功能性测试

## 摘要

在这一课中，您将铸造 NFT！我们将创建一个图像和基本元数据的简约 NFT。如果您遵循该课程，您还将创建一个高级 NFT。此外，您将从之前的课程中掌握许多概念，包括[第 5 部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-5-d77a8c99bfc4)中的 **Chainlink 的 VRFConsumerBase** 以及我在[第 6 部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-6-24e1aaa177e7)中讨论的 **Open Zeppelin 的令牌标准(ERC721)** 。然而，我决定跳过本文中的高级项目。我发现如果不粘贴许多代码片段，很难解释清楚。但是你应该看看这一课，跟着帕特里克一起学。

## 经验教训

1.  **是什么让 NFTs 独一无二？**每个 ERC721 都是独一无二的。即使它们中的许多看起来相同，并附有相同的数据，它们也是不同的。为什么？因为 ERC721 标准有三个不可重复的属性。

*   **令牌 ID** :智能合约中的唯一编号，可以铸造 NFT，
*   **所有者**:拥有 NFT 的用户，
*   **令牌 URI(统一资源标识符)**:保存关于令牌的信息的标准。信息包括图像和其他属性。最重要的是，它**允许离线存储 NFT 数据**。我稍后会解释为什么将 NFT 数据添加到区块链是昂贵的。tokenURI 的一个基本示例是:

```
// tokenURI
{
  “name”: “Puppy”,
  “description”: “The most adorable puppy ever!”,
  “image”: “Image URI”, // do not confuse with token URI
  “attributes”: [{“trait_type”: “cuteness”, “value”: 99}],
}
```

2.**创建 aka 铸造 NFT**。编写一个智能契约来创建一个简单的 NFT 并不需要很长时间。

A minimal example of a Smart Contract for minting NFTs.

让我们来分解关键部分:

*   我们继承了 ERC721 标准，
*   我们在构造函数中给我们的 NFT 起**名字**“Dogie”**符号**“DOG”，
*   我们添加了`createCollectible()`函数来铸造 NFT。它调用两个 ERC721s 函数:`_safeMint()`和`_setTokenURI()`，
*   `_safeMint()`将所有者和令牌 ID 添加到我们的 NFT，
*   `_setTokenURI`添加更多数据，如名称、描述、图像和其他属性，
*   我们增加`tokenCounter`来保持它对于每个函数调用的唯一性。

这就是坚实的一面。我们只需要部署`SimpleCollectible`并调用`createCollectible()`就可以在 **OpenSea** 上看到我们的 NFT。

3.**以太坊区块链加入 NFTs 代价昂贵**。更具体地说，数据存储耗费大量的汽油。图像越大，收费越高。我们说的是几千美元。不，不是每个 NFT 都值 10 万美元。这个问题的解决方法引出了下一点。

4.**在大多数情况下，NFT 数据存储在区块链之外(链外)**。这就是为什么我们首先需要托肯·URI。但是这导致了一个主要的缺点。 **NFT 生态系统不是分散的**。如果存储您的令牌 URI 的服务器关闭，您将丢失 NFT 数据。

## 新术语

1.  **IPFS(星际文件系统)**。它是一个对等超媒体协议。由于其哈希能力，它受到区块链用户的欢迎。它允许在不运行服务器的情况下上传文件。
2.  **元数据**。正如您已经知道的，NFT 不仅仅是图像。我们可以用信息给它们添加功能，比如属性和统计。我们称之为元数据。
3.  **NFT 集市**。你可以在网站上买卖非功能性食物。它们提供了一个方便交互的 GUI。我认为 **OpenSea** 是最受欢迎的。其他还有**稀有**、**隐朋克**、**超稀有**。

## 技术

坚固，蟒蛇，布朗尼，开放齐柏林飞艇，链环，IPFS

# 最后的想法

这就是我为文章准备的全部内容。我想保持它的技术性。我还没有进入 NFTs 的投资机会。但我毫不怀疑它们不是一时的流行，而是有着巨大的潜力。

你有什么问题吗？你喜欢这种总结吗？请在评论中告诉我！

## **参考文献**

[YouTube 视频](https://www.youtube.com/watch?v=M576WGiDBdQ)

[全程 Github 回购](https://github.com/smartcontractkit/full-blockchain-solidity-course-py)

[NFT 教训 Github 回购](https://github.com/PatrickAlphaC/nft-demo)

[布朗尼 nft-mix](https://github.com/PatrickAlphaC/nft-mix)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取秘密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)