# “加密货币钱包”，是什么？

> 原文：<https://medium.com/coinmonks/cryptocurrency-wallets-what-are-they-32ce0461eb66?source=collection_archive---------37----------------------->

## 除了区块链最糟糕的名字。

![](img/c9a4b3109114cde12a602cffe751e898.png)

Photo by [Tezos](https://unsplash.com/@tezos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当你试图解释一个新概念时，简化事情会有所帮助。然而，如果你简化得太多，你可能会遇到这样的问题，早期的简化已经把你逼到了一个角落，如果没有一个如此大的信息转储，你将无法走出这个角落，这将不可避免地破坏整个解释。我相信这就是加密货币“钱包”一词的由来。这个词唯一有意义的时候是，如果你目前深陷将比特币与美元进行比较的类比，这是一个非常流行(也很糟糕)的类比。

# 区块链交易

首先，让我们快速回顾一下基本区块链是如何工作的。我在*中稍微解释了这一点*在我之前的[中更详细“说真的，比特币是什么？”](/@flapjackslappack/seriously-what-is-bitcoin-3a758aa4d3c9)系列。如果你很难跟上，去看看吧！对于比特币，个人用户会制作一对密钥，分别称为私钥和公钥。它们就像是在线服务的用户名和密码，一个是共享的，另一个是保密的。理解这些键在数学上相互联系是很重要的。在以前的帖子中，我将这与弹道取证进行了比较，在弹道取证中，发射的子弹上的标记只会与那把枪完全匹配。如果你有枪，生产带有这些标记的新子弹很简单。相比之下，如果你只有子弹，制造一把能重现相同标记的枪就要困难得多。这些密钥的联系是相似的，因为公钥是从私钥派生出来的，从私钥到公钥要比反过来容易得多。

当用户想要接收比特币时，他们将共享他们的公钥，无论是谁发送交易，都会将交易发送到这个公钥。这就是接收比特币所需的全部内容。如果此人随后决定将它发送给其他人，他们必须在交易过程中同时使用私钥和公钥。这是一个需要理解的重要过程，因为你从来没有真正拥有单个比特币，而是你是唯一可以将交易发送给其他人的人。所以比特币的真正价值在交易中，交易完全由私钥控制。

![](img/6f65b87af4fcd52862a5675341abd554.png)

Photo by [Tarik Haiga](https://unsplash.com/@tar1k?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 匿名

如果你真的想，有可能只创建一对密钥。任何时候有人想给你汇钱，他们就把钱汇到这个公钥上，当你把钱汇到别处时，你就使用与之相关的私钥。然而，加密货币的一大卖点是匿名性和隐私性。第一次使用钥匙时，你可以确信没人知道你是谁。但是请记住，所有的交易都是公开可见的，如果您不小心泄露了您的公钥，任何人都可以回顾整个历史，并看到您每次参与的交易。因此，建议用户更频繁地创建新的一对，比如一次性手机。你永远不会留下这样的痕迹，如果一把钥匙与你联系在一起，你的其他交易就与你无关了。

![](img/860b8db780cd1e93914b1fc9874587c6.png)

Photo by [Mika Baumeister](https://unsplash.com/@mbaumi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 随机性

假设我们想参与我们的第一笔比特币交易。我们首先需要挑选一个随机数作为我们的私钥，然后通过一个单向函数“发射”它。单向函数就像弹道取证类比中的枪。这是一种将一个给定的数字转换成第二个数字的数学方法，如果我们有第一个数字，得到第二个数字是很容易的，而只从第二个数字得到第一个数字是极其困难的。我们应该使它容易记忆，但它必须只是数字，没有字母。假设你的生日是 1992 年 4 月 29 日，你曾经最喜欢的数字是 140，那么我们选 04291992140 (04，29，1992，140)作为我们的私钥，超级好记！我们通过一个单向函数激发它，它给出了:15302003251。现在我们有了自己的私钥和公钥！最终，有人发现这是我们的公钥，而我们在选择密码方面是出了名的糟糕。他们尝试了几次，最终猜出了我们的私钥！现在他们可以把我们的交易发给他们自己了，该死！

在这个领域保持不可预测是很重要的，因为计算机可以非常快地猜测大量的数字，在上面的例子中，仅仅知道我们的生日就可以将猜测时间从数千年缩小到几秒钟。所以要真正做到不可预测，我们需要一个随机数，而不是一个容易记住的数。我们发现一些软件会产生一个随机数，我们用这个作为我们的私钥。在生成它们之后，我们有几年没有使用它们，并且已经忘记了这个完全随机的数字…我们真的不走运！除非我们能猜出它，否则我们没有办法将此交易发送到任何地方。这肯定更安全，但更难记住。当然，我们可以把它写在笔记本上，当我们忘记带私人钥匙的时候就去查一下。

![](img/73d067bb72e206593f306b9e85fcd736.png)

Photo by [Florian Olivo](https://unsplash.com/@florianolv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 钱包

为了解决这个问题，如果我们有一个能为我们保存私有和公共密钥对的计算机程序会怎么样呢？更好的是，如果它为我们生成了私钥，这样我们就不用担心它们是随机的了。当我们需要它时，我们要求软件创建一个新的随机私钥，通过单向函数激活它，并保存与之相关联的结果公钥。如果我们稍后进行第二次交易，它甚至可以自动生成新的密钥来隐藏我们的身份，以防将来泄露。现在，让我们再增加一个特性:组合事务。假设我们想给我们的朋友发送 10 个比特币，但是我们只有 3 笔小额交易，两笔 3 比特币，一笔 4 比特币。这些加在一起构成了 10 个比特币，所以我们的钱包可以将这三个组合在一起，并一次性发送给我们的朋友。我们不需要对单个交易进行计数，也不需要找到正确的交易组合，我们的软件会为我们做这些。

我们刚刚描述的，是一个**加密货币钱包**！根据这一描述，很明显他们实际上并不持有任何资金。它们只是生成密钥，为您跟踪这些密钥，并在交易期间管理它们的使用。在物理领域，钱包用于保存我们的实际资金，当加密货币不是有形的时，这是一个令人困惑的类比。它真的应该被称为类似于关键经理的东西。当然，这不太直观，但区块链不是直观的，糟糕的类比会使理解它们更加困难。

![](img/7a6bcdfba7186400842f452d60559724.png)

Photo by [Franck](https://unsplash.com/@franckinjapan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 冷 vs 热

不过，钱包没必要这么复杂。之前我说过我们可以把钥匙写在一张纸上，这仍然是一个钱包，叫做“纸钱包”。如果你有很好的记忆力，那么你可以记住钥匙，创造一个“大脑钱包”。实际上，大多数人使用的软件钱包与之前描述的类似。另一种常见的钱包是“硬件钱包”。这就像在文本文档中键入关键字，并将其保存到拇指驱动器中。密钥不是储存在你电脑的程序里，现在它们在你的 u 盘里(一个硬件)。不管你遇到什么类型的钱包，你可能会听到更多的形容词:*热*或*冷*。

冷热钱包的区别很简单。一个热的钱包意味着它在某种程度上与你个人之外的世界相连，而一个冷的钱包则不然。让我们考虑最简单的钱包，一个纸钱包。一个冰冷的纸钱包会把你的钥匙写在一张纸上，放在你家的保险箱里。你是唯一有可能接近它的人。现在把同样的一张纸放在你的桌子上，任何路过的人都可以捡起来或者偷偷看一眼。它现在是一个热门的纸钱包。一般来说，热门钱包以安全性换取可访问性。如果你只需要看着桌子上的数字，而不是走到你的保险箱，输入代码，然后走回来，发送比特币会更容易。同样，如果你有一个软件钱包，并且你的电脑连接到互联网，它就是一个热门钱包。如果你电脑上的恶意软件允许黑客远程访问你的电脑，他们可以看到并复制你的密钥。你的同一台电脑，但没有互联网，将是一个冰冷的钱包(假设你的电脑在你的家里，有密码保护)。

如果你有兴趣了解更多关于加密货币或区块链的话题，请给我发消息！谢谢你。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Bookmap 点评](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [KuCoin 评论](https://coincodecap.com/kucoin-review)