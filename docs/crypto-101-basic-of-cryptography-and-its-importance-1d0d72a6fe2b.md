# 密码 101:密码学的基础及其重要性。

> 原文：<https://medium.com/coinmonks/crypto-101-basic-of-cryptography-and-its-importance-1d0d72a6fe2b?source=collection_archive---------59----------------------->

![](img/80c9fe7622b46e409b70f2578150c9be.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我开始的这一系列故事将深入探讨我作为一个行业新手所投入的话题。CRYPTO101 系列源于我在第一篇博客[*——我在 CRYPTO、NFT 和元宇宙*](/@bnelsonsep3/my-education-and-connection-journey-on-nft-crypto-and-the-metaverse-349def7419c7) *的世界中的教育和联系之旅。*

你能想象一个数字时代吗？在这个时代，网络安全正变得越来越令人担忧，特别是当我们在网上存储越来越多的个人和私人信息时。如果你的答案是肯定的！密码术将减轻你的信任问题。

# 什么是密码学？

密码学是一门使用数字、单词和其他符号对信息进行编码的艺术，这样信息就可以被其他人阅读。我们用来描述这种艺术的语言叫做“密码学”。从第一台无线电发射机的发明到互联网的发展，密码学已经影响了人类努力的每一个领域。

它的目的是产生和传递信息。它可用于向计算机发送信息、加密信息、启用加密技术来防止信息被截获、保护隐私以及为消息提供安全通道。

# 密码术是如何工作的？

在密码学中，加密消息被编码为一个数字、一个单词或一系列数字、单词或符号。这些数字或单词，或者一组数字、单词或符号，有时被称为“密钥”。密钥用于加密或解密信息。一个密钥用于加密，另一个密钥用于解密。

在一个系统中，数据的机密性、完整性和可用性，以及真实性和不可否认性是至关重要的。当有效应用时，加密技术可以帮助提供这些保证。传输中的数据和静态数据都可以使用加密技术来保密和保护。它还可以通过验证发送者和接收者来防止抵赖。

# 不同的加密方法

有三种主要的美国国家标准与技术协会(NIST)认可的加密算法，它们通过所使用的加密密钥的数量或类型来区分。以下是:

**哈希函数**

加密哈希函数是一种算法，它采用任意数量的数据输入(凭据)并创建固定大小的加密文本输出，称为哈希值，或简称为“哈希”，然后可以保存该哈希值而不是密码本身，并随后用于验证用户。

加密哈希函数的基本功能不包括密钥的使用。通过一个单向过程，这个函数从大量数据中生成一个微小的摘要或“哈希值”。哈希函数通常用于生成密钥管理的构造块，并提供安全服务，例如:

生成消息认证码(MAC)以提供源和完整性认证服务，压缩消息以生成和验证数字签名

密钥建立算法中的密钥生成

产生确定性随机数

**对称密钥算法**

在对称密钥算法中，密钥在两个系统之间共享。这可能是一个问题。您必须设计一种方法，将密钥分发给所有必须使用对称密钥技术加密或解密数据的系统。向所有计算机手动分发密钥是一项耗时的工作。这有时只能通过从中央位置复制密钥来实现。你可以想象这有多不方便。

对称密钥技术，也称为秘密密钥算法，改变数据，使其在没有秘密密钥的情况下非常难以读取。

因为它同时用于加密和解密，所以被称为对称密钥。一个或多个授权实体通常可以访问这些密钥。对称密钥算法用于以下目的:

通过使用同一密钥加密和解密数据来保持数据的保密性。

为源和完整性认证服务提供消息认证码(MAC)。该密钥用于生成 MAC，随后对其进行验证。

在密钥建立过程中创建密钥

产生确定性随机数

**非对称密钥算法**

非对称密钥算法，通常称为公钥算法，用于克服对称密钥算法无法解决的两个问题:密钥分发和不可否认性。前者有助于解决隐私问题，而后者有助于解决真实性问题。

这些目标通过非对称操作的公钥算法来实现，也就是说，一个密钥被分成相应的两半，一个公钥和一个私钥。

非对称密钥算法，通常称为公钥算法，使用成对的密钥(一个公钥和一个私钥)来执行它们的工作。每个人都知道公钥，而私钥只有该密钥对的所有者知道。即使它们是加密连接的，私钥也不能使用公钥进行数学计算。不对称算法用于以下目的:

生成数字签名

创建加密密钥材料

*   身份管理

# 最后的想法

加密的重要性在于保护交易和通信、保护个人身份信息(PII)和其他私人数据、验证身份、防止文档篡改以及在服务器之间建立信任。想象一下，在向前迈进的数字时代，信任不再是一个问题，我们应该为此感谢密码学。

*来源:*

[*https://www . science direct . com/topics/computer-science/symmetric-key-algorithm*](https://www.sciencedirect.com/topics/computer-science/symmetric-key-algorithm)

[*https://www . synopsys . com/blogs/software-security/cryptographic-hash-functions/*](https://www.synopsys.com/blogs/software-security/cryptographic-hash-functions/)

[*https://www . synopsys . com/glossary/what-is-cryptography . html #:~:text = Definition，output%20(即% 2C %密文)*](https://www.synopsys.com/glossary/what-is-cryptography.html#:~:text=Definition,output%20(i.e.%2C%20ciphertext)) *。*

[*https://www . investopedia . com/tech/explaining-crypto-crypto currency/#:~:text = % 22 cryptography % 22% 20 means % 20% 22 secret % 20 writing，确保% 20 pseudo % 2D % 20 or % 20 full % 20 匿名*](https://www.investopedia.com/tech/explaining-crypto-cryptocurrency/#:~:text=%22Cryptography%22%20means%20%22secret%20writing,ensure%20pseudo%2D%20or%20full%20anonymity) *。*

***关于作者***

Brayan Nelson 是一名业余爱好作家，目前是一名大学讲师，同时在 NFT 的一个项目中实习。在 Medium 上，他写了他在 NFT 和元宇宙的联系和教育之旅。订阅他的时事通讯，成为第一个阅读他的博客故事的人。你也可以在 bnelsonsep3@gmail.com 通过电子邮件联系到他

[https://ph . LinkedIn . com/in/bray an-Nelson-pagatpatan-012882155？trk = profile-badge](”<a)">bray an Nelson Pagatpatan</a></div>

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [如何在 FTX 交易所交易期货](https://coincodecap.com/ftx-futures-trading) | [OKEx vs 币安](https://coincodecap.com/okex-vs-binance)
*   [CoinLoan 评论](https://coincodecap.com/coinloan-review) | [YouHodler 评论](/coinmonks/youhodler-4-easy-ways-to-make-money-98969b9689f2) | [BlockFi 评论](https://coincodecap.com/blockfi-review)
*   [XT.COM 评论](https://coincodecap.com/profittradingapp-for-binance)币安评论 |
*   [SmithBot 评论](https://coincodecap.com/smithbot-review) | [4 款最佳免费开源交易机器人](https://coincodecap.com/free-open-source-trading-bots)
*   [比特币基地僵尸程序](/coinmonks/coinbase-bots-ac6359e897f3) | [AscendEX 审查](/coinmonks/ascendex-review-53e829cf75fa) | [OKEx 交易僵尸程序](/coinmonks/okex-trading-bots-234920f61e60)