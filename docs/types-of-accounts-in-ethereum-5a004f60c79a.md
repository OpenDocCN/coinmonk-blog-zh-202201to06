# 以太坊中的账户类型

> 原文：<https://medium.com/coinmonks/types-of-accounts-in-ethereum-5a004f60c79a?source=collection_archive---------7----------------------->

免责声明:我不认为自己是专家，这是初学者对绝对初学者说的话。请务必考虑阅读下面的参考资料。

区块链通常被表示为分布式交易账本，即谁拥有多少以及所有交易的记录。虽然对于比特币和比特币叉子来说是这样，但以太坊和 EVM 的区块链增加了部署智能合约的能力。有效地创造可编程货币，增加以太的内在价值。

智能合同就像普通以太坊账户一样存在于一个地址上。但是差别很小

**账户类型**

以太坊区块链有两种类型的账户。

1.  **EOA —** 外部拥有的账户
2.  合同- 令人敬畏的东西。

# EOA-外部拥有的账户

由私人密钥、个人拥有的账户、密码交易所、企业等控制。拥有私人钥匙的人有权使用资金。

**私钥**为 32 字节(64 个十六进制字符)，通常由钱包随机生成。

**公钥**是使用 ECDSA 从私钥中导出的。

**地址**是公钥的最后 20 个字节(40 个十六进制字符)，前缀为 0x。

私钥用于签署交易以防止伪造。在当前的(PoW)共识模型中，只要私钥是安全的，只要 50%以上的矿工没有恶意行为，就不可能伪造交易。

# 智能合同

智能合约帐户具有与其相关联的代码和存储，它们不由私钥控制，而是由与之相关联的代码控制。

智能合约是生活在区块链的一个基本程序。

部署它们需要一些气体，因为它们一创建就使用存储。

虽然也有像 Vyper 这样的选项，但它们通常是用 solidity 编写的。

他们的 USP 是，一旦部署，他们不能被编辑。虽然这听起来像是一个缺点，但这正是智能合约如此强大的原因。

一旦部署，有关各方都知道它将如何执行，它不能被篡改。这消除了各方之间信任的要求，也增加了透明度。

然而，自毁是作为一种万无一失的安全措施，作为一种绝对的最后手段而加入的。

创建智能合同需要耗费大量的代码和存储空间。

**注**

*   智能合约不能启动交易，它们只对外部消息起作用，但是一旦交易开始，智能合约可以触发其他合约或转移以太网。
*   在实现应付方法之前，合同不能接受付款。

**共同属性**

这两个账户都可以接收、转移和持有乙醚。

所有帐户都有 4 个字段

**nonce—**EOA 发起的交易数量或智能合约部署的合约数量。

**余额-** 魏所拥有的账户(1 韦= 10)

**CodeHash —** (不可变字段)智能合约关联代码的 Hash。对于 EOA 来说，它是一个空字符串。

**存储散列—** 合同的整个状态树的 Merkle 根散列，对于 EOA 为空。

# 部署智能合同

智能合约在 EVM(以太坊虚拟机)上运行。

固态码被转换成**字节码**，该字节码可以被部署到网络上，并且可以被 EVM 理解。

**ABI(应用程序二进制接口)——**对于与智能合约交互很重要，它列出了函数、它们的预期回报类型和参数。

**读写合同状态**

要访问合同的公共可用属性或视图，不需要 gas。

然而，任何改变合同气体状态的功能都是必需的。

# 总部位于 EVM 的区块链

以上所说的不仅仅是以太坊，而是所有基于以太坊的区块链。

例如:多边形，雪崩 C 链，测试网等。

# 参考

[https://ethereum.org/en/developers/docs/accounts/](https://ethereum.org/en/developers/docs/accounts/)(必读)

[https://hacker noon . com/getting-deep-into-EVM-how-ether eum-works-back stage-AC 7 EFA 1 f 0015](https://hackernoon.com/getting-deep-into-evm-how-ethereum-works-backstage-ac7efa1f0015)

[](https://solidity-by-example.org/hacks/self-destruct/) [## 自毁|实例证明的可靠性| 0.8.10

### 一个如何通过调用 Solidity 中的 seldestruct 来删除你的智能合约的例子

solidity-by-example.org](https://solidity-by-example.org/hacks/self-destruct/) 

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Bookmap 评论](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [收购 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳加密软件](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [库币评论](https://coincodecap.com/kucoin-review)