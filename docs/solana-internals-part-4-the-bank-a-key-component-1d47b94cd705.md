# 索拉纳内部第 4 部分:银行——一个关键的组成部分

> 原文：<https://medium.com/coinmonks/solana-internals-part-4-the-bank-a-key-component-1d47b94cd705?source=collection_archive---------3----------------------->

继[第 3 部分:TPU](https://blog.soteria.dev/solana-internals-part-3-the-transaction-processing-unit-tpu-79887af07a04) 之后，本文将详细介绍`**bank**`模块，它是索拉纳区块链的核心组件。

# 什么是银行？

`bank` 模块的重要性不言而喻:

> 它管理所有帐户和程序的状态，执行链上程序，并跟踪它们的进度。

在高层次上，一个`bank`与单个领导者产生的块相关，并且每个`bank`(除了 genesis bank)指回一个父`bank`。