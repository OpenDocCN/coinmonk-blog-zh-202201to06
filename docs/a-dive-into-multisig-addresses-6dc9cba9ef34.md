# 对多重签名地址的探究

> 原文：<https://medium.com/coinmonks/a-dive-into-multisig-addresses-6dc9cba9ef34?source=collection_archive---------17----------------------->

![](img/f8dbba0d1f1e888c9ff5ab0ee233f041.png)

# 介绍

简单地说，多重签名地址是需要从这些地址中花费多于一个密钥的地址。数千年来，多重签名的概念已经在许多意识形态、民族、种族和/或企业中使用。作为一个例子，多重签名已经被用来保护保存最昂贵的圣徒遗物的地下室的安全。修道院的院长只会给修道士 1/2 特殊遗物的钥匙。结果，没有一个僧侣能够接近并占有这些遗物。

传统业务中的“关键人物风险”一词指的是一家公司过于依赖一个人来发展壮大。在处理资金时，加密货币公司以外的许多公司都容易出现这种风险。幸运的是，多重签名比特币地址提供了一种管理这种风险的机制，它没有将管理资金的唯一责任交给个人。

# 什么是多重签名地址？

多签名地址是一种比特币地址，允许您作为一个群体管理资金。一旦您要求两个或更多人连同您的加密签名一起释放其中包含的资金，就会发生这种情况。一旦你想从钱包里寄钱，交易就形成并签署了。通过对交易进行数字签名，您声称拥有钱包中资金的所有权。要签署交易，单签名(又名“基本”)比特币钱包只需要一个签名。

Multisig 是 multi-signature 的缩写，顾名思义，这种钱包需要一个或多个签名才能签署交易。multisig 钱包是由两个或两个以上的共付人共享的钱包。签署交易所需的签名数量将少于或等于共付额，这取决于钱包的类型。举个例子，一个由两个共付人共享的 2-of-2 multisig 钱包将迫使两个签名签署一项交易。在三个共付人共享的 2/3 multisig 钱包中，至少需要三个共付人中的两个才能签署交易。

# 多重信号地址的起源

比特币有三种核心地址格式:P2PKH、P2SH 和 bech32。P2SH 被认为是多重信令地址的发起者。Gavin Andresen 提出了 P2SH 地址。它们还可以用作多重签名地址等。该概念于 2012 年 3 月通过 BIP16 推出。2012 年 4 月，BIP16 发布一个月后，P2SH 地址被添加到比特币中。

在此之前，比特币 P2SH 尚未投入使用，但这并不意味着在引入 P2SH 地址之前不可能生成多签名地址。这是可行的，但必须极其简单地完成，而且没有常规的、公认的程序。

历史上第一次，在块 170052 中的多签名地址接收交易(2012 年 3 月 7 日)。342 ftsrcvfhfceffbuz 4 xwbeqndw 6 bguey。然而，该事务是在不遵守 BIP16 标准的情况下创建的，但是它遵守 BIP13 标准(以“3”开头)。

# 多信令地址是如何工作的？

假设我们有一个金库，需要不止一把钥匙才能打开并花掉里面的资金。这是 multisig 地址工作原理的简单说明。在多重签名地址的情况下，您可以决定打开保险库(花费资金)所需的钥匙数量。例如，可能有一个 2/3 的 multisig，其中总是需要两个密钥来花费地址中的资金。我们还可以有一个 n-of-m 的 multisig 地址，其中需要 m 个密钥中的 n 个密钥来签署交易，然后才能在该地址花费资金。示例包括二选二、三选二、五选三、七选五等。

他们是如何工作的？例如，使用 2-of-3 multisig，它是用 Bob、Alice 和 Carol keys 设置的。三方中的两方将被要求发送交易。为了进行支付，Bob 可以创建一个交易并用他的密钥签名。这称为事务请求。然后，他可以将该事务发送给 Alice 或 Carol，让他们中的任何一个用他们的密钥签名。一旦签名，他们中的任何一个将签名的事务发送回 Bob 以完成事务。

# 为什么要使用多重地址？

所有共付人都可以看到钱包中的资金和交易。要从钱包中转移资金，必须有一个或多个共付人签署交易。这一功能增加了您资金的安全性。

如果出现使您丧失能力的医疗紧急情况，您的亲人将无法获得在这种情况下可能需要的现金。此外，由于人们未能为最糟糕的情况做好准备，数百万美元的比特币已经丢失。multisig 钱包可以保证即使您不在或不在，您的资金也可以被访问，尽管这取决于(这在 2/2 multisig 钱包中似乎是不可能的。

我们还可以使用 multisig 地址进行众筹，因为项目需要资金来启动。在这种情况下，multisig 地址可用于托管服务，该服务持有其中一个密钥，项目持有 2-of-2 multisig 中的最后一个密钥。当项目启动事务时，如果项目满足某些要求和/或里程碑，服务可以提供第二个密钥。在这里，将会有一个检查和平衡，并且对项目过程有贡献的每个人都可以监控项目进度。

# 结论

我们生活在一个信任已经成为谬误的世界，每个人总是在寻找一种方法来为自己的利益提供一个信任系统。人们不愿意一起做生意，因为害怕其中一个合伙人会随着生意的增加而消失，夫妇们更喜欢有单独的账户来管理他们的资金，因为他们的配偶很谨慎。这并不意味着 multisig 地址完全解决了这个问题，但它有助于通过在可能信任或不信任彼此的不同方之间带来透明度和更好的资金管理来缓解这些问题。

在我的下一篇文章中，我将讨论如何使用比特币 cli 创建多签名地址

# 参考

1.  https://en . bitcoin . it/wiki/Multi-signature #:~:text = Multi % 2d signature %20(Multi SIG)% 20 指% 20 个比特币% 20 中的% 20 个% 20 多人。
2.  https://www.quora.com/How-does-a-multisig-wallet-work
3.  [https://www . bit coin . com/get-started/shared-multisig-bit coin-wallet/](https://www.bitcoin.com/get-started/shared-multisig-bitcoin-wallet/)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [支持卡审核](https://coincodecap.com/uphold-card-review) | [信任钱包 vs 元掩码](https://coincodecap.com/trust-wallet-vs-metamask)
*   [Exness 回顾](https://coincodecap.com/exness-review)|[moon xbt Vs bit get Vs Bingbon](https://coincodecap.com/bingbon-vs-bitget-vs-moonxbt)
*   [如何开始通过加密贷款赚取被动收入](https://coincodecap.com/passive-income-crypto-lending)
*   [BigONE 交易所评论](/coinmonks/bigone-exchange-review-64705d85a1d4) | [电网交易 Bot](https://coincodecap.com/grid-trading)
*   [氹欞侊贸易评论](https://coincodecap.com/anny-trade-review) | [CoinSpot 评论](https://coincodecap.com/coinspot-review)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [收购 AXS](https://coincodecap.com/buy-axs-token)