# 全部加密—2022 年 4 月 1 日第一周

> 原文：<https://medium.com/coinmonks/all-been-crypto-week-1-april-2022-9c750484c7d?source=collection_archive---------53----------------------->

本周收盘时，我们的市值相对保持不变，为 2.2 万亿美元。早些时候有一个重要的反弹，昨天在欧盟敌意加密裁决后放弃了很多收益。BTC 表现不佳，现在优势下降到 39.6%，L1 和优于。Luna、AVAX 增长了 7-8%，SOL 增长了 19%。本周的另一个大赢家是多链聚焦协议。他们发布了 v3，提供了+25%的跨协议可移植性和+37%的 RUNE，并在 DEX 上正式集成了 terra 生态系统资产。在新闻中，我们看到 Axie 的 ETH bridge Ronin 又遭受了一次重大黑客攻击，欧盟议会针对私人钱包的敌意裁决，Microstrategy 获得了 2 亿 BTC 抵押贷款，Terra Foundation Guards 继续将 BTC 纳入国库。享受阅读！

蝙蝠太极—[btc21@mail.com](mailto:btc21@mail.com)

![](img/6660924677589649760d2a52f3f0fa0b.png)

# 标题:

## [**又一次最大的黑客攻击——浪人**T5 上的 600ml](https://www.bloomberg.com/news/articles/2022-03-29/hackers-steal-590-million-from-ronin-in-latest-bridge-attack)

