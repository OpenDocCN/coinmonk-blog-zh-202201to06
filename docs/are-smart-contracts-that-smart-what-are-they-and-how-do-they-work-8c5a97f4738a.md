# 智能合约有那么智能吗？它们是什么，它们是如何工作的？

> 原文：<https://medium.com/coinmonks/are-smart-contracts-that-smart-what-are-they-and-how-do-they-work-8c5a97f4738a?source=collection_archive---------24----------------------->

智能合约是储存在区块链网络上的计算机程序，在特定条件得到满足时执行。

让我们来分解一下这个定义:

> **【计算机程序】**

智能合同是在区块链网络上执行交易时使用的一种软件。

人们可以把智能契约想象成一组 IF-THEN 语句，它根据契约接收到的输入自动执行某些操作。

智能合约接收交易的内容，然后根据编程逻辑标准确定交易是否有效。

> **“存储在区块链网络上”**

智能合约的代码由给定网络中的节点存储。智能合约通常与公共网络地址相关联，用户可以将交易定向到该公共网络地址，以便触发智能合约的执行。

智能契约还可以通过 oracles 引用链外数据源。

> **“满足特定条件时执行”**

因为智能合约的逻辑是用代码形式化的，所以智能合约无法决定是否执行或如何执行。

执行的标准，以及将采取的后续步骤，不变地编码到每个智能合同中。

此外，当智能合约被触发时，其逻辑在给定网络的每个节点上独立执行，使得没有单个节点能够阻止智能合约的执行。

## **以太坊智能合约研究**

1.  **以太坊虚拟机——EVM**

以太坊智能合约通常用 Solidity 编程语言编写。

然而，以太坊虚拟机(EVM)——负责运行智能合约的分散式计算引擎——无法直接读取和执行 Solidity 代码。

相反，这些代码必须首先被编译，翻译成 EVM 节点可以理解的字节码。

一旦智能合约的代码被编写和编译，合约的作者必须将字节码发送到一个特定的以太坊地址(称为零地址)，这向网络的节点表明一个新的合约正在被创建。

一旦该交易被网络验证，智能合约被部署，并且其代码被保存在合约账户中。

与传统用户帐户一样，合同帐户与公共网络地址相关联，可以持有令牌余额，这些余额可以转移到其他网络地址。但是，合约帐户没有关联的私钥，这意味着没有个人有权控制智能合约的余额。

相反，只有根据智能合约中编码的规则，才能从智能合约中转移余额。没有任何与以太坊智能合约相关联的私钥意味着:智能合约不能自己发起交易。相反，必须将事务发送到智能合约的地址，才能触发其执行。一个智能协定可以被另一个智能协定调用。

**2。智能合同的功能**

给定的智能合约可以包含任意数量的不同功能，这些功能执行不同的动作，并在执行时导致不同的网络状态变化。

例如，在 DeFi 借出/借入中，智能合同可能包括管理协议促进的借入和借出动作的功能:

*   调用“借款”功能以命令智能合同从其储备中向指定用户发送一些代币，减少该代币的合同账户余额并增加该代币的用户余额
*   调用“借出”功能可能会产生相反的效果。

因此，以太坊交易包含一个可选的“数据”字段，可用于指示用户希望调用给定合约账户中存储的哪些功能。“数据”字段也可用于将特定数据或参数传递给函数。

## **智能合约的挑战**

虽然智能合约代表了一项重要的创新，并在许多区块链应用程序中广泛使用，但应该记住一些重要的注意事项:

1.  **网费:**

与智能合约交互会产生网络费用。由于智能合约交互通常比普通令牌传输的计算量更大，因此这些网络费用通常会很高，甚至可能超过由可信第三方在中介环境中收取的费用。

**2。公开代码:**

智能合约是可公开访问的软件应用程序，因此容易受到编程错误、恶意行为者的攻击以及其他不可预见的负面结果的影响。此外，对 oracles 的日益依赖可能会成为漏洞的来源和攻击的媒介。

**3。交易是不可变的**:

通过智能合约执行的交易在设计上是不可逆的，这使得资金受到黑客攻击、漏洞或其他不可预见情况影响的用户收回资金的能力有限。当然，法律体系的管辖范围延伸到了加密领域。

此外，区块链社区过去曾投票决定对那些资金受到恶意行为者影响的人进行赔偿，基于智能合同的保险系统也被开发出来，试图为用户提供一定程度的安全保障。

**4。对“代码”可翻译应用的限制**

最后，可以被智能合约取代的现实世界合约的范围仅限于那些条款可以用计算机代码完全表达的合约，以及那些可以基于计算机可读的、oracles 可访问的在线信息来衡量绩效的合约。

![](img/0dab2240629336355ade3727adcfb1af.png)

# 反馈

在这里[让我知道你的想法](https://www.philippeho.com/contact)并在[推特](https://twitter.com/1philippeho)上关注我！

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs Ngrave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)