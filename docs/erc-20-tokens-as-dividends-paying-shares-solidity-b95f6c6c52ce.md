# ERC-20 代币作为派息股(实实在在)

> 原文：<https://medium.com/coinmonks/erc-20-tokens-as-dividends-paying-shares-solidity-b95f6c6c52ce?source=collection_archive---------1----------------------->

我最近挑战自己，用 solidity 在以太坊上实现了一个支付股息的 ERC20-token。我正在开发一个 dapp，它也将使用相同的 ERC20-token 进行治理(更多信息请点击[这里](/@alberto.molina.arribere/dapp-governance-using-erc-20-tokens-solidity-9953c2e82831))，这意味着 token 所有者可以与传统股东相关联。

在集中式计算中，这将是一个相对容易的任务，但对于分散式应用程序，您将面临几个挑战，我将列出其中一些挑战，并解释我提出的解决方案。