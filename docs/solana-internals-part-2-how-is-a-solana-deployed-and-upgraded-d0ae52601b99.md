# Solana 内部第 2 部分:如何部署和升级 Solana 程序

> 原文：<https://medium.com/coinmonks/solana-internals-part-2-how-is-a-solana-deployed-and-upgraded-d0ae52601b99?source=collection_archive---------1----------------------->

当您将智能合同部署到 [Solana Mainnet](https://explorer.solana.com/) 时，Solana 内部会发生什么？Solana 程序可以修改或关闭吗？如何升级一个 Solana 程序？谁有权更改索拉纳计划？

这篇文章关注的是 Solana 程序的可升级性，并强调了一些复杂性。

以下是一些笔记:

*   ***可以修改和升级*** *(默认)*
*   *[*bpfloardupgradeab1e*](https://explorer.solana.com/address/BPFLoaderUpgradeab1e11111111111111111111111)*装载机是所有者* …*