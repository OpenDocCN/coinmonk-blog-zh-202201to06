# 当你想要一枚用本国货币买不到的硬币时该怎么做——初学者指南

> 原文：<https://medium.com/coinmonks/what-to-do-when-you-want-a-coin-that-you-cant-buy-with-your-native-currency-a-beginner-s-guide-6b448c82f194?source=collection_archive---------40----------------------->

![](img/2382ec32cc2789c44a359e084fb39da8.png)

在我的加密之旅的早期，我对 altcoin DeFiChain (DFI)产生了兴趣，但它不是在我的 go-to exchange(双子座)上提供的。我听说它在 KuCoin 上可用，但在我注册后，我意识到我不能像在其他一些交易所那样，将我辛苦赚来的美元直接存入贸易账户。我需要用另一种加密货币购买 DFI。

这对我提出了新的挑战。当时我不想交易掉我的任何股份，所以我必须在一个交易所用美元购买 crypto，把它转移到 KuCoin，用我最近转移的 crypto 购买 DFI，然后把 DFI 转出 KuCoin。这个过程不仅仅包括从我的银行账户转账和购买我想买的东西，还包括更多的步骤，但它看起来非常简单。但是当我想得更多的时候，我意识到有很多事情我需要考虑。我在这里列出了其中的一些:

*   我需要做两笔交易来买 DFI，而不是一笔。因此，最大限度地降低交易费用符合我的最大利益。
*   我会在两个不同的交易所进行交易，所以我也需要考虑转让费。
*   加密货币是不稳定的，我不能立即购买 DFI，因为我需要采取所有的步骤。如果我不小心的话，DFI 的价格变化和传输的密码会影响我在交易结束时收到多少 DFI。

许多投资 crypto 的人发现自己处于这样的情况。这篇文章描述了我购买 DFI 的经历，但是关于费用计算和现货价格变化的原则可以适用于任何类似的情况。先说费用。

# 费用

我第一次买 DFI 的时候用比特币(BTC)作为兑换货币。BTC 和 DFI 都非常不稳定，但是为了计算费用，让我们假设在我转换的时候两个硬币的价格都没有变化。考虑到这个假设，我们可以使用下面的等式来确定交易的费用:

W + X + Y + Z = T 以下为真:

*   w 是与购买我的转换加密(BTC)相关的费用。
*   x 是将我的转换密码转移到 KuCoin 的相关费用。
*   y 是使用 BTC 购买 DFI 的相关费用。
*   z 是将我的 DFI 转出库币的相关费用。
*   t 是我购买 DFI 的总费用。

我通过 Gemini API 使用制造商订单购买了 BTC。当我启动交易时，通过 Gemini API 运行的制造商 BTC 订单的交易费用固定在总交易金额的 0.1%。

Gemini 每月允许 10 次免费取款，所以我可以免费将我的 BTC 转移到 KuCoin。

我用我的 BTC 在库科恩买了 DFI。当我发起那笔交易时，KuCoin 上的接受者和制造者订单费用都被固定在交易总额的 0.1%。

最后，我从库科恩撤回了 DFI。当时，KuCoin 对所有 DFI 取款收取 0.1 DFI 的统一费用。

记住以上内容，我们可以将特定的值代入前面给出的等式，以确定我为转换支付的总费用。以下是我购买 DFI 的费用:

**(0.001 x A)+0+(0.001 x(A-(0.001 x A)))+0.1D = T**以下为真:

*   a 等于总交易金额。
*   d 是交易时以美元计的 DFI 成本。
*   t 是我购买 DFI 的总费用。

你的费用结构可能与这个例子相似，也可能不相似，这取决于你使用的交易所，但是事先确定所有费用以避免为你的加密支付过多费用是有帮助的。

# 转换期间现货价格变化的影响

我前面提到过，我们的两个例子硬币，BTC 和 DFI，都是不稳定的。在兑换过程中——在你购买 BTC 之后，但在你购买 DFI 之前——两种硬币的现货价格的变化会改变你在兑换过程结束时获得的 DFI 的总价值。大致来说，价格的变化可能对你有利，也可能对你不利，这取决于在从你的本国货币兑换成 DFI 货币的过程中，硬币价格相对于彼此以及相对于你的本国货币的变化。

令人担忧的是，在兑换上可能会有一个**负面影响**，这意味着你得到的 DFI 总价值低于你支付的本币价值。然而，也有可能**对价值没有影响**，甚至有**正面影响**，这意味着你得到的 DFI 总价值超过了你支付的本国货币价值。

# 如何在转换期间最小化现货价格的变化

确定你可以利用上述现货价格的变化为自己谋利的情况是困难和令人困惑的。此外，你必须把握市场时机，对价格变化做出短期预测。这些类型的预测是不可靠的——你可能会走运，但也可能会赔钱。因此，最大限度地降低现货价格变动的影响变得更加容易和简单。这可以通过尽可能快地进行交易来实现，以最大限度地减少价格大幅变动的可能性。你也可以使用类似系绳(USDT)的稳定币进行转换(你可以在 KuCoin 上使用 USDT 购买 DFI)。

对交易密码感兴趣吗？使用 [**此链接**](https://gemini.com/share/vdp4aeat8) 注册 Gemini，当你在开户后 30 天内买入或卖出 100 美元或以上，我们都将获得 10 美元的比特币。详情见条款。

使用此 [**推荐链接**](https://www.kucoin.com/ucenter/signup?rcode=rPEZUVW) 注册 KuCoin，赢取 USDT。详情见条款。

我是一个密码爱好者。我不是财务顾问，我所说的任何内容都不构成财务建议。我所做的所有陈述都是观点，未经进一步研究，不应被视为事实。

点击这里查看我的链接树[T5。](https://linktr.ee/Dreiberg)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [如何购买 Monero](https://coincodecap.com/buy-monero) | [IDEX 评论](https://coincodecap.com/idex-review) | [BitKan 交易机器人](https://coincodecap.com/bitkan-trading-bot)
*   [CoinDCX 评论](/coinmonks/coindcx-review-8444db3621a2) | [加密保证金交易交易所](https://coincodecap.com/crypto-margin-trading-exchanges)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [Bookmap 评论](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   [如何在 FTX 交易所交易期货](https://coincodecap.com/ftx-futures-trading) | [OKEx vs 币安](https://coincodecap.com/okex-vs-binance)
*   [CoinLoan 审查](https://coincodecap.com/coinloan-review) | [YouHodler 审查](/coinmonks/youhodler-4-easy-ways-to-make-money-98969b9689f2) | [BlockFi 审查](https://coincodecap.com/blockfi-review)