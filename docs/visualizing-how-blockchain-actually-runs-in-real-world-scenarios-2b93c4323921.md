# 想象区块链在现实世界中是如何运行的。

> 原文：<https://medium.com/coinmonks/visualizing-how-blockchain-actually-runs-in-real-world-scenarios-2b93c4323921?source=collection_archive---------59----------------------->

以太坊使用密码术将文本从语言转换成散列比特，以保持数据的安全和工作。它使用或多或少类似于 SHA 算法的 Keccak256 算法来计算数据的散列函数。哈希算法是一种将数据计算成唯一哈希的函数。

现在，每当要创造新的比特币时，就会成立一个矿工团队，用暴力方法解决复杂的问题，并提供问题的解决方案。作为回报，他们会得到金钱上的回报。

现在，为了举例说明这个过程实际上是如何工作的，让我们来看看一个演示模块——[https://andersbrownworth.com/blockchain/block](https://andersbrownworth.com/blockchain/block)

在这里，如果我们要开采一个比特币，区块已经提供给我们了。假设我们要找出前面有 4 个零的哈希函数。我们基本上必须猜测 nonce 值。

随机数是一个用来寻找区块链问题解决方案的数字。它也可用于定义账户/地址的交易号。

我们必须破解一个值，这样在我们散列的开始有 4 个零。如果该值最终被破解，我们单击“我的”,可以看到我们的哈希已经自我挖掘。

现在，让我们以链的形式来举例说明这是如何工作的—【https://andersbrownworth.com/blockchain/blockchain

如果我们对 nonce 或数据值进行任何更改，我们可以注意到更改后的数据块变为无效或红色。当有人试图破坏存储在区块链的值时，就会发生这种情况。通过这种方式，它会立即被纠正并从列表中删除，以避免进一步的中断。

现在，让我们以一个分布式系统的形式来举例说明这是如何工作的——https://andersbrownworth.com/blockchain/blockchain

我们假设不同的对等点表示不同的人，这些对等点中的块表示那个人的事务。类似地，如果观察到从改变 nonce 的值到输入任何错误数据的任何改变，则块和其他块的值变得无效，并且该特定对等体被从链中移除。

在令牌中，我们可以看到交易细节是否被伪造或篡改，块不再具有任何进一步的价值。

这就是我们如何实际可视化和感知这一令人惊叹的技术背后实际发生的事情，以及它如何帮助我们从今天发生在 Web 2 环境中的大漏洞中拯救自己。内容受到了免费代码营的 Youtube 教程的启发，观看视频了解更多细节—[https://www.youtube.com/watch?v=gyMwXuJrbJQ](https://www.youtube.com/watch?v=gyMwXuJrbJQ)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [用信用卡购买密码的 10 个最佳地点](https://coincodecap.com/buy-crypto-with-credit-card)
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [Bybit vs 币安](https://coincodecap.com/bybit-binance-moonxbt)
*   [阿联酋 5 大最佳加密交易所](https://coincodecap.com/best-crypto-exchanges-in-uae) | [SimpleSwap 评论](https://coincodecap.com/simpleswap-review)
*   购买 Dogecoin 的 7 种最佳方式
*   [最佳期货交易信号](https://coincodecap.com/futures-trading-signals) | [流动性交易所评论](https://coincodecap.com/liquid-exchange-review)
*   [用于 Huobi 的加密交易信号](https://coincodecap.com/huobi-crypto-trading-signals) | [Swapzone 审查](/coinmonks/swapzone-review-crypto-exchange-data-aggregator-e0ad78e55ed7)