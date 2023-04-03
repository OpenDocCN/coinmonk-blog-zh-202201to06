# 比特币均衡理论

> 原文：<https://medium.com/coinmonks/the-bitcoin-equilibria-theory-608fb80507b7?source=collection_archive---------12----------------------->

2015–2022 年比特币价格分析后我的结论。

## 入门指南

当我开始用数学方法解读比特币价格时，我感兴趣的是找出比特币价格是否遵循一种“内在逻辑”，或者它是否取决于外部影响，如世界经济形势，或类似因素。
在 2016 年减半后的价值趋势与 2020 年减半后的趋势之间的第一次比较之后，我认为这将是清楚的。价格似乎只受内在价值的驱动，这也是库存-流量理论所描述的。我意识到价格发展有一个数学描述，它可以描述长期发展以及中期增长。
但在 2021 年，比特币价格的反应与预期不同。我们来看看为什么。

## 方程式

长期价值趋势显然遵循一般方程:
**USD/BTC≈a SF ^ b**
SF =现有比特币数量/每年开采的比特币数量。
a =线性因子
b =指数因子
这是由 PlanB 的库存-流量理论证明的。[1]
根据我自己的研究，一个具体的公式是**0.116 SF ^ 3.4** a 和 b 的值是使用 2016 年和 2020 年减半时的比特币价格计算的。为什么这是有意义的，你会在这个故事中了解到。
我的研究还表明，减半后的价值趋势由以下等式决定:
**USD/BTC≈a e ^(Bt+CT)**
t =自开始增长以来的年数
a =以美元计的起始价值
b =开始增长因子
c =增长增加因子
我的故事中的推导[一点数学和一个比特币预测](/@100trillionUSD/modeling-bitcoins-value-with-scarcity-91fa0fc03e25) [2]。以下是我对 2016/17 年和 2020/21 年牛市的具体计算

![](img/c2911127037975d6ce2bc88e4ee01f07.png)

Bitcoin hyper-exponential growth in 2016/17

![](img/29e203788e2b1ac9e34582465ea5dc3d.png)

Bitcoin hyper-exponential growth in 2020/21 (with way to optimistic forecast)

我还注意到比特币的价值有一个下限，可以用下面的等式来描述:
**USD/BTC≈a e ^ Bt**
a =起始价格
b =指数增长因子
t =自开始增长以来的年数
它可以直接从 S2F 等式中导出。
将两个数值进行比较，计算出一个数值到下一个数值的指数增长。
实际比特币周期(2020 年至 2024 年)的方程式为
**USD/BTC≈****9100 e ^ 0.68t** 这对应的是每月上涨 5.8 %或一年内价值大约翻倍。如果这个等式是正确的，2024 年下一次减半时的比特币价格应该在 121000 美元左右。
该路径通常在减半之前的时间段最明显。

![](img/d470d70423d5813c45b6f9c1d2bee9a7.png)

exponential and hyper-exponential growth 2015–2018

小提示:
所描述的行为仅仅是一种观察。不幸的是，我无法给出比特币如此表现的原因。这些方程是真实的，也可以用数学方法验证。例如，牛市 2020/21 与找到的方程的相关性是 0.977。因此，在任何情况下都可以排除巧合匹配。

## 库存到流量的平衡

我们都知道 PlanB 关于他的存量到流量理论的预测在 2021 年没有实现。根据他的理论，到 2021 年底，比特币的价格应该会超过 10 万美元。这是否意味着他的理论或方程式有缺陷？

幸运的是，错误只是出在对数字的解读上。
普兰布的错误在于，他将存量-流量方程的值解释为对比特币价格的预测。然而，实际上，这是对一种可能的均衡的描述。这意味着比特币价格不一定会达到，而是当它们达到适当的水平时，价值会被这种平衡“捕获”。这可以在 2018 年初的价值观
课程中很好地看到。由于市场上的欣快情绪，当时的比特币价格非常夸张，然后突然暴跌。
令人惊讶的是，就在预测的存量-流量值的水平上。他犯的第二个错误是，他在计算中使用了统计累加值，而不是在减半时非常精确的已知值。因此，他在计算中包括了市场的乐观情绪，这通常会导致价值被夸大。

在我的计算中，我使用了一种简化的方法来获得 S2F 值，并假设采矿活动是平均的。实际价值取决于相应时间的采矿活动。该参数各不相同，并且仅在比特币区块链上可用。因此它很难用在一般的等式中。对我的计算来说，由此产生的误差可以忽略不计。

## 超指数增长平衡

任何消息，以及主要的比特币买入或卖出，通常只会在非常短的时间内影响价格，但又被修正。2021 年 2 月，特斯拉投资 10 亿美元比特币就是一个例子。

![](img/acf4b9bc52f92a7fa1a04aed7a3fd4a3.png)

Overview of Bitcoin growth in 2020–22

当值回落到计算的路径时，这是一个平衡的强烈指示。

