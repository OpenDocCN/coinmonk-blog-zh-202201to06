# FreeCodeCamp 的可靠性、区块链、智能合约初级到专家课程总结，第 6 部分

> 原文：<https://medium.com/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-6-24e1aaa177e7?source=collection_archive---------14----------------------->

让我们**烘焙核仁巧克力饼项目**！

![](img/2b8cf550839e08ba0196a94446b87a07.png)

[Patrick Collins](/@patrick.collins_58673); the Author of the Course

欢迎来到我总结的第 6 部分！我很高兴你在这里。我写这些文章来分享我从[这门课](https://www.youtube.com/watch?v=M576WGiDBdQ)中学到的东西。

查看该系列的前几部分:

1.  [第一部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-1-3539606eee0e):区块链介绍【第 0 课】
2.  第二部分:介绍 Solidity，混合 IDE，创建你的第一个智能合同。[第 1、2、3 课]
3.  [第三部分](https://kris-ograbek.medium.com/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-3-fea146841d9a):web 3 . py 简介。
4.  [第四部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-4-d9bb72a4a6bf):布朗尼简介。
5.  [第五部分](/coinmonks/freecodecamps-solidity-blockchain-smart-contracts-beginner-to-expert-course-summary-part-5-d77a8c99bfc4):区块链中的随机性。

对于这一部分，我准备了两节课的总结。没有很多编码，但是 Patrick 给出了实用的技巧。首先，你将学习如何启动核仁巧克力饼项目。然后，您将创建自己的令牌并将其部署到区块链中。多酷啊。你可以把你的姓名牌放在你的钱包里！

让我们开始吧！

# 第 8 课:链环组合

**总结**

这是一个 2 分钟的课程，你将学习如何在布朗尼样板。他们允许你启动你的项目。

**经验教训**

1.  用布朗尼混合物创建一个新项目。Brownie 项目具有相同的文件夹结构。此外，每个项目都有许多相同的文件。所以如果你已经用布朗尼开发过，你通常会复制粘贴很多东西。如果有模板来跳过复制粘贴的部分不是很好吗？当然，会的！这也是为什么核仁巧克力饼混合物存在的原因。您会发现有一长串您可以克隆的实用存储库。但是克隆对于核仁巧克力饼的开发者来说听起来不够酷。使用布朗尼，你就在**烘焙**新项目。例如:

```
$ brownie bake dao-mix
```

一些有趣的模板:

*   **dao-mix** :与**Dao(去中心化自治组织)**合作建立的回购，
*   **token-mix** :用 Solidity 编写的 **ERC-20** 模板的回购，
*   **nft-mix** :一个使用 **NFTs** 智能合约的回购协议。

2.**使用 chainlink-mix 启动新项目**。如果你读过我以前的文章，你就对 Chainlink 及其用例有了基本的了解。通常，我们使用 Chainlink 生成**随机数**或检查当前**价格馈送**，例如 ETH/USD。然而，建立一个项目是一个漫长的过程。幸运的是，你已经知道怎么做可以节省很多时间。你**烤**链环-mix！

```
$ brownie bake chainlink-mix
```

它将生成:

*   可靠性合约，包括*价格反馈消费者*(价格反馈)和*vrf 消费者*(随机性)，
*   *brownie-config.yaml* 带 keyhashes 和有用地址，
*   Python 脚本来部署合同，
*   测试，
*   还有更多！

试试看！

**新术语**

1.  核仁巧克力饼混合物。
2.  **链环组合。**

**技术**

坚实，布朗尼，链环混合。

# 第 9 课:ERC-20、EIP 和令牌标准

**总结**

在本课中，您将铸造自己的代币！你可以选择它的名字和数量！你只需要几行代码。

**经验教训**

1.  **ERC-20 代币**。ERC-20 是部署在区块链上的令牌。它们是具有共同规则和功能的智能合约。从技术上讲，它们既是智能合约，也是代币。你可以用 ERC-20:

*   作为治理令牌，
*   为了保护底层网络，
*   创造一个人造资产。

2.**令牌标准**。还有许多其他标准，如:

*   **ERC-721** 又名 **NFT(不可替代代币)**。NFTs 与 ERC-20s 的不同之处在于以下属性: **tokenId** 、**所有者**、 **tokenURI** 。它们的组合使得每个 ERC-721 令牌都是独一无二的。每一架 ERC-721 都有一段独特的历史，即创造者和拥有者的历史。
*   **ERC-1155** 又名**半替代代币**。
*   其他 ERC-20 的“孩子”。它们是 ERC-20s 的改进型，用于特定的应用场合。例如，链接令牌实现了 **ERC-677 标准**。它在 ERC-20 功能的基础上添加了 *transferAndCall()* 函数。

3.**铸造自己的代币**。造币就是添加到一个区块链。多亏了开放的 Zeppelin 库，创建 ERC-20 令牌变得很容易。

Smart Contract for minting the KrisToken

当您添加一个小脚本来部署合同时，您将能够在区块链上找到您的令牌。

Python script to deploy MyToken Contract

就是这样！KrisToken 现在是区块链的一部分！

**新术语**

1.  **ERC-20s 等令牌标准**。

**技术**

坚固，布朗尼，开放齐柏林飞艇。

# 最后的想法

今天到此为止。从 15 分钟的视频开始，我写了这篇文章。帕特里克的课程包含了如此多的知识！

推荐看下面我贴的视频。他们帮助我理解什么是代币。

你有什么问题吗？你喜欢这种总结吗？请在评论中告诉我！

**参考文献**

[YouTube 视频](https://www.youtube.com/watch?v=M576WGiDBdQ)

[GitHub 回购](https://github.com/smartcontractkit/full-blockchain-solidity-course-py)

[硬币 vs 代币白板加密 YouTube](https://www.youtube.com/watch?v=422HORNUfkU)

[什么是包裹代币？白板加密 YouTube](https://www.youtube.com/watch?v=DuwQ6NuPQp4)

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [3 commas Review](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92)|[Pionex Review](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot)|[coin rule Review](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange Review](/coinmonks/bybit-exchange-review-dbd570019b71)|[bit 亚德 Review](https://coincodecap.com/bityard-reivew)|[Jet-Bot Review](https://coincodecap.com/jet-bot-review)
*   [3 commas vs Cryptohopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取密码利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最佳比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [比特币 02 点评](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)