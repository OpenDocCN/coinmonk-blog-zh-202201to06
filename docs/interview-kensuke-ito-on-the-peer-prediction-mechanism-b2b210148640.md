# 采访:伊藤健介谈同伴预测机制

> 原文：<https://medium.com/coinmonks/interview-kensuke-ito-on-the-peer-prediction-mechanism-b2b210148640?source=collection_archive---------56----------------------->

## [同行预测](https://blog.ledgerback.coop/tag/peer-prediction/)

## 在这次对话中，我与日本东京大学区块链创新捐赠主席项目研究员 Kensuke Ito 博士进行了交谈，讨论了他如何对 Web3 以及他对将对等预测机制应用于去中心化 oracles 的研究感兴趣。

![](img/86b233fe5b8ff9e73e1e5da75f43e4b0.png)

在 [*同伴预测机制*](/greyscail/peer-prediction-mechanism-9004f53a6b5d)【1】中，我( [Charles Adjovu](https://twitter.com/CAdjovu) )介绍了前述的在没有地面真相时从参与者那里引出真实信息的机制，该机制在 Web3(即区块链)及更远的应用领域，以及关于该机制的补充读物的简短列表。

在这次谈话中，我与日本东京大学区块链创新捐赠主席[的项目研究员](https://www.blockchain.t.u-tokyo.ac.jp/)[ken suke Ito](https://knskito.com/)博士进行了交谈，讨论他如何对 Web3 以及他对将对等预测机制应用于去中心化 oracles 的研究产生兴趣。

访谈记录以发言人为标题，他们的回答作为普通文本出现在下一行。

# 查尔斯·阿乔乌

你是如何对 Web3 感兴趣的？

# 伊藤健介

我是在 2015 年看了中本聪的白皮书 [*比特币:一个点对点的电子现金系统*](https://bitcoin.org/en/bitcoin-paper)【2】之后对 Web3 产生了兴趣。

我听说过“Web3”和“加密货币”，但当时我认为它们是其他学科(如计算机科学、密码学)的研究领域，与我无关。

然而，中本聪的白皮书告诉我，比特币协议，特别是其在交易记录合法性上建立共识的机制，正是基于我的主干——经济学。

从那以后，Web3 的概念对我来说突然变得很熟悉。

# 查尔斯·阿乔乌

非常酷。我认为人们开始越来越意识到一个事实，特别是随着分散金融和像区块科学这样的组织的工作，区块链是一个创造新经济系统(和模拟你在现实生活中无法合理运行的系统)的伟大环境。

# 伊藤健介

是的，我认为你完全正确。特别是从经济学的角度来看，加密经济学看起来像一个巨大的前沿，就像一个新大陆。

# 查尔斯·阿乔乌

你是如何对同辈预测机制产生兴趣的？

# 伊藤健介

在 2018 年进行文献综述后，我对同行预测机制产生了兴趣。

我对比特币协议的研究课题之一是将其分散的共识构建从区块链内部的客观信息(即交易记录)扩展到区块链外部的主观信息(如学术论文的质量)。

这个主题已经作为一个所谓的去中心化的预言被讨论过了，但是它的广泛采用仍然存在几个挑战(例如[凯恩斯选美比赛](https://en.wikipedia.org/wiki/Keynesian_beauty_contest) [4】)。

作为文献回顾的结果，我强烈地感觉到，对等预测机制将是对去中心化先知的挑战的最佳解决方案，因为它可以为报告他们对主观事物的真实信念的对等者提供最大的回报。

# 查尔斯·阿乔乌

我发现有趣的是，你的共识建立过程使用了一个基于网络的推荐者(个性化页面排名)来分配策展人，以避免与标记相关的问题。

你认为在[分散式应用](https://www.investopedia.com/terms/d/decentralized-applications-dapps.asp) (DApps) [5]中使用**桩**进行任务分配，而不是使用像你的基于网络的推荐器这样的其他方法，是不是太过强调了？

# 伊藤健介

我不这样认为，特别是因为打桩可能是任务分配的最简单的方法之一。作为 DApps 的第一步，token-staking 方案值得强调。

另一方面，随着任务内容变得更加专业化(例如，学术文章的同行评审、艺术作品的评论)，我们可能需要结合除了标桩之外的其他措施。它可能是我的研究涉及的引用图，也可能是所谓的社交图、令牌图或其他声誉得分。

换句话说，在使 DApps 更通用的过程中，我们将需要扩展任务分配中的令牌标记方案。

不用说，使用象征性的赌注来建立共识而不是分配任务仍然存在一些挑战。

# 查尔斯·阿乔乌

你介意讨论你的论文吗， [*用引用图*](http://ledgerjournal.org/ojs/ledger/article/view/182)【6】标记管理注册表？

在我介绍同伴预测机制的文章中，我把这篇论文作为阅读材料的一部分放在了补充材料中。

我非常喜欢你的论文，主要有三个原因。首先，因为它显示了发展区块链 DApp 所需的跨学科的理解。第二，您试图通过将对等预测机制应用于[令牌管理的注册中心](https://education.district0x.io/general-topics/understanding-ethereum/token-curated-registry/) (TCR) [7]，来解决分散式 oracles 无法处理主观信息的问题。最后，使用去中心化的 oracle 对学术论文进行同行评审有助于表明区块链对于激励研究人员参与开放科学实践是非常有益的。

# 伊藤健介

我的论文【6】是将对等预测机制应用于一个分布式 Oracle――令牌管理注册表的主要成果。

本文旨在将(匿名)同行的专业知识整合到分布式预言的共识构建中，不仅利用同行预测机制，还利用智力产品之间的引用关系。

建立共识的具体过程请参考以下幻灯片:[*Token-策展的带有引用图的注册表*](https://docs.google.com/presentation/d/14lY3M33xwJQAbUoMB2UboNyXhVzttctZBTZQXKnH5-I/edit?usp=sharing)【8】。

# 查尔斯·阿乔乌

我看到你最近发表了论文。你介意也讨论一下你的论文吗？

# 伊藤健介

[](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3936833)*【9】是我的博士论文，由几篇论文组成，包括 [*带有引用图的令牌管理注册表*](https://docs.google.com/presentation/d/14lY3M33xwJQAbUoMB2UboNyXhVzttctZBTZQXKnH5-I/edit?usp=sharing)【6】。*

*本论文还涵盖了对主观(和技术)信息的同行预测机制和共识建立，尽管由于与其他论文的冲突，它的故事侧重于引用关系而不是分散的预言。*

*任何人都可以获得全文，所以如果你能阅读、评论和引用我的最新成果，我会非常高兴。*

# *查尔斯·阿乔乌*

*你对区块链如何为开放科学发展新的激励机制有什么想法？*

# *伊藤健介*

*首先，我对区块链开放科学的潜力非常乐观。*

*我在 [*令牌管理的带有引用图的注册表*](https://docs.google.com/presentation/d/14lY3M33xwJQAbUoMB2UboNyXhVzttctZBTZQXKnH5-I/edit?usp=sharing) 和 [*中提出的在对等系统中就引用建立共识*](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3936833) 是区块链如何激励研究人员参与开放科学实践的明显例子。*

*此外，在与开放科学略有不同的背景下，项目 [#FREEHAWAIIPHOTO](https://www.freehawaiiphoto.com/) [9]提出了另一种方法，一旦照片作为不可替代的令牌[10】(NFTs)出售，任何人都可以获得照片(即，该项目假设照片使用越广泛，相应的 NFTs 的价值越高)。*

*这些例子说明了我们如何利用区块链来使开放获取和对创作者的奖励兼容。*

*我想首先强调的是，区块链可以成为开放科学的技术(通过平衡开放获取和对创造者的奖励)，这取决于其激励设计，尽管它经常被解释为导致数字数据被占领的技术，部分原因是最近的 NFT 热潮。*

# *查尔斯·阿乔乌*

*一样的。*

*你认为我们没有看到许多区块链和开放科学项目取得重大进展的原因之一是因为他们对为什么使用区块链缺乏理解吗？*

*或者说他们想要解决的问题不能用区块链轻易解决？*

# *伊藤健介*

*我认为两者都是。一方面，公众对区块链仍然缺乏了解，另一方面，对区块链了解很多的人似乎很难设计出创新的 DApps(可能是因为设计它们需要跨学科的知识，如计算机科学、经济学和密码学)。*

*因此，我们应该促进区块链意识和不同领域的研究人员之间的交流。*

# *感谢您阅读文章！*

*如果你有任何问题，意见或担忧，请在推特上给我发信息或发电子邮件给 ledgerback@gmail.com。*

*您可以通过以下链接在网上找到 Kensuke Ito 博士:*

*   *博客:[https://knskito.com/](https://knskito.com/)*
*   *https://twitter.com/knskito*
*   *https://scholar.google.com/citations?user=bQTxPTMAAAAJ HL = en&oi = ao*

# *参考*

1.  *莱德贝克 DCRC。“同行预测机制。” *Greyscail 区块链评论*，2020 年 12 月 25 日[https://medium . com/greys cail/peer-prediction-mechanism-9004 f 53 a6 b5d。](/greyscail/peer-prediction-mechanism-9004f53a6b5d.)*
2.  *比特币:点对点的电子现金系统。(2008)(2019 年 12 月 3 日访问)[https://bit coin:org/bit coin:pdf。](https://bitcoin:org/bitcoin:pdf.)*
3.  **区块科学*。https://www.block.science/.号于 2021 年 12 月 23 日进入。*
4.  *“凯恩斯选美大赛。”维基百科，2021 年 12 月 9 日。*维基百科*，[https://en.wikipedia.org/w/index.php?title =凯恩斯主义 _ 美容 _ 竞赛& oldid=1059457029。](https://en.wikipedia.org/w/index.php?title=Keynesian_beauty_contest&oldid=1059457029.)*
5.  *"什么是分散式应用程序？" *Investopedia* ，[https://www . Investopedia . com/terms/d/decentralized-applications-dapps . ASP .](https://www.investopedia.com/terms/d/decentralized-applications-dapps.asp.)于 2021 年 12 月 23 日访问。*
6.  *伊藤健介和田中秀幸。"带有引用图的令牌管理注册表."4 (2019): n. pag。*
7.  *"什么是令牌管理的注册表." *District0x 教育门户*，[https://Education . district 0x . io/general-topics/understanding-ether eum/token-策展-registry/。于 2021 年 12 月 23 日获取。](https://education.district0x.io/general-topics/understanding-ethereum/token-curated-registry/.)*
8.  *Ito，Kensuke,《对等系统中引用的共识构建》( 2021 年 8 月 27 日)。在 https://ssrn.com/abstract=3936833 的[或 http://dx.doi.org/10.2139/ssrn.3936833 的](https://ssrn.com/abstract=3936833)或[SSRN 有售](http://dx.doi.org/10.2139/ssrn.3936833)*
9.  *" #FREEHAWAIIPHOTO。" *#FREEHAWAIIPHOTO* ，[https://www.freehawaiiphoto.com。](https://www.freehawaiiphoto.com.)于 2021 年 12 月 23 日访问。*
10.  *"不可替换的令牌(NFT). " *Investopedia* ，[https://www . Investopedia . com/non-functionable-tokens-NFT-5115211。](https://www.investopedia.com/non-fungible-tokens-nft-5115211.)于 2021 年 12 月 23 日访问。*

**原载于 2021 年 12 月 24 日*[*https://blog . ledger back . coop*](https://blog.ledgerback.coop/interview-kensuke-ito-on-the-peer-prediction-mechanism/)*。**

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)*
*   *[莱杰 vs Ngrave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)*
*   *[Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)*
*   *[3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)*
*   *最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)*