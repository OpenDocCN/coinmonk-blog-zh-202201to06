# Solana 程序第 3 部分:理解 Metaplex 令牌元数据

> 原文：<https://medium.com/coinmonks/solana-programs-part-3-understanding-metaplex-token-metadata-3cafde284d72?source=collection_archive---------7----------------------->

metaplex-token-metadata 程序是 Solana 上 NFT 的主干。

想象你想为你的艺术创作一个 NFT，基本上你需要:

1.  将你的作品(数字化)上传到永久存储器
2.  在 Solana 上为你的作品创建一个标记造币厂(即一个唯一的标识符)
3.  铸造一枚属于你钱包的代币

在第二步中，信物造币厂是特殊的——它的供应只有一个，并且必须与你的艺术信息相关联(例如…