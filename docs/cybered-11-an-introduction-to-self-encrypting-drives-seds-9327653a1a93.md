# CyberEd #11 自加密硬盘(sed)简介

> 原文：<https://medium.com/coinmonks/cybered-11-an-introduction-to-self-encrypting-drives-seds-9327653a1a93?source=collection_archive---------10----------------------->

SED(或自加密硬盘)是一种无需用户干预即可自动连续加密磁盘上数据的硬盘。这种加密是通过使用唯一的随机 ***数据加密密钥******(***[***【DEK】***](https://www.techopedia.com/definition/5660/data-encryption-key-dek#:~:text=Encryption%20Key%20(DEK)-,What%20Does%20Data%20Encryption%20Key%20(DEK)%20Mean%3F,created%20by%20an%20encryption%20engine.)***)***来实现的，驱动器使用该密钥来加密和解密数据。当数据写入驱动器时，首先用 DEK 加密。类似地，从磁盘读取的所有数据在发送到系统的其余部分之前都由同一个 DEK 解密。这意味着光盘上的所有数据始终都是加密的。要求 SED 创建一个新的 DEK 渲染所有…