然而，我自己在解释超指数增长时犯的错误是，我最初并不认为这种平衡会被外部影响简单地抛弃。然而，正如你在图表中看到的，相应的坏消息，例如印度或中国的加密禁令足以让比特币失去平衡。有趣的是，我们随后可以看到一个新的平衡形成了，这又是一个超指数增长。从 2021 年 5 月 20 日到 2021 年 11 月 21 日的价格发展清楚地显示了与减半后的直接发展类似的发展。
我必须意识到，这样的平衡也可以在没有直接明显原因的情况下保持，因为它发生在 2021 年 11 月 21 日之后。
人们只能猜测原因，但在这种情况下，重要的是均衡被完全抛弃，价格趋势没有任何调整。上升的路好像真的只有一条，从一开始就是固定的。
这种方式只能被中断，向上的方式不会发生调整或改变。
中断后，上升趋势又从头开始，例如减半后。在第一次增长实现后，超指数增长的逻辑再次生效。上升趋势每次都在加强。

## 指数增长平衡

第三个平衡特别重要。它构成了比特币价值的下限。如果这一限制被大量低于，那么一个非常快速的向上修正发生。通常的缓慢增长，如超指数增长，在这里没有发生。2020 年 2 月 13 日的崩盘就是一个例子。

![](img/f72417b73556ab3b65787441a8d92d99.png)

Bitcoin Growth Phase 2018–21

人们在这里可以看到直接的向上修正。达到的下限值不稳定，立即被保留。
我认为，如果不是这样，比特币将会有一个严重的问题，因为它可能会离开所有的稳定均衡。在整个比特币历史上，下冲是相当罕见的，通常发生在上下界越来越接近的时候。
在这里，你可以非常清楚的看到，这段时间比特币价格是沿着一个轨道运行的。即使是更大的崩溃，如 2018 年 11 月 9 日，也不会低于这条线，并被它捕获。这很好地说明了它作为均衡的功能。

## 摘要

总体而言，可以观察到比特币价格的以下行为:
价格通常在下均衡(指数增长)和上均衡(存量对流量值)之间运动。高于和低于这些限制的值是不稳定的，并导致相应的修正。在这些限度内，价格通常沿着超指数路径移动，这也代表均衡。然后，价格要么被库存-流量平衡所捕获，要么上升趋势被中断并达到新的平衡。
崩溃，或者低指数增长的下降趋势也是可能的，然后现有的上升趋势再次导致超指数增长。
减半的时候，上下界重合，所以当时的真实比特币价格正常是在一个很窄的范围内。
库存-流量平衡确实是阶梯形的，并且在减半后突然改变，因此在接下来的周期中立即跨越了一个新的值范围。根据我的方程式，2020 年这个范围在 9100 美元到 96000 美元之间。

## 观点

就目前的情况来看，价格趋势在未来将变得更加不稳定，尤其是由于杠杆交易的众多机会。这将导致更多的价格下跌，价值可能会更经常地回落到下限。因此，整体价值趋势将变得更加平稳，减半后的极端上涨可能会更早中断。然而，总的来说，目前看来，由 S2F 理论决定的长期趋势将会保持下去。

我的定期更新预报可以在这里找到:
[www.pisu666.de](http://www.pisu666.de)
你可以在 twitter 关注我: [Pisu@Pisu6661](https://twitter.com/Pisu6661)

注意:本文决不能被视为财务建议。这只是我的个人观点。

## 参考

[1]用稀缺性建模比特币价值，由 PlanB
[https://medium . com/@ 100 trillion USD/Modeling-bitcoins-Value-with-稀缺性-91 fa 0 fc 03 e 25](/@100trillionUSD/modeling-bitcoins-value-with-scarcity-91fa0fc03e25)
【2】一点数学和一个比特币预测，由 Pisu
[https://medium . com/coin monks/A-Little-Math-and-A-bit coin-Forecast-BC addc 17d 252](/coinmonks/a-little-math-and-a-bitcoin-forecast-bcaddc17d252)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [收购 AXS](https://coincodecap.com/buy-axs-token)
*   [投资印度的最佳加密软件](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021) | [WazirX P2P](https://coincodecap.com/wazirx-p2p)
*   [7 个最佳零费用加密交换平台](https://coincodecap.com/zero-fee-crypto-exchanges)
*   [最佳网上赌场](https://coincodecap.com/best-online-casinos) | [期货交易机器人](/coinmonks/futures-trading-bots-5a282ccee3f5)
*   [分散交易所](https://coincodecap.com/what-are-decentralized-exchanges) | [比特 FIP](https://coincodecap.com/bitbns-fip) | [宾邦评论](https://coincodecap.com/bingbon-review)
*   用信用卡购买密码的 10 个最佳地点
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt)
*   [阿联酋 5 大最佳加密交易所](https://coincodecap.com/best-crypto-exchanges-in-uae) | [SimpleSwap 评论](https://coincodecap.com/simpleswap-review)
*   [购买 Dogecoin 的 7 种最佳方式](https://coincodecap.com/ways-to-buy-dogecoin) | [ZebPay 评论](https://coincodecap.com/zebpay-review)
*   [最佳期货交易信号](https://coincodecap.com/futures-trading-signals) | [流动性交易所评论](https://coincodecap.com/liquid-exchange-review)