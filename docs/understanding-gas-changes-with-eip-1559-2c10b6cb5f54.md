# 用 EIP-1559 了解气体变化

> 原文：<https://medium.com/coinmonks/understanding-gas-changes-with-eip-1559-2c10b6cb5f54?source=collection_archive---------26----------------------->

以太坊社区用 EIP-1559 改变了汽油费的计算方式。我会尽量简化这些变化，这本身就不是一件容易的事情。如果你对计算油费的新方法感到困惑，你肯定不是唯一一个。

让我们先回顾一下过去如何计算汽油费——

**气体—** 气体是以太量的术语，以太是以太坊的本地加密货币，网络需要用户与网络交互。这些费用用于补偿以太坊矿工验证交易所需的能量，并通过使恶意用户向网络发送垃圾邮件的成本过高来为以太坊网络提供安全层。

**Gas Cost —** 交易使用的计算量和存储量。如果一次交易是一次公路旅行，这是从 A 地到 b 地所需的汽油总量。

**天然气价格—** 每单位天然气的成本。这是你旅途中每加仑汽油的价格。这由发送者设置。

**Gas Limit —** 您希望为执行事务而分配的计算资源的上限。因此，它的最大数量的天然气，你愿意花，任何超过你的交易被还原。

所以用户最终要支付的天然气费用是—

> 交易费用=气成本*气价

L 伦敦叉和 EIP-1559

2021 年 8 月，引入了一种新方法。它演变成一个更加混合和复杂的系统。以前你只监控汽油价格，但现在有多个参数需要跟踪。让我们深入研究一下—

**基本费用—** 这是您必须为完全执行交易支付的每单位天然气的基本费用。这由以太网决定，并基于最近确认的块的内容。根据新块有多满，`Base Fee`会自动增加或减少。该费用随后被烧掉。

**最大优先费用—** 这是发送者添加的可选小费，直接发给矿工。添加此矿工提示是为了将您的交易包含在下一个块中。

**最高费用—** 您愿意为将要执行的交易支付的绝对最高费用。为什么要设置此价格—您交易的最低天然气价格是基本费用，但在交易执行过程中可能会发生变化。在这种情况下，您的事务可能会被卡住。因此，最好设定最高费用，假设基本费用可能会波动。确定这一点的简单方法—

> 最高费用= (2 *基本费用)+最高优先费用

最高优先费用(矿工小费)根据您为交易设置的最高费用进行调整。

**气体限制—** 与之前相同。

**天然气成本—** 与之前相同。

> 交易费=(基本费+最高优先权费)*气费

你不必为每一笔交易都计算所有这些，你可以使用如下一些有用的气体估算器

[](https://ethgasstation.info/) [## 实时气体使用

### 这是什么网站？计算器天然气价格建议其他常见问题

ethgasstation.info](https://ethgasstation.info/)  [## 以太气估计器

### 不用多付钱就能进入下一个街区。

www.blocknative.com](https://www.blocknative.com/gas-estimator) 

Block native 有一篇更深入的文章谈到这一点——https://www.blocknative.com/blog/eip-1559-fees

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取秘密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)