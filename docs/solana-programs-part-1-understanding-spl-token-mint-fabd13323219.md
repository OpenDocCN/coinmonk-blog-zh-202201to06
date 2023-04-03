# 索拉纳计划第 1 部分:了解 SPL 代币厂

> 原文：<https://medium.com/coinmonks/solana-programs-part-1-understanding-spl-token-mint-fabd13323219?source=collection_archive---------2----------------------->

Solana token 程序([源代码](https://github.com/solana-labs/solana-program-library/tree/master/token/program/src))是执行最频繁的 Solana 智能合约之一。其程序 id:[tokenkegqfezyinwajbnbgkpfxcwubvf 9 ss 623 vq5d a](https://explorer.solana.com/address/TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA)

*   大多数用户部署的 Solana smart contracts(直接或间接)使用令牌程序来铸造/转移/刻录令牌(即 SPL 令牌)。例如，如果你的 Solana 项目是一个*去中心化交易所*、一个*稳定币*、一个 *ICO、*或一个*跨链桥*，你很可能依赖于 token 程序。
*   SPL 令牌类似于 ERC20/ERC721 令牌，但有一些棘手的…