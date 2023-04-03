# 构建您的首个 DeFi 应用——我的经验

> 原文：<https://medium.com/coinmonks/build-your-first-defi-application-my-experience-34e8de59b19a?source=collection_archive---------19----------------------->

![](img/1221448b032b3c4014d50afdb8e45409.png)

Photo by [Tezos](https://unsplash.com/@tezos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我知道，我们知道你在某个时候听说过**分散式金融(DeFi)** ，我在这里谈谈它的意义以及我学习和构建 **DEX(分散式交易所)**的经验。

# 什么是分权金融？

> DeFi 是一个金融产品和服务的统称，任何可以使用以太坊的人都可以使用，只要有互联网连接

这个意思来自以太坊的官方页面，可以查看更多细节[这里](https://ethereum.org/en/defi/#what-is-defi)。

但简单来说，DeFi 是一种金融产品，你可以在不需要中间人(在这种情况下是银行)的情况下获得，给你对你的钱的控制和可见性。

上面的定义提到，任何人都可以使用以太坊，但这个概念是为了让所有能够运行智能合同(或 Solana 上的程序)的连锁店实现这一点。

你可以从基本用法中得到的一些例子是**交易或借出/借入**你的资产以获得一些利益。

现在在市场上，你可以看到许多或多或少做同样事情的 DeFi 应用程序，其中一些非常受欢迎和成功( [Uniswap](https://uniswap.org/) 、 [Compound](https://compound.finance/) )，其他的是最受欢迎的应用程序的简单拷贝，但是我要告诉你我从 0 开始构建和部署一个示例项目的经验，该项目能够用 ETH 交换一些 SCHY，我自己的令牌。

# 走进这个加密的世界

在我看来，我认为 2021 年是我听到和看到很多关于任何与加密相关的信息的一年，特别是与 NFTs 相关的“成功”故事，所以我说，**我也想这样！**

一开始，我想做正确的事情，而不是陷入绝望，在学习过程中做出错误的举动或投资，因为是的，99%的可能性是你会投资购买一些加密货币，以了解这个世界的真实运作方式，这是了解基础知识的过程的一部分，这是我的第一个建议**从基础知识开始**， 不要直接进入如何开发 dApps(去中心化应用程序)或创建 NFT 集合，因为你将面临许多更难学习和理解的术语和概念，而是继续了解什么是区块链、交易、密码学、比特币的历史及其用途、智能合约等。 我提到了 5 个主题来开始，还有很多，所以慢慢开始，理解每一部分。

有很多信息和课程可以理解这些主题，所以我会向你推荐这些 Youtube 频道，从基本主题开始，但如果你自己做研究来培养你的好奇心和兴趣，会更好。

*   [白板加密](https://www.youtube.com/c/WhiteboardCrypto)
*   [西班牙语 BTC](https://www.youtube.com/c/btcenespanol)

现在，您已经阅读、学习、实验并理解了关于区块链和加密货币的基本但重要的主题，也仍然有兴趣了解如何进入开发部分，让我们看看是关于什么的。

# 我采取的路线图

要开始构建您的第一个 DeFi 应用程序，需要记住这一点，如果您有编程语言(Javascript、Python)的经验，将更容易开始，与学习 Solidity 作为您的第一个编程语言相比，更推荐学习其他编程语言的知识。

这包括两个要构建的重要部分:

*   前端应用程序
*   智能合同

[**Solidity**](https://docs.soliditylang.org/en/v0.8.13/) 是一种面向对象的高级语言，用于实现智能合约。它旨在针对以太坊虚拟机，例如，如果你想建立一个智能合同的[多边形](https://polygon.technology/)链将是兼容的。

开始学习 solidity 的一个很好的起点是玩这个名为 [Crypto Zombies](https://cryptozombies.io/) 的游戏，它教你编写智能合同并获得更高级的主题来实现。另外，如果你想编写和测试你自己的智能合约，你可以使用一个在线 IDE 来编写和部署智能合约并与之交互。

您需要知道的一个重要部分是关于框架，这些框架可在您最喜欢的代码编辑器(例如 VSCode)中使用，以在您的本地上构建、测试和部署您的智能合约。

在这篇文章中，我们有两个流行的选择:

*   [松露](https://trufflesuite.com/truffle/)
*   [安全帽](https://hardhat.org/)

此外，了解一下 [Open Zeppelin](https://www.openzeppelin.com/contracts) 为 ERC20(可替代令牌)或 ERC721(不可替代令牌)等智能合约展示的标准也很不错。

既然您已经学习、测试和部署了，现在是时候在 [ethers.js](https://docs.ethers.io/v5/) (或 [web3.js](https://web3js.readthedocs.io/en/v1.7.3/) )的帮助下用我们的智能合约连接前端了，这些库帮助我们与智能合约进行交互(读取数据、调用函数等)。ethers.js 和 web3.js 非常相似，但是它们在实现以及如何在应用程序中使用它方面有所不同。

这些是你开始开发完整的 dapp 需要知道的必要工具，在这种情况下，将留下一个基本的 DeFi 应用程序的示例项目，仅用于使用前面提到的工具购买/出售你自己的令牌。

[](https://github.com/santychuy/santychuy-crypto-exchange) [## GitHub-santy chuy/santy chuy-crypto-Exchange:分散交换示例

### DeFi 项目来玩它，简单但完整的项目来处理必要的概念，以处理智能合同…

github.com](https://github.com/santychuy/santychuy-crypto-exchange) 

# 最后的想法

自从我开始认真学习、试验和构建与区块链相关的应用程序以来，已经有 6 个月了，我认为我们正处于开始学习这些技术的最佳时机，因为我们开始看到有用的用例，例如在财务方面，它们已经产生了重要的影响，并且还有很多公司在寻找能够管理这些技术的开发人员，所以我将继续学习新的东西，掌握我已经知道的知识，继续分享 mi 流程，因为所有这些都将留下来！