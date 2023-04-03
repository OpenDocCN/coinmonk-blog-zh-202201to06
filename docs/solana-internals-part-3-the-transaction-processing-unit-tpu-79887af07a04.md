# Solana 内部第 3 部分:事务处理单元(TPU)

> 原文：<https://medium.com/coinmonks/solana-internals-part-3-the-transaction-processing-unit-tpu-79887af07a04?source=collection_archive---------3----------------------->

由于网络拥塞，Solana 最近经历了严重的性能下降。TPS(每秒处理的事务数)下降了几个数量级(从几千到几十个)。

从技术上来说，这个问题是由 Solana 中的性能错误引起的，特别是——事务处理单元 ( *TPU* )。在市场波动期间，机器人会大量喷洒重复的垃圾邮件，从而使 TPU 陷入困境。

这篇文章详细阐述了 TPU 的设计，并强调了一些复杂性。