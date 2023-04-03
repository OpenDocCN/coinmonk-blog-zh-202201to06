# 索拉纳计划第 4 部分:Metaplex 糖果机——它是如何工作的？

> 原文：<https://medium.com/coinmonks/solana-programs-part-4-metaplex-candy-machine-how-does-it-work-a27d7a133fad?source=collection_archive---------0----------------------->

Metaplex 糖果机是 NFT 在索拉纳最受欢迎的智能合同之一。最近，它甚至实现了用于检测和征税机器人的[复杂逻辑。](https://twitter.com/brianlong/status/1521213171872108544)

[糖果机程序](https://github.com/metaplex-foundation/metaplex-program-library/tree/master/candy-machine/program)内部是如何工作的？它的预期用例及依赖关系是什么？它如何检测机器人？本文将详细阐述这些技术细节。

![](img/9d7ad9e4da3306b6f21e242d7550d897.png)

[Okay Bear #1756](https://opensea.io/assets/solana/C2sH8dCHYPTUpEU6ygBTGfRmpCxE2xfBRAffscFKG4T8) NFT