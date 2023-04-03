# 比特币中的地址

> 原文：<https://medium.com/coinmonks/addresses-in-bitcoin-15425706b154?source=collection_archive---------39----------------------->

![](img/0a45e99232db1ee14b85d982b674fbf5.png)

证明比特币所有权的方法之一是通过比特币地址。类似于拥有一个可以向其发送现金的账号，比特币拥有可以向其发送加密货币的地址。由于隐私，比特币地址不是永久的，因此为交易创建了不同的地址。

地址由 26–35 个字母数字字符组成，可以从公钥生成，也可以表示脚本。传统上，比特币地址是使用单向函数从公钥导出的，因此不可能从公钥导出私钥。
由于银行账户的类型不同，比特币的地址格式也不同。有些钱包只支持一种格式，有些则兼容几乎所有格式。这些地址格式取决于锁定脚本(scriptPubKey)包含的内容，如果它包含公钥的散列，则地址格式将是 P2PKH，如果它是自定义脚本的散列，则地址格式将是 P2SH

# P2PK(付费公钥)

**P2PK** 用于将比特币锁定到公钥，这基本上意味着比特币只能由拥有与用于锁定比特币的公钥相对应的私钥的用户使用。与生成比特币地址的传统方式不同，公钥直接用作地址。

尽管它是锁定比特币的最佳脚本，但却很少被使用。P2PK 可在区块链早期区块的 coinbase 交易中找到，在构建候选区块时，它被矿工用于区块奖励。P2PK 还被用于从 Satoshi 到 Hal Finney 的第一笔比特币交易。
目前不使用 P2PK，因为它暴露了接收方的公钥，使地址易受攻击，公钥有 130 个字符的长度，需要更加小心，因为它容易因长度而出错，任何错误都意味着资金损失。此外，它需要较大的交易费用，因为交易大小将主要取决于密钥的长度。

# P2PKH(付费公钥散列)

P2PKH 是比特币交易开始时的传统格式，默认情况下，该脚本存在于实现比特币客户端的钱包中。它比 P2PK 更安全，因为对实现 SHA-256 算法的公钥应用散列使得不可能从公钥推导出私钥。
T5 P2PKH 地址总是以 1 开始。

# P2PKH 如何工作

如果爱丽丝想向鲍勃发送比特币，鲍勃将通过使用 SHA-256 和 RIPEMD-160 函数从公钥生成 P2PKH 地址格式来启动该过程，鲍勃然后将地址发送给爱丽丝，爱丽丝然后启动生成交易和 P2PKH 脚本的过程，当爱丽丝输入交易细节时，她的钱包将数据转换为 P2PKH，这样他们就可以发送比特币。将执行 P2PKH 脚本，将硬币的所有权传递给 Bob，因为它们有对应于散列的公钥。

P2PKH 比 P2PK 更安全，因为您不必将您的公共地址发送给任何人，这使得它不容易受到攻击。然而，P2PK 已经过时，并且与大多数钱包不兼容，可能是因为从 P2PKH 地址发送时的平均费用通常因交易规模而较高。scriptPubKey 将如下所示:

```
OP_DUP OP_HASH160 {the public key hash} OP_EQUALVERIFY OP_CHECKSIG
```

# P2SH(付费脚本哈希)

P2SH 是 2012 年初作为 BIP16 的一部分推出的。与 P2PKH 不同，P2SH 不使用公钥的哈希，而是使用一个脚本的哈希，该脚本涉及某些消费条件，不会向发送方透露。这是一种将 scriptPubKey 表示为比特币地址的简单方法，它允许您在脚本哈希中锁定比特币，然后在比特币解锁进行交易时提供原始脚本。
**P2SH 地址总是以 3 开始**

# P2SH 如何工作

P2SH 可以最好地由多签名地址使用，比特币允许通过多签名交易或多签名来共享硬币的所有权，并且代表 n 个多签名中的 m 个的 scriptPubKey 被创建，这意味着为了花费硬币，将需要 m 个私钥来签署所提供的 n 个不同公钥中的花费交易。

在 P2SH 之前，向多签名地址发送比特币的过程很复杂，你需要将新创建的未签名的多签名交易发送给每个签名者，在他们签名后，你还需要从他们那里收集部分签名的交易，并将它们合并成一个，然后可以在网络上发布。

有了 P2SH，向多签名 scriptPubKey 支付变得像提供比特币地址一样简单。创建一个兑换脚本，它可以具有这样的条件:在硬币可以被花费之前，3 个密钥中的 2 个需要签名，然后将该脚本的散列发送给发送者，发送者不知道它是一个多重签名，一旦硬币被发送，脚本散列将这些硬币锁定在它上面，花费它们的唯一方式是输入用于创建散列的原始脚本(兑换脚本)，该散列可以包括数字签名和公钥验证。

P2SH 将提供完整兑换脚本的责任从发送者转移到接收者，这降低了发送者的交易费用，因为固定长度的散列允许发送者向任意兑换脚本发送资金，而不用担心支付更高的费用。创建兑换脚本的接收者有责任确定他们的消费交易的规模和费用。它也更安全，因为仅仅通过查看它不可能知道散列来自哪种锁定脚本。然而，P2SH 在区块链中占用更多空间，这会影响网络的运行容量。P2SH 的 scriptPubKey 会是这样的:

