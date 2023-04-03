# 在我们的 NFT 中有效地存储 IPFS 散列

> 原文：<https://medium.com/coinmonks/efficiently-storing-ipfs-hashes-in-our-nft-2ff972590c8c?source=collection_archive---------7----------------------->

![](img/923cbc3c5ddd0c8f4fbd3852f735bb7f.png)

21 毫米像素[合同](https://etherscan.io/address/0x7dd7aa4b560692c882d982312c0b53b24c51523a#code)的独特之处之一是它能够以高效的方式有效地存储图像位置数据。许多合同使用字符串存储来存储位于 T2、IPFS 或其他地方的文件或数据的链接。存储字符串是低效的，因为字符串使用 UTF-8 编码(每个字符需要一个字节)，并以其 256 位长度为前缀，即使是最短的字符串也需要 64 个字节的存储，典型的 IPFS [cidV1 哈希](https://docs.ipfs.io/concepts/content-addressing/#identifier-formats)至少需要 3 个字节。

在 [21MM 像素](https://21mmpixels.com) NFT 合约中，我们使用了一个由两个字节 30 组成的结构，一个 uint16 用于读取字节 30 的位大小，一个 bytes1 用于表示编码，一个 uint8 用于存储有关图块状态的信息，以适应两个存储槽中所需的所有信息。两个字节 30 的存储槽比 IPFS 内容标识符或 [Arweave](https://www.arweave.org/) 事务 ID 所需的要大，但是根据以太坊虚拟机的工作方式，一旦我们超过 32 字节标志，我们就要为 64 字节的存储支付汽油，所以我们还不如将来证明(有大量额外的字节 1 标识符可用于表示将来的编码)。

为了在存储信息以链接到令牌(又名“瓦片”)持有者希望为其[21 兆像素](https://21mmpixels.com)瓦片设置的图像时节省汽油成本，我们创建了视图函数来将 IPFS cidV1 哈希和 Arweave 事务 ID 转换为字节数组，以便与 21 兆像素 NFT *setImage* 函数一起存储，以及以人类可读(且可用)的形式显示存储的 IPFS 哈希和 Arweave 事务 ID 的视图函数。

*cidv1ToBytes* 和 *arweaveTxIdToBytes* 视图函数类似，都是以字符串作为输入。在引擎盖下， *cidv1ToBytes* 使用 Base32 编码(每个字母 5 位)，而 *arweaveTxIdToBytes* 使用 Base64URL 编码(每个字母 6 位)。每个函数首先从输入字符串创建一个字节数组(*bytes memory bytes array = bytes(input)*)。然后，这些函数遍历该数组，将 UTF-8 字符串字符转换为 uint8(实质上将该字符转换为其 ASCII 代码)，然后从该 ASCII 代码转换为 Base32 或 Base64URL 等效的 uint 8(ASCII 中的“a”是 65，Base32/Base64URL 中的“a”是 0)。我们使用整数数学进行这种转换，因为它比使用实数组更简单

Base32/Base64 字符的新 uint8 表示( *thisByte* )使用函数*bytes30(uint 240(this byte))*转换为 bytes 30(在我们的代码中为 *tempBytes* )。此 *tempBytes* 左移，使得字符串的第一个字符出现在最左边的位置(对于 Base32，此左移为前 48 个字符的*tempBytes<<(5 *(47—I))*，其中 *i* 表示字符，字符串的第一个字符为 *i* = 0)。然后，我们获取左移的*临时字节*，并对摘要使用按位 or 运算符(|)，例如， *digest1 = digest1 |临时字节*。由于*摘要 1* 和*摘要 2* 已经被初始化为字节 30，这具有将每个*临时字节*放置在其适当位置而不影响先前添加的字符的效果。

对于每个视图函数， *digest1* 和 *digest2* 被返回，表示两个字节 30 变量，以及*大小*，一个 uint16，指定两个摘要之间用于编码的位数，以及一个字节 1，指定编码(0x98 或 0x66 用于 Base32 IPFS 散列，0x01 用于 Arweave 事务 id)。

在以后的文章中，我将介绍如何将存储的信息转换回 IPFS 散列和 Arweave 事务 id 以供显示。如有任何问题，请随时联系我们。