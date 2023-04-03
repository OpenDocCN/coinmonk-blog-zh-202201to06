# 以太坊虚拟机(EVM)。它是如何工作的？(第二部分)

> 原文：<https://medium.com/coinmonks/ethereum-virtual-machine-evm-how-does-it-work-part-2-4198401d2a11?source=collection_archive---------5----------------------->

这篇博客是博客系列“以太坊虚拟机(EVM)如何工作？”的第二部分，也是最后一部分。如果您想阅读第 1 部分，请点击此链接:

[以太坊虚拟机(EVM)。它是如何工作的？(第一部分)|作者阿尔贝托·莫利纳| 2022 年 6 月| Medium](/@alberto.molina.arribere/ethereum-virtual-machine-evm-how-does-it-work-part-1-81f65bedbe8f)

# **内部通话**

如果协定的函数调用同一协定中的另一个函数，则易失性堆栈和内存保持不变，因为 EVM 实例将保持不变。