# Arkadiko 清算池

> 原文：<https://medium.com/coinmonks/arkadiko-liquidation-pool-9a2e98bb6ee3?source=collection_archive---------8----------------------->

你好，阿卡迪亚人

忠实的追随者已经知道这次升级即将到来！我们对它已经兴奋了很长时间，因为它是多方面的重大改进。

在本帖中，我们深入探讨 Arkadiko 清算池的细节，这是一个清算基础设施，通过确保充足的备用流动性来改善 Arkadiko 协议，以便在需要时购买保险库抵押品。

**这次升级的背景是什么？**

作为补充，Arkadiko 是一个分散的流动性协议，允许用户铸造 USDA 的 Arkadiko stablecoin。为了铸造 USDA，用户将抵押品锁在 Arkadiko 保险库中。我们支持 STX，它可以通过 PoX 和 xBTC 持续获得收益。

Arkadiko 金库使链上用户能够通过美国农业部创造额外的流动性。它确实带来了一些责任，因为用户需要仔细关注他们的 Vault 健康状况。金库中锁定的抵押品价值与铸造 USDA 所承担的未偿债务之间的比率需要得到控制，以确保 USDA 始终得到金库中更多资产的支持。如果抵押品的价格大幅下跌，导致价值与债务之间的比率不健康，则需要启动清算机制来偿还债务。作为偿还债务的回报，清算人以 10%的折扣获得金库中的抵押品。这使得金库清算非常有吸引力，因为你以低于公平市价的价格购买加密资产。

现在，通常来说，利用这种类型的机会是留给老练的玩家的，他们观察智能合约，并对标记为清算的金库自动做出反应。没有运行脚本，没有资金备用移动，你会太慢。

**arka diko 清算池来了！**

我们已经创建了一个解决方案，每个人都可以在不运行专门软件的情况下参与金库清算。我们通过创建一个资金池来做到这一点，在这种情况下是美国农业部，并运行我们自己的脚本来指导美国农业部在需要时进行清算。

![](img/b345e1c6f50910a5872753a0afb114cd.png)

Example liquidation with xBTC

Arkadiko 运行这些脚本来帮助支持该机制，但这绝不是必需的。任何人都可以调用智能合约上的函数来触发清算金库中的清算池。这意味着清算池的工作是完全分散的。我们只是出于对社区的礼貌运行脚本。

我们也只能将 USDA 用于抵押品购买，而不能用于任何钱包提款。因此，这是一个分散的和非监禁的解决方案，在 Arkadiko 的精神。

这个资金池的工作方式类似于大多数 DeFi 资金池机制，在这种机制下，缴款和利润按照你的资金池份额按比例分配。请注意，美国农业部用于清算，因此它实际上是贴现资产的交换。当这种情况发生时，你的 USDA 的一部分就会变成 xSTX/STX/xBTC。然后，你可以收回这些代币，出售它们，将美国农业部重新纳入清算池，或者享受套利利润。

这种方法对 Arkadiko 有几个优点和好处:

1.  用于清算的资金池，提高美国农业部在市场低迷情况下的稳定性和稳健性。
2.  美国农业部的单一赌注用例，有经济基本面支持(清算折扣)
3.  由于 1)提高了稳定性，我们可以提高金库的贷款价值比，创造更多的流动性和额外的效率。

除此之外，我们还将向这个池子排放 DIKO 气体！根据最近的治理投票，总排放量的 8.2%将被送往那里。计算一下这将是多少 APY，对于决定加入这个池的早起鸟来说，肯定会有一些阿尔法。

美国农业部承诺将有一个锁定机制。在有多少价值是备用的方面让池波动很大是不理想的，我们更希望有稳定的价值存在。美国农业部存款的初始锁定期为 30 天(4320 块)。每次存款时锁定都会重置，在复利/转存时请注意这一点！纪元周期为 5 天，DIKO 奖励在每个纪元结束时发放，在纪元开始时按比例分配给 USDA。这意味着，第一笔 DIKO 奖励将在池中存款 7 天后发放。

这就是关于清算池的所有知识，真的就这么简单！

锁定这一新功能的治理投票正在运行，请继续并在此投票[。](https://app.arkadiko.finance/governance/11)

希望看到你和我们一起清算。

去清算池和更远的地方！

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Capital.com 评论](https://coincodecap.com/capital-com-review) | [香港的加密借贷平台](https://coincodecap.com/crypto-lending-hong-kong)
*   [如何在 Uniswap 上交换加密？](https://coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 审查](https://coincodecap.com/a-ads-review)
*   [WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [本地比特币审核](/coinmonks/localbitcoins-review-6cc001c6ed56) | [加密货币储蓄账户](https://coincodecap.com/cryptocurrency-savings-accounts)
*   [什么是融资融券交易](https://coincodecap.com/margin-trading) | [成本平均法](https://coincodecap.com/dca)