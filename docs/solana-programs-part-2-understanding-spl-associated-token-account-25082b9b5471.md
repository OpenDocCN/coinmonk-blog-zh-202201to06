# Solana 计划第 2 部分:了解 SPL 联合令牌帐户

> 原文：<https://medium.com/coinmonks/solana-programs-part-2-understanding-spl-associated-token-account-25082b9b5471?source=collection_archive---------3----------------------->

继[第 1 部分:了解 SPL 代币厂](/coinmonks/solana-programs-part-1-understanding-spl-token-mint-fabd13323219)之后，本文介绍另一个流行的官方 Solana 智能合约 [SPL 联合代币计划](https://github.com/solana-labs/solana-program-library/tree/master/associated-token-account/program/src)的技术细节。

该程序提供了一种从钱包地址管理用户令牌帐户的便捷方式。其节目 id:[atokengpvbdgvxr 1 b 2 hvzbsiqw 5 xwh 25 eftnslja 8 knl](https://explorer.solana.com/address/ATokenGPvbdGVxr1b2hvZbsiqW5xWH25efTNsLJA8knL)

这个想法是从用户的钱包地址和代币厂创建一个 **PDA** (即程序衍生账户)。有两个主要的好处: