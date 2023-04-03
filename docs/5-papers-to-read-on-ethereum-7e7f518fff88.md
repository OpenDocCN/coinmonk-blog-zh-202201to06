# 以太坊上要读的 5 篇论文

> 原文：<https://medium.com/coinmonks/5-papers-to-read-on-ethereum-7e7f518fff88?source=collection_archive---------73----------------------->

![](img/369f773d57d7cd4b2e7ba351008c97b4.png)

Photo by [Kanchanara](https://unsplash.com/@kanchanara?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/ethereum?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

1.  **智能电网私有以太坊区块链网络的有效框架(**[**arXiv**](https://arxiv.org/pdf/2203.12435.pdf)**)**

**作者:** [Do Hai Son](https://arxiv.org/search/?searchtype=author&query=Son%2C+D+H) ， [Tran Thi Thuy Quynh](https://arxiv.org/search/?searchtype=author&query=Quynh%2C+T+T+T) ， [Tran Viet Khoa](https://arxiv.org/search/?searchtype=author&query=Khoa%2C+T+V) ， [Dinh Thai Hoang](https://arxiv.org/search/?searchtype=author&query=Hoang%2C+D+T) ， [Nguyen Linh Trung](https://arxiv.org/search/?searchtype=author&query=Trung%2C+N+L) ， [Nguyen Viet Ha](https://arxiv.org/search/?searchtype=author&query=Ha%2C+N+V) ， [Dusit Niyato](https://arxiv.org/search/?searchtype=author&query=Niyato%2C+D) ， [Nguyen N. Diep](https://arxiv.org/search/?searchtype=author&query=Diep%2C+N+N) ， [Eryk](https://arxiv.org/search/?searchtype=author&query=Dutkiewicz%2C+E)

**摘要:**智能电网是工业 4.0 中的一项重要应用，有很多新技术和设备协同工作。因此，存储在智能电网中的敏感数据很容易被恶意修改和窃取。本文提出了一个基于高效私有以太网的智能电网框架。我们的框架提供了一个真正的智能电网，包括现代硬件和智能合同，以保护区块链网络中的数据。为了获得高吞吐量但低叔叔率，以太坊共识机制的挖掘过程中使用的难度计算方法被修改以适应实际的智能电网设置。通过仿真评估了吞吐量和延迟方面的性能，并通过真实的智能电网设置进行了验证。基于以太坊的增强型智能电网比公共电网具有更好的性能。此外，该框架可以应用于任何用于在以太网中存储数据的系统。

**2。有状态到无状态:建模无状态以太坊(**[**arXiv**](https://arxiv.org/pdf/2203.12435.pdf)**)**

**作者:** [桑德拉·约翰逊](https://arxiv.org/search/?searchtype=author&query=Johnson%2C+S)，[大卫·海兰-伍德](https://arxiv.org/search/?searchtype=author&query=Hyland-Wood%2C+D)，[安德斯·L·麦德森](https://arxiv.org/search/?searchtype=author&query=Madsen%2C+A+L)，[凯丽·门格尔森](https://arxiv.org/search/?searchtype=author&query=Mengersen%2C+K)

**摘要:**“无状态以太坊”的概念是以减缓以太坊的无界状态增长为主要目标而构思的。无状态以太坊的主要推动者是通过将“见证人”引入生态系统。需要识别和分析这些额外数据包对网络造成的变化和潜在后果，以确保以太坊生态系统能够继续安全高效地运行。在本文中，我们提出了一个贝叶斯网络模型，一种概率图形建模方法，以捕捉以太网(公共以太坊区块链)中的关键因素及其相互作用，重点关注无状态以太坊引入的变化，以评估由此产生的以太坊生态系统的健康状况。在数据不可用的情况下，我们使用经验数据和专家知识的混合来量化模型。基于建模时可用的数据和专家知识，以太坊生态系统有望在引入无状态以太坊后保持健康。

**3。以太坊智能合约中的特征交易还原语句(**[**arXiv**](https://arxiv.org/pdf/2108.10799.pdf)**)**

**作者:**，[李丽丽](https://arxiv.org/search/?searchtype=author&query=Wei%2C+L)，[吴起](https://arxiv.org/search/?searchtype=author&query=Zhang%2C+W)，[张](https://arxiv.org/search/?searchtype=author&query=Wen%2C+M)，[刘叶胖](https://arxiv.org/search/?searchtype=author&query=Liu%2C+Y)，[张成志](https://arxiv.org/search/?searchtype=author&query=Cheung%2C+S)

**摘要:**智能合约是运行在区块链上执行交易的程序。当在运行时违反输入约束或安全属性时，需要恢复智能合约正在执行的事务，以避免不良后果。在支持智能合约的最受欢迎的区块链 Ethereum 上，开发人员可以在三种事务恢复语句(即 require、if…revert 和 if…throw)中选择一种来处理异常事务。虽然这些事务恢复语句对于防止智能合约表现出异常行为或遭受恶意攻击至关重要，但人们对它们在实践中的使用方式了解有限。在这项工作中，我们进行了第一次实证研究，以表征以太坊智能合约中的交易回复声明。我们测量了来自流行 dapps 的 3，866 个经过验证的智能合同中这些语句的流行程度，并通过手动分析 557 个交易恢复语句建立了它们目的的分类。我们还比较了模板契约和它们对应的定制契约，以理解开发人员如何定制事务恢复语句的使用。最后，我们通过从智能契约中删除事务恢复语句，并将变异后的契约与原始契约进行比较，来分析事务恢复语句的安全影响。我们的研究带来了重要的发现，可以为智能合同质量保证的广泛领域的进一步研究提供启示，并为智能合同开发人员提供关于正确使用交易恢复语句的实用指导

**4。以太坊智能合约安全漏洞综述(**[**arXiv**](https://arxiv.org/pdf/2105.06974.pdf)**)**

**作者:** [诺玛·法蒂玛·萨姆林](https://arxiv.org/search/?searchtype=author&query=Samreen%2C+N+F)，[马纳尔·h·阿拉菲](https://arxiv.org/search/?searchtype=author&query=Alalfi%2C+M+H)

**摘要:**基于区块链技术(BT)的以太坊智能合约(Ethereum Smart Contracts)实现了独立于中央授权机构的区块链网络上的对等方之间的货币交易。以太坊智能合约是作为分散应用程序部署的程序，具有区块链共识协议的构件。这使得消费者能够在透明和无冲突的环境中达成协议。然而，在这些智能合约中存在一些安全漏洞，这些安全漏洞对应用程序及其消费者是潜在的威胁，并且在过去已经表明会造成巨大的经济损失。在这项研究中，我们回顾了现有的文献，并大致分类的 BT 应用。由于以太坊智能合约主要应用于电子商务应用，我们认为这些应用更容易受到攻击。在这些智能合约中，我们主要关注于识别智能合约的程序员和用户必须避免的漏洞。本文旨在通过分析这些安全漏洞过去被利用的案例来解释特定于 BT 应用层的八个漏洞。我们还回顾了一些可用的工具和应用程序，从它们的方法和有效性方面检测这些漏洞。我们还调查了用于识别这些安全漏洞的检测工具的可用性，以及缺乏这些工具来识别其中一些漏洞的情况

**5。以太坊智能合约中的可重入漏洞识别(**[**arXiv**](https://arxiv.org/pdf/2105.02881.pdf)**)**

**作者:** [诺玛·法蒂玛·萨姆林](https://arxiv.org/search/?searchtype=author&query=Samreen%2C+N+F)，[马纳尔·h·阿拉尔菲](https://arxiv.org/search/?searchtype=author&query=Alalfi%2C+M+H)

**摘要:**以太坊智能合约使用区块链在没有中央代理的网络上的对等体之间转移价值。这些程序部署在运行于区块链共识协议之上的分散式应用程序上，使人们能够在透明和无冲突的环境中达成协议。这些智能合约中的安全漏洞是应用程序的潜在威胁，并给用户造成了巨大的经济损失。在本文中，我们提出了一个结合静态和动态分析的框架来检测以太坊智能合约中的可重入性漏洞。该框架基于受测智能合约的 ABI 规范生成攻击者合约，并分析合约交互以准确报告重入漏洞。我们在来自 Etherscan 的 5 个修改的智能契约上对我们提出的框架进行了初步评估，我们的框架能够检测我们所有修改的契约中的可重入性漏洞。我们的框架静态地分析智能契约来识别潜在的易受攻击的函数，然后使用动态分析来精确地确认可重入性漏洞，从而实现提高的性能和减少的误报。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [德国最佳加密交易所](https://coincodecap.com/crypto-exchanges-in-germany) | [Arbitrum:第二层解决方案](https://coincodecap.com/arbitrum)
*   [币安交易机器人](/coinmonks/binance-trading-bots-d0d57bb62c4c) | [OKEx 评论](/coinmonks/okex-review-6b369304110f) | [Atani 评论](https://coincodecap.com/atani-review)
*   [最佳加密交易信号电报](/coinmonks/best-crypto-signals-telegram-5785cdbc4b2b) | [MoonXBT 评论](/coinmonks/moonxbt-review-6e4ab26d037)
*   如何在 Bitbns 上购买柴犬(SHIB)币？ | [买弗洛基](https://coincodecap.com/buy-floki-inu-token)
*   [CoinFLEX 评论](https://coincodecap.com/coinflex-review) | [AEX 交易所评论](https://coincodecap.com/aex-exchange-review) | [UPbit 评论](https://coincodecap.com/upbit-review)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)