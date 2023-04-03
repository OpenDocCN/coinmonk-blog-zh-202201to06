# 如何用熊猫来检验你的交易策略？

> 原文：<https://medium.com/coinmonks/how-to-backtest-your-trading-strategy-with-fees-using-pandas-8e5ba1278431?source=collection_archive---------1----------------------->

# 定义策略

利用你的交易经验和你在图表上看到的东西，你设法把你的交易策略总结成一些简单的系统规则。现在，您需要进入下一步，即自动化这组规则。这将允许你根据过去的数据和/或不同的市场来测试你的策略。为了本文的目的，让我们使用商品通道指数(CCI)来研究一个简单的策略:

*   当 CCI(100)穿过 100 时买入