# Stablecoin 初级读本第 3 部分— Stablecoin 类型

> 原文：<https://medium.com/coinmonks/stablecoin-primer-section-3-stablecoin-types-c416ce5f455f?source=collection_archive---------4----------------------->

# 有人说中央银行在区块链吗？

本文是 Stablecoin 初级读本系列的一部分。如果你有兴趣阅读其他文章， [*看看这个帖子*](https://namsso.medium.com/stablecoin-primer-intro-54689d6fcdba) *。*

![](img/e3b8b5076fd954a6f292ebdcc7056185.png)

Types of stablecoins by [diedamlas](https://www.instagram.com/diedamlas/)

区块链上的中央银行实际上是算法稳定计算中使用最广泛的类比之一，但稍后会有更多的介绍。

## 两种心智模式

在我们开始讨论不同类型的 stablecoins 之前，我想先做一个说明，希望能让本书和本书接下来的章节更容易理解。

到目前为止，在[简介](/coinmonks/stablecoin-primer-intro-54689d6fcdba)、[第 1 节](/coinmonks/stablecoin-primer-section-1-path-to-stablecoins-8bcdb39c73e1)和[第 2 节](/coinmonks/stablecoin-primer-section-2-stablecoin-landscape-132b27f7f2d3)中，我们讨论了稳定积分的消费级价值主张和用途，例如使用稳定积分进行跨境汇款。这些都很简单。然而，稳定硬币的概念听起来可能很简单，但这些稳定硬币背后的协议和机制可能非常复杂，需要对经济学和区块链有一定程度的了解。这仍然是一个初级读本，所以我的意图是尽可能保持内容的介绍性，但我们确实需要为一些复杂性做好准备。

为了让你对本节和第 4 节的内容有所准备，我将提出两个心理模型:

*   **两种不同类型的稳定币用户**:消费者和 DeFi 参与者(DeFi =分散金融)。一个**消费者**就是那些只想购买和持有稳定的商品的人。例如，一个人只使用稳定的货币将他的工资转换成戴或来存美元，他可以被认为是一个消费者。消费者通常只通过二级市场与 stablecoins 进行互动，例如使用从法定到加密的交易所来购买/出售 stablecoins。如果您是消费者，并且不一定对 stablecoin 背后的系统感兴趣，那么您不必担心 stable coin 协议的复杂性——请随意浏览第 5 部分。另一方面， **DeFi 参与者**利用 stablecoin 协议铸造(创建)stable coin 并参与各种 DeFi 活动，如[产量农业](https://blockworks.co/what-is-yield-farming-what-you-need-to-know/#:~:text=Yield%20farmers%20generally%20use%20decentralized,between%20two%20or%20more%20parties.)。一系列的团体可以算作 DeFi 参与者，包括但不限于交易商、机构、密码交易所和 Dao。理解 DeFi 参与者如何与 stablecoin 协议相互作用至关重要，因为没有它们，stable coin 就不存在。如果你是 DeFi 的参与者，或者对 stablecoins 的具体细节感兴趣，这一部分可能对你有用。尽情享受吧！
*   Stablecoin 协议就像运行在代码上的金融机构:就像我说的，stablecoin 协议很复杂。我认为一种有帮助的和过于简化的思考方式是这样的:稳定币协议，尤其是分散式的，就像银行对代码(即区块链)进行操作，令牌对这些协议如何操作至关重要。这听起来可能很简单，但如果你没有金融背景，或者对金融机构的内部运作不感兴趣，你可能不会太直观地了解银行是如何运作的。由于区块链和代币，在此基础上又增加了一层复杂性。这就是为什么我认为开始时期望一些复杂性是有帮助的。

![](img/a4a18e5a916110680f203f501004dce1.png)

Two different stablecoin users and a stablecoin protocol by [diedamlas](https://www.instagram.com/diedamlas/)

记住这些心智模型，让我们来谈谈设计一个成功的 stablecoin 的一般原则。

## 设计原则

不幸的是，目前还没有一本剧本明确阐述如何设计成功的 stablecoin。stablecoin 景观仍然是一个狂野的西部，各种实验选择独特的机制来实现稳定。然而，回顾整体情况，我们可以观察到一种模式，其中每个项目都针对一组公共参数进行优化，并针对其他参数进行权衡，这些构成了 stablecoins 的设计原则。

第一个，也许是最重要的参数是**稳定性**。这是指稳定币的价格在其价格目标(例如 1 美元)附近具有最小方差。为稳定而优化的稳定币通常选择有一个抵押品或储备机制来支持稳定币。这意味着稳定的硬币只是代表发行者储备中抵押品的借据。在储备机制下，稳定硬币的供应取决于支持它们的抵押品数量，因为稳定硬币只能在系统收到抵押品存款后才能铸造。这防止了稳定硬币发行者随意增加稳定硬币的供应量，从而导致稳定硬币价格的不稳定。

stablecoins 优化的第二个设计原则是**去中心化**，这是指 stablecoin 协议由多方管理，没有单点故障。稳定币越分散，就越能抵制审查，因为分散阻止了任何一方控制稳定币的许可。这对于那些货币管制和审查严格的国家的公民来说尤其重要，在这些国家，获取外汇并不容易——还记得[第二章](https://namsso.medium.com/stablecoin-primer-section-2-stablecoin-landscape-132b27f7f2d3)中的例子吗。去中心化的另一个好处是，它使一个协议的货币政策对其参与者更加透明。例如，在算法稳定的情况下，协议产生的[铸币税](https://www.investopedia.com/terms/s/seigniorage.asp)利润的数量对其参与者来说在任何时候都是可见的。这在建立信任和扩大稳定的社区网络方面起着关键作用。

从不同的 stablecoin 实验中得出的最后一个设计参数是**资本效率**，它指的是协议允许用户如何有效地利用他们的资本。依赖于其他加密货币支持的稳定货币经常被过度抵押。这意味着，为了创造(铸造)新的稳定硬币，用户必须存入一定数量的抵押品(例如，乙醚),其价值高于他们作为回报收到的稳定硬币。例如，用户存入价值 200 美元的乙醚来铸造价值 100 美元的稳定可卡因。通过要求超额抵押，这些协议保护他们的稳定货币免受支持加密货币向下波动的影响。然而，这导致了[更昂贵的](https://twitter.com/samkazemian/status/1380022652560023556?s=20&t=lfrruTwjI0_FnSRFoGGMfw)借贷和 DeFi 中的贷款，因此协议需要在他们的抵押品要求和资本效率之间取得平衡。

![](img/0550a2f4c630002a280aca5999db0f94.png)

Overly-simplified stablecoin mission control deck by [diedamlas](https://www.instagram.com/diedamlas/)

那么，为什么我们需要这些设计原则来进一步复杂化我们的生活呢？这些设计原则的目标不是对不同的 stablecoin 项目进行相互比较，而是回顾整体情况并解释 stable coin 及其背后的机制是如何随着时间的推移而演变的。最终，新项目通过找出旧项目机制中的差距，建立在旧项目的基础上。

透过这些设计原则的镜头，我们可以看到，迄今为止已经出现了三种类型的 stablecoins:**(1)**【fiat-backed stable coins】、**、**【crypto-backed stable coins】、**、**算法 stable coins。

![](img/3d12ed0895f51e4271a9b65e312eb4d3.png)

Total market cap of stablecoins currently stands at+$186 billion. Source: [CoinMarketCap](https://coinmarketcap.com/view/stablecoin/)

让我们用我们的设计原则双击每个 stablecoin 类型。

# 1-菲亚特支持的 stablecoins

![](img/37636619309db1b5ce47a0bc41be5599.png)

Fiat-backed stablecoin issuance by [diedamlas](https://www.instagram.com/diedamlas/)

**定义:**对于菲亚特支持的稳定币的每一个单位，在发行公司或协议的储备中都有相应的菲亚特单位。以 Tether 为例，每流通一个 USDT，Tether 在巴哈马的 [Deltec 银行就有 1 美元的集中储备。这是一种利用基础货币稳定性的传统机制。](https://www.coindesk.com/business/2021/01/22/tethers-bank-deltec-says-stablecoin-is-fully-backed-by-reserves/)

**市值:**

![](img/af0a8072b7565a102d1df471ffea9d73.png)

Total market cap of fiat-backed stablecoins currently stands at +$155 billion, account for ~85% of the total stableocin market. Source: [CoinMarketCap](https://coinmarketcap.com/view/stablecoin/)

项目: USDT ( [系绳](https://twitter.com/Tether_to))、USDC ( [圈](https://twitter.com/circlepay)和比特币基地)、BUSD ( [币安](https://twitter.com/binance))、TUSD ( [信任令牌](https://twitter.com/TrustToken))、TRYB ( [BiLira](https://twitter.com/BiLira_Official) )、USDP ( [Paxos Dollar](https://twitter.com/paxosglobal) )，不一而足……

**稳定性:**平背稳定犬利用储备机制实现稳定性。用户只有在发行者的储备中存入一些法定货币，才能铸造(创造)法定支持的稳定货币。换句话说，发行者不首先收到法定货币存款就不能铸造新的稳定货币。通过将用户存款保留在储备金中，发行者保证每个用户一旦归还稳定的硬币，就能够赎回他们原来的法定存款。由于稳定硬币的价格跟随基础法定货币的价格，因此稳定性取决于基础货币的价格。如果使用相对稳定的法币作为抵押品(如欧元)，稳定的法币将保持更加稳定。

**分散化:**这是一个完全集中的结构，因为发行公司充当用户抵押品或法定货币的保管人。除非定期审计发行公司，否则这可能不是对用户最透明的结构。因为谁知道一个发行者是否在其储备中持有所有抵押品。菲亚特支持的稳定货币的批评者说，这一类别中的大多数稳定货币依赖美元储备的事实最终导致了区块链的美元化。最终，美元支持会带来系统性风险(如通货膨胀)和监管风险(如 KYC 要求、审查制度等)。)的秘密经济。

资本效率:这些稳定的资本创造成本很高，变现也很慢。发行者通常对法定存款收取 T2 费，赎回可能需要一天以上，因为他们是传统的法定结算渠道。此外，我们可能会看到一种情况，即秘密经济的资本需求可能超过法定货币所能提供的，这将使法定抵押品的效率降低。例如，在乌俄战争最激烈的时候，[乌克兰加密交易所 Kuna](https://www.coindesk.com/markets/2022/02/23/ukraines-wealthy-finding-it-hard-to-buy-crypto-amid-geopolitical-tension/) 由于 USDT 在交易所的供应有限，只能提供 USDT 4%的溢价。

![](img/f612b6326474ca94722a9fd943b8d0db.png)

Mission control deck for fiat-backed stablecoins by [diedamlas](https://www.instagram.com/diedamlas/). High stability, low decentralization, medium capital efficiency.

# 2-加密支持的 stablecoins

![](img/cc318d009706a6a0de75ab96d945955e.png)

Crypto-backed stablecoin issuance by [diedamlas](https://www.instagram.com/diedamlas/)

**定义:**对于希望避免法定货币系统性风险(如通货膨胀、审查)的去中心化寻求者来说，加密支持的稳定货币通过用其他加密货币超额抵押其储备来实现稳定性。“ **Over** ”是必不可少的，因为发行协议希望确保支持加密货币的波动性不会使系统抵押不足或支持不足。然而，这些稳定的货币并不仅仅作为无许可的通货膨胀保护货币。作为区块链创造的加密货币，这些稳定硬币在 DeFi 应用中也有多种用途，如杠杆交易，我们将在第 4 节中讨论。

**市值:**

![](img/70d9da6e99d8f77ca4398f90bdf311f1.png)

Total market cap of crypto-backed stablecoins currently stands at +$13 billion. Source: [CoinMarketCap](https://coinmarketcap.com/view/stablecoin/)

**项目:**戴([马克尔道](https://twitter.com/MakerDAO))、MIM ( [神奇互联网钱](https://twitter.com/MIM_Spell))、[流动资金美元](https://twitter.com/LiquityProtocol))、[原始股美元](https://twitter.com/OriginDollar)等等…

**稳定性:**用户只有向发行协议存入所需数量的抵押品，才能铸造加密支持的稳定币。这就保证了协议不会凭空产生稳定的积分，造成膨胀。加密支持的稳定硬币的价格通常与法定货币的价格挂钩。为了保持与菲亚特的稳定联系，这些 stablecoin 协议采用了各种专门的机制来影响用户对 stable coin 的需求和供应。例如，如果一种稳定货币的价格高于目标价格，协议将实施增加这些稳定货币供应的策略。

**去中心化:**密码支持的 stablecoin 协议由去中心化自治组织(Dao)管理。这意味着任何具备所需知识的人都可以参与一个加密支持的稳定币的管理。例如，参与者可以对协议提供的利率进行投票，或者对协议利用的算法的开发做出贡献(更多信息请参见第 4 节)。此外，稳定币的用户通常可以检查抵押比率和定义这些比率的算法，使协议的货币政策尽可能透明。与菲亚特支持的 stablecoin 发行商不同，加密支持的 stablecoin 协议不监管用户的资产。当用户想要制造稳定的密码时，他们只需将其加密资产锁定到智能合约作为抵押品，并保持对智能合约的完全控制。关于加密支持的稳定账户的一个批评是，为了实现稳定性，他们倾向于严重依赖[集中的菲亚特支持的稳定账户](https://twitter.com/KyleSamani/status/1438105848128147461?s=20&t=ZuH_wtRo7RkD2zH_PTS4iw)，这使他们容易遭受适用于菲亚特支持的稳定账户的相同风险。例如，目前 [68%的抵押品支持](https://makerburn.com/#/) DAI 由集中的稳定信贷组成。

**资本效率:**由于过度抵押，这些稳定债券比菲亚特支持的稳定债券更资本密集。为了创造新的稳定币，用户存入的抵押品价值通常高于他们获得的稳定币。而对于菲亚特支持的 stablecoins，抵押用户存款和他们收到的 stablecoins 是相等的。

![](img/76aa3907a1bf6f9a76911e5adc9d5636.png)

Mission control deck for crypto-backed stablecoins by [diedamlas](https://www.instagram.com/diedamlas/). High stability, high decentralization, low capital efficiency.

# 3-算法稳定积分

![](img/751d4cb33ea481c4a734b1eb40693dc7.png)

Algorithmic stablecoin issuance by [diedamlas](https://www.instagram.com/diedamlas/)

**定义:**算法稳定币(algorithmic stablecoin)越来越受欢迎，它是一种加密货币，可以确定性地调整其供应量，以使代币价格朝着目标挂钩的方向移动。换句话说，这些稳定的货币不是通过抵押机制实现稳定，而是通过模拟央行货币政策的算法实现稳定(还记得标题吗？)供应和需求的基本动态适用于算法稳定硬币，因此在高层次上，这些稳定硬币协议依赖于公开市场套利激励来增加或减少稳定硬币的供应，以匹配目标宠物。除了它们的 stablecoin 令牌，算法 stablecoin 协议通常还有另一个本地令牌:share 令牌(例如，Frax Finance 的 [FXS](https://coinmarketcap.com/currencies/frax-share/) )。股份代币用于稳定其稳定的货币对应物的价格以及管理协议。

**市值:**

![](img/a6956bb4ddffc28ff295a12db019e461.png)

Total market cap of algorithmic stablecoins currently stands at +$19 billion. Source: [CoinMarketCap](https://coinmarketcap.com/view/stablecoin/)

**项目:**([Terra Protocol](https://twitter.com/terra_money))、 [Frax Finance](https://twitter.com/fraxfinance) 、USDN ( [中微子](https://twitter.com/neutrino_proto))、FEI ( [FEI Protocol](https://twitter.com/feiprotocol) )等众多现有项目如 [UXD](https://twitter.com/UXDProtocol) 和 [VOLT](https://twitter.com/VoltProtocol)

**稳定性:**算法稳定连接协议依靠协议参与者来实现稳定性。例如，当对一种算法稳定币的需求下降时，这种稳定币的价格就会跌破其挂钩价。这要求《议定书》的现有参与者集体吸收短期波动。他们通过持有股票代币(而不是像市场上的其他人一样抛售)并押注于稳定的货币需求的未来增长来做到这一点。这在如此多不信任方的情况下很难实现，而且从历史上看，许多算法稳定点数在市场低迷时期失去了挂钩。当我们在第 4 节讨论具体项目时，这一点会变得更加清楚。

**去中心化:**类似于加密支持的 stablecoins，算法 stablecoins 通过 DAO 治理实现去中心化。由这些协议实现的货币政策由股票令牌持有者投票决定，并且对任何使用他们的 stablecoins 的人都是透明的。由于缺乏抵押品支持，这些稳定的货币成为最不受限制的货币形式。

**资本效率:**算法稳定的资本不需要任何抵押品，因此它们是抵押品有效的。

![](img/7c09d85baeee1192084d93f044f6daaa.png)

Mission control deck for algorithmic stablecoins by [diedamlas](https://www.instagram.com/diedamlas/). Low stability, high decentralization, high capital efficiency.

正如我们所见，哪种稳定币更好并没有明确的答案。“是谱，老弟！”在这里也适用，权衡无处不在。根据数据，可以肯定的一点是，菲亚特支持的稳定硬币使用最广泛，约占流通稳定硬币总供应量的 85%。如果你问这是为什么，我认为这可以归结为三个简单的事实:

*   美元存取:世界各地的人们都希望用美元进行交易和储蓄。与传统的银行渠道相比，以美元计价的法定支持的稳定债券是获得美元敞口的一种更快、更容易的方式。
*   熟悉的机制:在一天结束时，人们会问“那么，这是如何工作的？”。很容易解释菲亚特支持的稳定债券的储备机制，这只会建立信任。
*   **早期进入** : Tether 自 2015 年开始运营，随着 2018 年 ICO 热潮的到来，其受欢迎程度有所增长。人们只是熟悉 USDT 和其他菲亚特支持的稳定资本。

那么分散的稳定密码(包括密码支持的和算法的)重要吗？我在这里不是法官，但受到[哈苏布的帖子](/dragonfly-research/fighting-to-be-stable-the-evolution-of-stablecoins-aca81fb432f9)的启发，我完全可以看到，只有随着美元**通胀**的增加和对美元支持的稳定债券**监管**(如[第 2 节](/coinmonks/stablecoin-primer-section-2-stablecoin-landscape-132b27f7f2d3)所述)，人们才会过渡到分散的稳定债券。虽然 UST 和 FRAX 最近的市值增长是分散化稳定资本的亮点，但就目前而言，数字告诉我们，人们似乎可以很好地使用许可的加密美元。

所以你可以自己回答这个问题，在第 4 节，让我们仔细看看具体的 stablecoin 项目，了解它们如何实现稳定性、分散化和资本效率。

**Stablecoin Primer —简介:** [划手和慢炖锅](https://namsso.medium.com/stablecoin-primer-intro-54689d6fcdba)

**Stablecoin 引物—第 1 节**:[stable coin 的路径](/coinmonks/stablecoin-primer-section-1-path-to-stablecoins-8bcdb39c73e1)

**Stablecoin 底漆—第二节** : [Stablecoin 景观](/coinmonks/stablecoin-primer-section-2-stablecoin-landscape-132b27f7f2d3)

**稳定币入门—第三节**:稳定币类型(你在这里)

**稳定潜水引子——第四节** : [稳定潜水浅潜](https://namsso.medium.com/stablecoin-primer-section-4-stablecoin-projects-28b509624165)

**稳定玉米引物—第五节** : [稳定玉米的未来](/coinmonks/stablecoin-primer-section-5-stablecoins-future-b9649a85a722)

**稳定币引物-奖励部分**:遗漏任何东西

尽情享受吧！乐意通过评论、 [Twitter](https://twitter.com/_namsso_) 或 [Linkedin](https://www.linkedin.com/in/osman-sarman/) 进一步聊天

特别感谢 [NEAR 团队](https://nearprotocol.medium.com/)拨款使这项研究成为可能。

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n 格拉夫](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰纳诺 s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)