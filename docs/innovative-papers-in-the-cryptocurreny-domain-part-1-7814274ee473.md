# 加密货币领域的创新论文第一部分

> 原文：<https://medium.com/coinmonks/innovative-papers-in-the-cryptocurreny-domain-part-1-7814274ee473?source=collection_archive---------62----------------------->

![](img/9d16ae3a23bb02f10332d0a6252c8652.png)

Photo by [Milad Fakurian](https://unsplash.com/@fakurian?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cryptocurrency?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

1.  **GitHub 中区块链仓库的实证研究(**[**arXiv**](https://arxiv.org/pdf/2205.08087)**)**

**作者:** [Ajoy Das](https://arxiv.org/search/?searchtype=author&query=Das%2C+A) ， [Gias Uddin](https://arxiv.org/search/?searchtype=author&query=Uddin%2C+G) ， [Guenther Ruhe](https://arxiv.org/search/?searchtype=author&query=Ruhe%2C+G)

**摘要:**区块链是一种分布式账本技术，保证交易的可追溯性。区块链被应用于多个领域，如金融(如加密货币)、医疗保健、安全和供应链。在开源软件(OSS)门户 GitHub 中，我们观察到基于区块链的解决方案越来越多地被采用。鉴于基于区块链的解决方案在我们日常生活中的快速出现和不断发展的加密货币市场，了解现状、开发人员通常如何在这些回购中进行互动以及他们在应用代码更改方面有多大的自由度非常重要。我们报告了对 GitHub 的 3，664 个区块链软件库的实证研究。我们将区块链存储库分为两类:工具(例如，SDK)和应用(例如，使用 SDK 开发的服务/解决方案)。应用程序类别进一步分为两个子类别:加密和非加密应用程序。在所有区块链存储库类别中，提交上的贡献交互是最常见的交互类型。我们发现，为区块链回购做出贡献的组织比个人用户更多。工具中的内部和外部用户数量的中位数高于应用程序 repos。我们观察到区块链工具中的用户比应用程序 repos 中的用户有更高程度的协作(例如，维护工作)。在工件中，问题比提交和拉请求有更多的交互。关于自治，我们发现不到一半的项目贡献是自治的。我们的发现为区块链利益相关者提供了启示，如开发人员要了解围绕区块链软件的 OSS 实践

**2。估计补丁跨(区块链)叉的传播次数(**[**arXiv**](https://arxiv.org/pdf/2205.07478)**)**

**作者:** [塞巴斯蒂安·安德列娜](https://arxiv.org/search/?searchtype=author&query=Andreina%2C+S)，[洛伦佐·阿尔米尼奥](https://arxiv.org/search/?searchtype=author&query=Alluminio%2C+L)，[乔尔吉亚·阿祖拉·马森](https://arxiv.org/search/?searchtype=author&query=Marson%2C+G+A)，[加桑·卡拉姆](https://arxiv.org/search/?searchtype=author&query=Karame%2C+G)

**摘要:**比特币的广泛成功导致了替代加密货币(altcoins)的巨大激增。大多数 altcoins 本质上是对比特币的代码进行微小的修改，如要铸造的硬币数量、块大小和块生成时间。因此，它们通常被认为在安全性、稳健性和成熟度方面与比特币相同。在本文中，我们表明，这一共同的概念是误导。通过挖掘从各种替代硬币项目的 GitHub 存储库中检索的数据，我们估计了将相关补丁从比特币传播到替代硬币所需的时间。我们发现，虽然比特币开发社区在修复比特币代码库的安全缺陷方面相当活跃，但分叉加密货币在修补相同的漏洞(继承自比特币)方面并不严格。在某些情况下，我们观察到，即使是在比特币社区中发现并修复的关键漏洞，也在披露几个月后被替代币解决了。除了提高对这一问题的认识，我们的工作旨在激发在公开报告漏洞之前对所有分叉链进行适当负责任的披露的需求

**3。使用顺序训练的多对一 lst ms(**[**arXiv**](https://arxiv.org/pdf/2205.04678)**)**对金融市场中的时间序列进行实时预测

**作者:**

**摘要:**金融市场高度复杂多变；因此，为了进行预测而了解这些市场，对于对崩盘和随后的复苏发出早期警报至关重要。人们一直在使用金融数学和机器学习等不同领域的学习工具，试图对这类市场做出可信的预测。然而，在开发出人工神经网络(ANN)框架之前，这种技术的精确度还不够。此外，对金融时间序列进行准确的实时预测对于所使用的 ANN 结构和训练它的过程来说是高度主观的。长短期记忆(LSTM)是递归神经网络家族的一员，已被广泛用于时间序列预测。特别地，我们用先前数据的已知长度，比如 T 个时间步，训练两个 LSTMs，并且只预测一个时间步。在每次迭代中，当一个 LSTM 被用来寻找最佳的时期数时，第二个 LSTM 仅被训练用于最佳的时期数以进行预测。我们将当前预测视为下一个预测的训练集中的预测，并训练相同的 LSTM。虽然当预测在测试阶段进行得更远时，传统的训练方法会导致更多的误差，但是当训练在测试阶段进行时随着训练的增加，我们的方法能够保持较高的准确性。我们的方法的预测精度使用三个不同金融市场的三个时间序列进行验证:股票、加密货币和商品。将结果与扩展卡尔曼滤波器、自回归模型和自回归综合移动平均模型的结果进行了比较

**4。一种高效、可移植、平台无关的物联网设备加密货币挖掘算法的实现(**[**arXiv**](https://arxiv.org/pdf/2205.01646)**)**

**作者:** [金舒克·杜瓦](https://arxiv.org/search/?searchtype=author&query=Dua%2C+K)

**摘要:**最近，区块链和物联网(IoT)领域都有大量研究。区块链技术与物联网很好地协同作用，解决了隐私、互操作性和安全性等关键问题。然而，允许不信任方维护协议的共识机制，以及支撑加密货币挖掘的相同算法，通常计算成本极高，使得在低功耗物联网设备上实施非常困难。更重要的是，挖掘需要下载和同步数百千兆字节的数据块，这远远超出了大多数物联网设备的能力。本文提出了一种高效、可移植、平台无关的加密货币挖掘算法，该算法使用 Stratum 协议来避免下载整个区块链。我们在四个不同的平台上实现了该算法——PC、ESP32、仿真器和旧的 PlayStation Portable (PSP ),以证明任何设备都有可能在没有任何假设的情况下挖掘加密货币，除了连接到互联网的能力。为了确保在任何平台上的可移植性和所报告结果的可再现性，我们在 https://anonymous.4open.science/r/cryptominer.[的](https://anonymous.4open.science/r/cryptominer.)公开了具体的实施说明

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [CBET 评论](https://coincodecap.com/cbet-casino-review) | [库科恩 vs 比特币基地](https://coincodecap.com/kucoin-vs-coinbase) | [拜比特 vs 比特币基地](https://coincodecap.com/bybit-vs-coinbase)
*   [折叠 App 回顾](https://coincodecap.com/fold-app-review) | [本地比特币回顾](/coinmonks/localbitcoins-review-6cc001c6ed56) | [Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt)
*   [加密保证金交易交易所](/coinmonks/crypto-margin-trading-exchanges-428b1f7ad108) | [赚取比特币](/coinmonks/earn-bitcoin-6e8bd3c592d9) | [Mudrex 投资](https://coincodecap.com/mudrex-invest-review-the-best-way-to-invest-in-crypto)
*   [WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [比斯勒评论](https://coincodecap.com/bitsler-review)|[WazirX vs coin switch vs coin dcx](https://coincodecap.com/wazirx-vs-coinswitch-vs-coindcx)
*   [7 大副本交易平台](https://coincodecap.com/copy-trading-platforms) | [BuyCoins 点评](https://coincodecap.com/buycoins-review)