# 必须阅读关于智能合同的研究论文

> 原文：<https://medium.com/coinmonks/must-read-research-papers-on-smart-contracts-c518f72dd1e2?source=collection_archive---------25----------------------->

![](img/de58df7b7b7917110176dfab41221ffe.png)

Photo by [Tezos](https://unsplash.com/@tezos?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/smart-contracts?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

1.  **SoK: TEE 辅助的机密智能合同(arXiv)**

**作者:**[大卫加林](https://arxiv.org/search/?searchtype=author&query=Galindo%2C+D)[马克·瑞安](https://arxiv.org/search/?searchtype=author&query=Ryan%2C+M)

**摘要:**基于区块链的智能合约缺乏隐私性，因为合约状态和指令代码被公开。将智能契约执行与可信执行环境(TEEs)相结合提供了一种有效的解决方案，称为 TEE 辅助的智能契约，用于保护契约状态的机密性。然而，组合方法是多种多样的，缺乏系统的研究。新发布的系统可能无法从现有协议中吸取经验，例如重复已知的设计错误或以不安全的方式应用 TEE 技术。在这篇论文中，我们首先调查现有的系统并将其分为两类:第一层解决方案和第二层解决方案。然后，我们建立一个分析框架来捕捉它们的共同点，包括期望的属性(对于合同服务)、威胁模型和安全性考虑(对于底层系统)。基于我们的分类法，我们确定它们的理想功能，并揭示每个规范设计中挑战的根本缺陷和原因。我们相信，这项工作将为 TEE 辅助的智能合同的开发提供指导，并为评估未来 TEE 辅助的保密合同系统提供框架

**2。ScrawlD:一个标注了漏洞的真实世界以太坊智能合约数据集(**[**arXiv**](https://arxiv.org/pdf/2202.11409.pdf)**)**

**作者:**

**摘要:**以太坊上的智能合约处理数百万美元和其他金融资产。过去，攻击者利用智能合同窃取这些资产。以太坊社区开发了大量工具来检测易受攻击的智能合约。然而，没有标准化的数据集来评估这些现有的工具，或任何新开发的工具。现实世界以太坊智能合约需要一个不偏不倚的标准基准。我们已经创建了 ScrawlD:一个取自以太坊网络的真实世界智能合约的注释数据集。使用 5 种工具对数据集进行标记，这些工具使用多数投票来检测智能合同中的各种漏洞

**3。使用甲骨文和智能合同的物联网区块链架构:食品供应链的用例(**[**arXiv**](https://arxiv.org/pdf/2201.11370)**)**

**作者:**

摘要:区块链是一种分布式技术，它允许在相互交互和执行事务的不可靠用户之间建立信任。虽然区块链技术主要用于加密货币，但它已成为在物联网(IoT)领域建立信任的使能技术。然而，将区块链用于物联网会导致高延迟和大量计算能力。在本文中，我们提出了一种专用于供应链的区块链架构，该供应链包括不同的分布式物联网实体。我们为这个架构提出了一个轻量级的共识，叫做 LC4IoT。共识是通过广泛的模拟评估的。结果表明，所提出的一致性使用低的计算能力、存储能力和延迟

**4。智能合约翻译认证(**[**【arXiv】**](https://arxiv.org/pdf/2201.04919.pdf)**)**

**作者:** [Jacco O. G. Krijnen](https://arxiv.org/search/?searchtype=author&query=Krijnen%2C+J+O+G) ， [Manuel M. T. Chakravarty](https://arxiv.org/search/?searchtype=author&query=Chakravarty%2C+M+M+T) ， [Gabriele Keller](https://arxiv.org/search/?searchtype=author&query=Keller%2C+G) ， [Wouter Swierstra](https://arxiv.org/search/?searchtype=author&query=Swierstra%2C+W)

**摘要:**编译器的正确性是一个老问题，但是随着智能合同在区块链的出现，这个问题以一种新的方式出现了。智能合约是控制资产的独立软件，在敌对环境中，这些资产通常具有很高的金融价值，一旦承诺区块链，就不能再更改。智能合约通常用高级合约语言开发，并在提交给区块链之前编译成低级虚拟机代码。对于要信任区块链上给定的一段低级代码的智能合约用户，他们必须说服自己:( a)他们拥有匹配的源代码;( b)编译器忠实地翻译了源代码的语义。编译器正确性的经典方法解决了第二点。我们认为翻译认证也解决了第一个问题。我们描述了一个新颖的翻译认证框架的证明结构，该框架在 Coq 中实现，用于功能性智能契约语言。我们证明，我们可以将编译管道建模为一系列翻译关系，这有助于模块化证明方法，并且在面对不断发展的编译器实现时是健壮的。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [CBET 评论](https://coincodecap.com/cbet-casino-review) | [库科恩 vs 比特币基地](https://coincodecap.com/kucoin-vs-coinbase) | [拜比特 vs 比特币基地](https://coincodecap.com/bybit-vs-coinbase)
*   [折叠 App 回顾](https://coincodecap.com/fold-app-review) | [本地比特币回顾](/coinmonks/localbitcoins-review-6cc001c6ed56) | [Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt)
*   [加密保证金交易交易所](/coinmonks/crypto-margin-trading-exchanges-428b1f7ad108) | [赚取比特币](/coinmonks/earn-bitcoin-6e8bd3c592d9) | [Mudrex 投资](https://coincodecap.com/mudrex-invest-review-the-best-way-to-invest-in-crypto)
*   [WazirX vs CoinDCX vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [比斯勒评论](https://coincodecap.com/bitsler-review)|[WazirX vs coin switch vs coin dcx](https://coincodecap.com/wazirx-vs-coinswitch-vs-coindcx)
*   [7 大副本交易平台](https://coincodecap.com/copy-trading-platforms) | [BuyCoins 点评](https://coincodecap.com/buycoins-review)