```
OP_HASH160 {the hash of the redeem script} OP_EQUAL
```

# 支付给证人公钥散列

P2WPKH 是一种高级地址类型，有助于减少区块链块大小，从而加快事务响应时间。2015 年，比特币增加了一个新功能，称为**隔离见证**，这将所有权证明从 scriptsig 部分移到了见证部分。

P2WPKH 与 P2PKH 比较类似，主要区别是公钥哈希不包含在 scriptsig 中，而是包含在 witness 中。这有助于大幅降低交易发送费用，并允许高处理速度，然而，大多数钱包不支持 SegWit，因为围绕它仍有许多争议。P2WPKH 地址以“bc1q”开头，因为它们是 Bech32 编码的。

# P2WSH(支付给证人脚本哈希)

就像 P2PKH 和 P2WPKH、P2WSH 和 P2SH 是相似的，不同之处只是脚本哈希的位置，它现在将在见证中，而不是在 scriptsig 中。它具有与 P2WPKH 相同的优点，因为它们都是 SegWit 地址。scriptPubKey 将如下所示:

```
OP_0 {the 32 byte Witness Script hash}
```

# P2TR(付费点击根)

P2TR，也称为 TapRoot address，是最新的比特币地址格式，它就像一个隐私升级，使更复杂的交易完全像正常交易一样成为可能。它是一种 ScriptPubKey，将比特币锁定在一个可以通过公钥或 Merkelized 替代脚本树(MAST)解锁的脚本上，使比特币能够以各种方式使用。

主根升级由 3 个不同的 bip 组成，它们是:

*   **BIP 340** :提议为比特币区块链引入 Schnorr 签名，schnorr 签名是一种加密方案，可以创建简短高效的数字签名，同时保持高度的安全性。使用 schnorr 签名，对于多签名事务，在区块链上记录单个聚合公钥和签名，而不是所有涉及的公钥和签名
*   **BIP 341(主根)**:这涉及到 schnorr signature 如何融入比特币网络。它解释了如何更新比特币脚本，以使用 Merkelized 替代脚本树来评估和集成 schnorr 签名，这确保了只有智能合约交易的执行条件才被提交给区块链，而不是所有其他可能结果的完整细节。
*   **BIP 342(Tapscript)** :这与更新和添加操作码有关，操作码有助于验证主根花费和 Schnorr 签名。

在我看来，P2TR 真的是比特币网络的一大升级。以多签名交易为例，大多数多签名交易都具有为了花费硬币而必须满足的条件，这些条件可以写成智能合同，在该智能合同中，可以有各种花费硬币的方式。无论执行什么条件，多签名交易仍然需要 m/n 个签名，并且在大多数情况下，签名不止一个，而 SegWit 帮助解决了必须将交易发送给每个签名者的麻烦，签名将被记录在区块链中。然而，Taproot 采用相关的签名或密钥，并使用 schnorr 签名方案创建一个简短有效的签名，然后当花费硬币的条件之一已经满足并且现在可以花费时，taproot 确保在区块链上只记录执行的条件。

P2TR 比任何其他地址格式更安全，它不区分单 sig 和多 sig 交易，这样，没有人知道什么类型的钱包用于交易。它还有助于节省区块链上的空间，从而提高交易验证的效率。P2TR 是在 2021 年几经周折才实现入网的，和 SegWit 一样是 Bech32 编码的地址，以“bc1p”开头。

了解不同的格式是必不可少的，这样才能知道什么时候使用它们，什么类型的钱包，这篇文章有助于让用户基本了解比特币地址格式如何工作以及使用它们的好处。所有的地址格式都确保隐私，因为这是比特币的原则之一，然而，最近的格式有助于提高隐私和扩大网络。

*原发布于*[*https://munirat . hash node . dev*](https://munirat.hashnode.dev/addresses-in-bitcoin)*。*

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)获取每日[加密新闻](http://coincodecap.com/)

# 另外，阅读

*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)
*   [block fi vs Celsius](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630)|[Hodlnaut 审核](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 审核](https://coincodecap.com/kucoin-review)
*   [Bitsgap 审查](/coinmonks/bitsgap-review-a-crypto-trading-bot-that-makes-easy-money-a5d88a336df2) | [Quadency 审查](/coinmonks/quadency-review-a-crypto-trading-automation-platform-3068eaa374e1) | [Bitbns 审查](/coinmonks/bitbns-review-38256a07e161)
*   [加密复制交易平台](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c) | [Coinmama 评论](/coinmonks/coinmama-review-ace5641bde6e)
*   [印度的加密交易所](/coinmonks/bitcoin-exchange-in-india-7f1fe79715c9) | [比特币储蓄账户](/coinmonks/bitcoin-savings-account-e65b13f92451)
*   [OKEx vs KuCoin](https://coincodecap.com/okex-kucoin) | [摄氏替代品](https://coincodecap.com/celsius-alternatives) | [如何购买 VeChain](https://coincodecap.com/buy-vechain)