随着加密变得越来越大，被黑客攻击的金额也越来越多。不过，这一次非常有趣。这件事发生在上周的 23 号，有几天没有被注意到(至少被市场注意到),直到有人显然无法提取 5k ETH(这座桥应该能容纳超过 15 万 ETH)。直到那时，Sky Mavis 团队才意识到，一名黑帽黑客已经成功攻破了 9 个验证器节点中的 5 个，并从网桥中抽取了 17.3 万以太网和 25.5 万 USDC。他们立即停止了连锁反应，并跟随主要交易所进行交易。我们仍然不确定他们是如何妥协的，实际上他们有很多困惑[把部分赃物送到 CEX](https://twitter.com/peckshield/status/1509003730334670861?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1509003730334670861%7Ctwgr%5E%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fcryptopotato.com%2Fthe-biggest-ever-crypto-hack-what-happened-in-the-ronin-bridge-attack%2F) ，甚至通过 CEXs 资助收件人地址。来自[的威尔·皮斯特](https://metaversal.banklesshq.com/p/analyzing-the-ronin-bridge-hack?token=eyJ1c2VyX2lkIjo3NTUyNTk4MywicG9zdF9pZCI6NTEyNTc2OTAsIl8iOiJkMHR0byIsImlhdCI6MTY0ODc3NzAwMiwiZXhwIjoxNjQ4NzgwNjAyLCJpc3MiOiJwdWItMjQyMTgxIiwic3ViIjoicG9zdC1yZWFjdGlvbiJ9.x5b-Dp9EgAZaAobh6H16IsSGPUORmI-XQytlgKf6uY8)有一个很好的总结。为什么这一个是有趣的，因为这里的缺陷不是像大多数以前的桥梁黑客那样的桥梁智能联系，而是更经典的“私钥”问题。Ronin 说黑客使用被黑的私人钥匙来伪造取款。他们通过他们的 gas-free RPC 节点找到了一个后门，他们滥用这个后门来获取 Axie DAO 验证程序的签名。因此，如果有一个更分散的节点系统和更高的共识要求(他们现在将它增加到 9 个验证者中的 8 个)，这可能是可以避免的。具有讽刺意味的是，在 25 日，他们还宣布了对 Ronin 的费用改革，将根据你在生态系统中的 NFT 股份的价值来限制自由交易的数量。Axie token 甚至 RON 相对稳定，Wow 下降了 10%和 15%。

## **隐私之战——欧盟更近一步** [**禁止私人钱包**](https://decrypt.co/96539/eu-parliament-votes-impose-kyc-private-crypto-wallets) **，美国提出** [**电子现金法案**](https://www.coindesk.com/policy/2022/03/28/us-lawmakers-introduce-ecash-bill-in-new-push-to-create-a-digital-dollar/)

周四，欧盟议会投票赞成禁止匿名加密交易的有争议的措施。[提案](https://decrypt.co/96539/eu-parliament-votes-impose-kyc-private-crypto-wallets)旨在将适用于超过 1000 欧元的传统支付的反洗钱(AML)要求扩展到加密领域。它们还取消了加密支付的下限，因此即使是最小的加密交易，也需要识别付款人和收款人，包括使用非托管或自托管钱包的交易。正在讨论的进一步措施可能会导致不受监管的加密交易所从传统金融体系中脱离出来。这是对加密的无许可本质的核心价值之一的巨大打击，你可以想象得到来自业界的巨大阻力。不幸的是，这似乎是一种趋势，各大公司已经在加强他们的 kyc..[比特币基地](https://www.coindesk.com/business/2022/03/25/coinbase-to-require-recipient-information-for-crypto-transfers-from-users-in-canada-singapore-and-japan/)现在要求加拿大、日本和新加坡的用户提供加密传输的接收方信息。在美国，我们看到了一项有趣的新法案的出台，该法案旨在通过电子现金保护某种类型的隐私。提出该法案的立法者建议财政部而不是美联储应该创造一个数字美元。根据该法案的定义，这种电子美元将是一种不记名工具，人们可以在手机或卡上持有。该系统将是基于令牌的，而不是基于账户的，这意味着如果有人丢失了手机或卡，他们将失去资金。因此，这不是一个基于区块链的分布式账本系统，从而承诺保护隐私。

## **黄色和橙色的故事——泰拉·抽水 BTC**

我们已经在 2 月 25 日的周刊上看到过，当时我正在讨论他们为 UST 财政部购买的第一笔 10 亿美元的 BTC 债券。此后，道权一直在微妙地、越来越不那么微妙地[暗示他想发展得更大，并且实际上已经开始在公开市场上购买](https://twitter.com/stablekwon/status/1503296630396645376?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1503296630396645376%7Ctwgr%5E%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fcointelegraph.com%2Fnews%2Fwe-re-already-buying-terra-founder-plans-to-obtain-10b-btc-for-reserves)。正如我之前所说，我不喜欢风险投资参与大宗销售，因为这不是分散的，我希望他们在公开市场上做得更多。看起来他们确实改变了策略。或者他们只是在买了一个相当大的垃圾后谈论 BTC，并试图建立一个自我强化的反馈循环。这就是一些批评家所说的，他们印刷《月神》来购买 BTC，在这个过程中抬高了两者的价格。我更倾向于建设性的一面，看看 BTC 是如何成为分散的 L1 另类投资者的首选储备资产的。问题是他们在哪里停下来，(100 亿真的做权术吗？)以及他们是否会将该库扩展到其他加密资产，从而将 UST 越来越多地转变为像 instrument 一样的阿呆。

# **行情:**

> 它(加密货币)被证明是一种真正的价值储存手段，但它尚未证明其在有效价值交换方面的效用。我们的平均行程是 15 美元，20 美元。所以，我们需要密码变得更有效率。我们当然会考虑所有的选择

**优步首席执行官达拉·科斯罗萨西**

> 我们看到一些最早的和最雄心勃勃的加密想法开始展现。
> 完全由数字原生资产支持的跨链分散稳定币是 2016 年的圣杯。
> 祝福

**朱苏——三箭资本联合创始人**

> 议会通过的资金转移条例的最新草案对待加密和每个持有加密的人都不同于法令。

**比特币基地首席执行官 Brian Armstrong**

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [有哪些交易信号？](https://coincodecap.com/trading-signal) | [Bitstamp vs 比特币基地](https://coincodecap.com/bitstamp-coinbase) | [买索拉纳](https://coincodecap.com/buy-solana)
*   [ProfitFarmers 回顾](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix 交易机器人](https://coincodecap.com/cornix-trading-bot)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [my constant Review](https://coincodecap.com/myconstant-review)|[8 款最佳摇摆交易机器人](https://coincodecap.com/best-swing-trading-bots)
*   [MXC 交易所评论](/coinmonks/mxc-exchange-review-3af0ec1cba8c) | [Pionex vs 币安](https://coincodecap.com/pionex-vs-binance) | [Pionex 套利机器人](https://coincodecap.com/pionex-arbitrage-bot)