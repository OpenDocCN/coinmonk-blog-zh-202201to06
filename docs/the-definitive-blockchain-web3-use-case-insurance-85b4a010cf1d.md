# 权威的区块链和 Web3 用例——保险

> 原文：<https://medium.com/coinmonks/the-definitive-blockchain-web3-use-case-insurance-85b4a010cf1d?source=collection_archive---------14----------------------->

![](img/3d294edb14765316cb063a460600627c.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/flood?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近，马克·安德森在播客“与泰勒的对话”中被问及 Web3 的真实使用案例。剧透:他真的不能很好地表达，特别是在播客领域。就像他们说的，互联网从不失手。就连 Tether 的 CTO 也开了一枪:

那么，批评者是对的吗？[web 3 是不是扯淡](https://www.stephendiehl.com/blog/web3-bullshit.html)？

我的答案肯定是否定的(对我来说，这就像一个物理学教授不能解释重力是如何工作的……这并不能使重力无效)，但我确实认为 Web3 倡导者的讨论框架有待改进。问题在于试图在如此狭窄的范围内描述区块链的好处。在 Andreessen 的案例中，从微交易的角度来看，它是如何使播客受益的。

更确切地说，区块链如何改变世界的范围必须更加广泛，并超越货币的效用。我是这样描述的[之前](/coinmonks/my-impressions-of-moxies-first-impression-of-web3-part-1-648fbe1fd300):

> **这是集中式实体保险**归结到一个基本问题——在生命周期的成本效益分析中，允许第三方对数据库进行可审计验证的交易费用是否值得，在集中式堆栈被破坏的罕见情况下是否值得激活？

让我们从基本原理中剥离层次。

## 概观

区块链的核心仅仅是一个分散的数据库(和以太坊的虚拟机)。

这与我们目前所习惯的、典型的非区块链技术堆栈所包含的内容形成了对比——集中式数据库实例，其中一个实体控制其读/写访问并负责维护其完整性。数据库实例位于由所述实体控制的服务器上，每次你登录他们的网站进行交易(比如通过 Venmo 给朋友汇钱)，数据库就会更新，你的交易也会得到“处理”，所有这些都由该实体代表你完成。

一切都很好——交易很快，不需要任何费用(显然),并且立即“结算”(我们稍后将回到这些“好处”)。

与提议的 web 3/区块链堆栈相比，乍一看，它似乎很麻烦而且没有根据。与 MySQL 不同，你有一个分散维护的数据库，在那里结算无法完成，直到验证者对分类帐的状态达成一致(这可能需要多个挖掘块)。交易速度较慢，处理的吞吐量较低，更不用说，您还需要为每笔交易支付汽油费！

所以你可能会问，到底哪里有好处？嗯，到目前为止我只画了一幅不完整的画；然而，这正是区块链批评经常得出的结论。

## 区块链作为集中式实体保险

正如我在之前说过的[:](/coinmonks/my-impressions-of-moxies-first-impression-of-web3-part-1-648fbe1fd300)

> 它忽略的是，区块链是为边缘案件而建造的。批评家们把苹果比作橘子——中央集权实体的日复一日的“美好时光”(当生活的肉汤；MySQL 数据库已经启动并运行；Robinhood app 居然让 GME·斯通克斯的采购订单通过；*我正在支付*我的保险公司的保险费)给日复一日的加密工作——不可否认的是，这需要更多的维护工作，可扩展性较差，并且需要为块空间付费。
> 
> 好吧，加密的效用在繁荣时期并没有表现出来。理论上，当网络出现大规模故障时，分散式系统会停机(在此插入索拉纳的笑话)；当数据库关闭时；当银行挤兑发生时；罗宾汉的城堡领主[来召唤](https://www.washingtonpost.com/business/2021/01/29/robinhood-citadel-gamestop-reddit/)；洪水摧毁了保险公司，而保险公司本该向我们付款。出现异常。当人类的腐败或无能取代了。在那些时刻，分散的代码就是法律，协议是不可改变的。至少在理论上是这样。

天真的观点忽略了区块链真实用例背后的细微差别，它应该在异常事件期间发光(理论上)。这就是为什么我把区块链比作保险，也是为什么很难简洁而又宏大地阐明它的好处(像安德森这样的风险投资家应该做的)——因为它真正的理论效用首先植根于厌恶损失，而不是具体的收益(也就是说它并不性感)。

如果你眯着眼睛看，针对区块链的许多同样的批评可以转而用于对保险的抱怨。

如果我每天都开车，但从未出过事故，那么我的汽车保险似乎也是多余的；汽车保险是“[寻找明天的问题来证明今天的投资](https://www.stephendiehl.com/blog/web3-bullshit.html)”。为什么我要心甘情愿地以汽车保险费的形式支付额外的每月费用，而我却没有得到任何好处？如果我从来没有生病或需要医生，为什么我需要健康保险？如果我的房子从来没有洪水，为什么我需要洪水保险？

这呼应了反加密技术人群的情绪:为什么我们需要一个干净、高效的 MySQL 数据库*的替代品？

(*这个反问中隐含的是警告——“假设稳定状态”，即事物是真实的——在这种情况下，他们是对的！在理想的情况下，没有必要分散管理，因为所有的事情都在运转；唉，一旦你过了高中物理，摩擦就存在了。)

因为保险不是为一切顺利的时候准备的；是为了它击中风扇的时候。

打粉丝:罗宾汉[心血来潮限制 GME 交易](https://www.cnet.com/personal-finance/investing/robinhood-backlash-what-you-should-know-about-the-gamestop-stock-controversy/)。伦敦金属交易所[单方面回滚交易](https://www.cnbc.com/2022/06/07/london-metal-exchange-hit-with-two-us-lawsuits-over-nickel-trading-chaos.html)。Twitter 突然[限制第三方 API 访问](https://www.theverge.com/2012/8/23/3263481/twitter-api-third-party-developers)，实际上扼杀了建立在它们之上的业务。

区块链是逻辑保险——无论外部因素如何，你都可以保证你的智能合同将以相同的方式执行；你可以保证分散的账本会继续增长。冷酷、客观的规则仍然是规则。不考虑市场状况，不考虑政治影响等等。

想象一下，如果我*实际上有洪水保险，但发生了洪水，但我的保险公司[骗了我](https://www.npr.org/2016/05/24/478868270/business-of-disaster-insurance-firms-profited-400-million-after-sandy)——这会使保险成为骗局吗？只限于它的个别实现，而不是作为一个概念。我只是从一家差劲的公司得到了差劲的保险；保险理论仍未受到污染。就像加密一样。不要让个别失败的加密公司(hello Celsius，BlockFi 等)在你最需要的时候，因为执行不力和鲁莽的抵押不足而在最不合适的时候失败，影响了你对区块链作为一个概念的真正效用的看法。*

*也要明白，为了获得保险的好处，你必须支付保险费——正如无创新者喜欢说的，价值不可能凭空创造。从交易者(默认的 web2 利益相关者，我们很自然地把自己想象成)的角度来看，交易费(汽油费)只是一个 bug，但是从矿工的角度来看，它们是一个特性。它们是激励的必要注入。这是你为维护一个分散的网络所付出的代价。*

*它们类似于你为换取风险分配而放弃的保险费。在 crypto 的例子中——有一天你的中央集权实体受到激励而违背你的利益。*

> *交易新手？试试[加密交易机器人](/coinmonks/crypto-trading-bot-c2ffce8acb2a)或者[复制交易](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c)*

*不要忘了——使用集中式数据库时，你也需要支付交易费，这要便宜得多，而且谷歌或脸书或抖音在[交易所为拥有你的数据](https://www.axios.com/pro/media-deals/2022/06/29/tiktok-data-concern-republicans)提供补贴。*

*现在，如果人们不同意这种保险是必要的这种评估，以及它所带来的权衡，那么这是完全公平的。他们只是有更高的风险容忍度*，并愿意盲目地相信中央集权的实体总是表现得令人钦佩和公平。或者他们很懒，会用必须使用元掩码的事务级激活能量来换取使用平滑的文莫 UX 的无忧无虑的无知是福的心态。*

*(*是的，没错——我只是暗示 web2 比 web3 有更多的概念风险。因为在 web2 中，公司被授权去拧你；鉴于他们拥有你的数据，你没有优势，退出的门槛高得惊人。在 web3 中，公司仍然可以欺骗你，但至少他们必须在链上分析的阴影笼罩下这样做。通常情况下，web3 中的骗局会提前曝光，但典型用户的退化特征使他们容易受到影响。以 Luna 为例——一个不可持续的约 20%的 4 月份，人们警告了几个月的薄荷和燃烧机制:*

*所有这些都被那些模仿纯粹堕落行为的疯子们一笔勾销了。这不是区块链的根本缺陷，而是人类固有的缺陷——贪婪。)*

*对于批评者来说，crypto 经常被批评为“[关于我们如何重建互联网以反映我们对一个更加人道和平等的社会的渴望的理想主义和乌托邦思想的一部分](https://www.stephendiehl.com/blog/web3-bullshit.html)”，暗示了代表 web3 支持者的某种理想主义的天真。*

*然而，真正的解释实际上是相反的——一种内在的怀疑主义渗透到整个区块链，需要在每一层进行制衡。区块链的每一个方面都是一次详细检查，而不是信任某个集中的实体——每个验证器都被认为在攻击网络。斯蒂芬·迪尔(Stephen Diehl)称之为“[试图就一个巨大的全球国家机器](https://www.stephendiehl.com/blog/web3-bullshit.html)达成共识的疯狂浪费过程”——我称之为安全因素。区块链的怀疑态度如此坚定，以至于它乐意牺牲 UX(希望只是暂时的)，并愿意为其安全性买单。出于这种悲观，产生了对保险的需求。*

*真正的理想主义和乌托邦主义难道不是期望你的 web2 实体永远值得信赖吗？*

*至少让我们对批评家们反对的是什么，以及各自的利弊达成共识。通常，他们想通过比较 web3 的最差特征和 web2 的最佳特征来攻击 web 3。让我们在平等的基础上比较它们，而不仅仅是想象我们的 web2 世界在理想的情况下。让我们以对“新事物”同样的怀疑态度来看待现状。*

## *区块链作为退出权*

*那么，web3 会给播客带来什么好处呢？*

*这又一次归结到边缘案例——保险。在最好的时候，当你和中央实体有很好的关系时，那么拥有链上机制的好处是最小的。*

*但是考虑一下并非不可行的边缘情况——如果 YouTube 改变了他们的货币化政策，或者你因为不支持当前的而被 Twitter 取消平台，或者 Spotify 拒绝列出你的播客。您想使用不同的提供商，但被拒绝导出您的订户列表；平台控制着你和观众的关系。*

*Via [丹·芬利](/@danfinlay/what-moxie-missed-on-web3-wallets-8dc572e7f39b):*

> *当你可以永远完全信任你的供应商时，退出的权利并不重要。也许你的银行很好，信用卡也为你服务，所以数字货币的概念对你来说是难以置信的愚蠢。如果你的账户因为银行不喜欢你的钱的来源而被冻结，你可能会有不同的看法。*

*仅此而已。区块链给你一个*潜在的*GTFO 的手段。现在，实施能否赶上理论还有待观察。*

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)*
*   *[加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [KuCoin 评论](https://coincodecap.com/kucoin-review)*
*   *[火币加密交易信号](https://coincodecap.com/huobi-crypto-trading-signals) | [HitBTC 审核](/coinmonks/hitbtc-review-c5143c5d53c2)*
*   *[TraderWagon 回顾](https://coincodecap.com/traderwagon-review) | [北海巨妖 vs 双子 vs 比特亚德](https://coincodecap.com/kraken-vs-gemini-vs-bityard)*
*   *[如何在 FTX 交易所交易期货](https://coincodecap.com/ftx-futures-trading)*