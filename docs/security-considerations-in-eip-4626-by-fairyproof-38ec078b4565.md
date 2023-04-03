# EIP-4626 的安全考虑

> 原文：<https://medium.com/coinmonks/security-considerations-in-eip-4626-by-fairyproof-38ec078b4565?source=collection_archive---------5----------------------->

![](img/fd8c4924a90c9f9769e8b1f8f0e8ab5c.png)

在 DeFi application Fei Protocol 的联合创始人乔伊·桑托罗的领导下，最近提出了一个 EIP，为令牌化金库创建一个新的令牌标准。它就是 EIP-4626[1]。

尽管它在 2021 年 12 月才被提出，但它很快就获得了以太坊社区的极大关注和支持，并据报道被包括部落道[3]和 Rari 资本道[4]在内的一些道[2]采用。

该 EIP 旨在解决令牌化金库现有实现中的一个痛点，即“令牌化金库缺乏标准化，导致实现细节多样化”[1]。这一痛点使得令牌化库的集成“在协议的聚合器或插件层很困难，这些协议需要符合许多标准，并迫使每个协议实现它们自己的适配器，这些适配器容易出错并浪费开发资源”[1]。

该 EIP 基于 ERC-20[5]，这是以太坊的 DeFi 应用中广泛采用的标准，具有相当大的安全问题或风险，需要智能合约开发人员的注意。

作为一家区块链安全公司，Fairyproof 的研究团队对 ERC-20 实施的问题或风险是否也会引入 ERC-4626 非常感兴趣。我们研究了这个 EIP，探索了可能的安全检查点，并想分享一些关于这些检查点的想法。

该 EIP 要求令牌化的保险库必须实施 ERC-20 来表示份额，并添加新的接口，以便在可视功能和转移功能中将份额转换为令牌或将令牌转换为份额。这些新增加的功能引入了需要我们注意的安全问题。

以下是基于此 EIP 实施令牌化存储时的安全注意事项列表:

-恶意功能的实现

考虑一个保险库的实现，它符合这个 EIP 定义的接口，但不符合规范。这种情况在使用代理机制的情况下经常发生，代理接口似乎符合令牌标准，但实际上，真正的实现是一个恶意的契约。

因此，在采取进一步行动之前，审计员或用户需要仔细检查它的实际实现。

**-支持 EOA 账户**

EIP 声明“如果实施者打算直接支持 EOA 账户访问，他们应该考虑增加一个额外的存款/造币/取款/赎回的功能调用，以适应滑动损失或意外的存款/取款限额”[1]。

除了滑点损失和意外的存款/取款限额之外，还有另一种常见的情况:令牌在其传输过程中被烧毁。一些 DeFi 应用程序使用这种机制来减少其代币的流通供应量并抬高代币的价格。

我们建议 ERC-4626 金库不允许这种代币存放在金库里。

**-使用接口作为神谕**

EIP 声明“预览方法返回尽可能接近精确的值。因此，它们可以通过改变链上条件来操纵，而且作为价格先知并不总是安全的。”[1]以及“在资产和股票之间转换时，使用时间加权平均价格来实现转换方法是正确的。”[1]

oracle 在加密领域中最常见的用例是使用它们来获取令牌的价格，但是智能合约需要的任何信息都可能依赖于 Oracle。因此，返回信息的预览方法也可以用作 oracles。虽然这似乎没有什么重要的用例，但是现在，这个列出的潜在问题需要我们注意。减轻链上信息被操纵风险的一种流行方法是使用 Uniswap[6]引入的时间加权平均算法。

**-舍入问题**

对于计算保险库份额或令牌数以及将份额转换为资产或资产转换为份额的接口，保险库实施者需要小心处理舍入方向。

该规范建议，当计算发行给用户的股份的基础代币的数量时，他/她提供的或发送给他/她的基础代币的数量为他/她返回的一定数量的股份，应该向下舍入。

在计算用户为获得特定数量的基础令牌而必须提供的股份数量或用户为获得特定数量的股份而必须提供的基础令牌数量时，应该向上取整。

当在 converTo 函数中计算份额或基础令牌的数量时，规范要求保险库实施者向下取整，以确保所有 ERC-4626 保险库实施的一致性。

这些建议和要求确保始终有足够数量的底层令牌保留用于传输。这是审计人员在基于此 EIP 审计保险库实现时需要注意的。

**-令牌兼容性问题**

这个 EIP 特别提到了 ERC-20 令牌标准。它是实现可替换令牌最广泛采用的令牌标准。然而，在我们过去的审计经验中，我们也审计了一些基于替代以太币令牌标准(如 EIP-777[7])实现的可替换令牌。

这些替代令牌标准与 ERC-20 令牌兼容，但有一些差异。

让我们以 EIP-777 令牌标准为例。令牌标准允许实现者使用注册表来查找接口。如果注册表有缺陷，任何依赖它的东西都会有负面影响。这个特性引入的一个常见问题是重入风险[8]。

因此，可能存在两种我们需要注意的情况。

第一种情况是基于 ERC-20 兼容但替代的标准来实现保险库。第二个是 ERC-4626 值，它与 ERC-20 兼容但基于替代令牌标准实现的令牌进行交互。

在这两种情况下，替代令牌标准可能会带来问题或风险。并且应该仔细审查和审计基于替代标准的实现。

**结束语:**

在本文中，我们列出了审核基于 ERC-4626 的保险库时一些可能的安全注意事项。其中一些考虑因素已经在《EIP》中提及，其他的则是根据我们的审计经验列出的。

我们希望我们的尝试性建议能给实施者、使用者和审计人员一些关于如何安全可靠地处理 ERC-4626 保险库的粗略想法。

参考资料:

[1]https://eips.ethereum.org/EIPS/eip-4626 EIP-4626:令牌化跳马标准，[2021 年 12 月 22 日](https://eips.ethereum.org/EIPS/eip-4626)

[2]分权自治组织，【https://ethereum.org/en/dao/】T4

[3]部落，[https://docs.fei.money/governance/tribe](https://docs.fei.money/governance/tribe)

[4]拉里资本，[http://rari.capital/](http://rari.capital/)

[5] ERC-20 令牌标准，[https://ether eum . org/en/developers/docs/standards/tokens/ERC-20/](https://ethereum.org/en/developers/docs/standards/tokens/erc-20/)

[6] Uniswap，[https://uniswap.org/](https://uniswap.org/)

[7]https://eips.ethereum.org/EIPS/eip-777 EIP-777:令牌标准

[8] Samreen N F，Alalfi M H .以太坊智能合约中的可重入性漏洞识别[C]//2020 面向区块链的软件工程 IEEE 国际研讨会(IWBOSE)。IEEE，2020 年:22–29。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)