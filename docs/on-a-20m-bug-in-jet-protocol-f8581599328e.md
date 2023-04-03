# 关于 Jet Protocol 中一个价值 2000 万美元的漏洞

> 原文：<https://medium.com/coinmonks/on-a-20m-bug-in-jet-protocol-f8581599328e?source=collection_archive---------7----------------------->

最近，查理·尤披露了 Jet 协议中的一个漏洞(请参见[推特](https://twitter.com/CharlieYouAI/status/1508842093514567687))。如果利用这个漏洞，Jet 用户的资金将损失 2000 万美元。幸运的是，Jet 在任何用户受到影响之前就对其进行了修补。

Soteria 团队在 Jet-v1 的代码中发现了一些棘手的问题，并在披露后不久与查理进行了讨论。实际情况表明，该漏洞有不同的原因(Charlie 未预料到)。以下是总结:

*   原因实际上是**一个未验证的输入** **账户**，而它本可以很容易地被 Soteria Auto Auditor】检测到