# 审计参考:如何审计您的 Dapp

> 原文：<https://medium.com/coinmonks/auditing-reference-how-to-audit-your-dapp-aee09ecbf95d?source=collection_archive---------13----------------------->

我不得不在一些农场和赌注池工作，许多用户会在那里放置他们的代币很长一段时间。在 DeFi 项目中，您不断受到黑客攻击的威胁，因为许多令牌将长期处于智能合同中。这就是为什么我必须学习更多关于智能合同审计的知识。我在一篇文章中收集了所有必要的实践、练习、教程和文档作为参考。

## 什么是审计？

![](img/3efb1ce10ed0d80efb6b5f7b3f73ed5a.png)

Smart Contracts Auditing

要使用您的 Dapp，请确保它值得用户和投资者信赖。您必须确保您的智能合约中没有任何漏洞。审计是一组技术和实践，用于检测和描述(在报告中)安全问题，包括潜在的暴露、严重性/难度、潜在的利用场景和建议的修复。我会告诉你如何审计任何智能合同。智能合同审计员的工作就像智能合同开发人员一样。但是作为一名智能合约开发人员，您必须确保您的代码或您将要重用的代码是安全的。在通过审计程序之前。您需要应用一些步骤来使您的生活更轻松，并从审计中获益。

# **审计前需要做的事情**

在审计智能合同之前，您需要确保智能合同在业务和技术部分得到了很好的解释。所以，当你开始审计的时候，你可以得到最有效率的结果。你需要做的三件事:

## 规格分析

记录并详细描述你的项目做了什么以及为什么。包括每项资产和所有参与者的特权。描述作为设计和架构的一部分在功能上应该做的组件。

## 文件分析

规格分析描述了什么和为什么。但是文档分析解释了如何。用 [NatSpec](https://docs.soliditylang.org/en/latest/natspec-format.html) 格式文档化所有源代码，可以自动生成[文档](https://www.npmjs.com/package/hardhat-docgen)。我不建议仅仅因为开发人员忘记了许多细节就依赖自动生成的文档。我更喜欢用点画图和写描述(这是我的偏好。你可以选择其他的东西)。

## 完整测试案例和测试案例覆盖

首先，您应该从单元测试用例开始，分别测试每个事务。然后，创建代码应该触发或查询任何结果的用户场景，以及应该恢复事务的其他过程。第二，用覆盖率测试和 gas 报告重做相同的测试用例。现在，您已经准备好开始审计步骤了。

# 审计步骤

## 使用工具发现漏洞

第一步听起来可能更容易，但事实并非如此😅你需要仔细阅读结果，不要忽略任何警告信息。有些消息很复杂，所以请不要犹豫询问 Github 问题或该工具的官方渠道。

审计时有许多工具可以帮助您，例如:

1.  [mythril](https://github.com/ConsenSys/mythril) 在 EVM 层面检查你的智能合约
2.  [slither](https://github.com/crytic/slither) 是最流行的工具之一，用于防止可靠性代码(智能合同级别)上的问题
3.  [针鼹](https://github.com/crytic/echidna)用于[模糊测试](https://en.wikipedia.org/wiki/Fuzzing)(软件测试技术，涉及提供无效、意外或随机数据作为计算机程序的输入。)
4.  [蝎狮](https://github.com/trailofbits/manticore)检查你的代码逻辑中任何潜在的错误和漏洞。

## 遵循已知惯例

**编译**检查**检查**

1.  仅使用 Solidity 已知版本。现在，你可以使用`0.7.5`、`0.7.6`或`0.8.4`你可以在这里查看不同版本的。
2.  锁定杂注，确保您使用的是正确的版本，而不是旧版本
3.  在所有智能合约中仅使用一个编译器版本

**低级功能**

1.  确保`delegatecall()`和`callcode()`的*可信目的地*和`address`。
2.  使用`call()`发送以太网，并通过[检查-效果-交互模式](https://docs.soliditylang.org/en/v0.6.11/security-considerations.html#re-entrancy)或[重入防护](https://docs.openzeppelin.com/contracts/4.x/api/security#ReentrancyGuard-nonReentrant--)确保不可重入攻击。
3.  低级函数的返回值(`call`/`callcode`/`delegatecall`/`send`/等等)。).此处见示例[。](https://swcregistry.io/docs/SWC-104)

**库使用**

1.  对于数字签名，使用 OpenZeppelin 的`ECDSA` [库](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol)。
2.  使用 [safeMath](https://docs.openzeppelin.com/contracts/2.x/api/math) 或 solidity 版本 0.8 来避免溢出和下溢问题，并在乘法后除法。

**了解语法**

1.  请勿使用`tx.origin`进行授权。用`msg.sender`代替。(`tx.origin`因为许可可能会被中间的男人滥用(MITM))
2.  避免不推荐使用的[关键字](https://swcregistry.io/docs/SWC-111)。
3.  删除包含`mapping`的`struct`不会删除映射内容，这可能会导致意想不到的后果。使用[锁定](https://github.com/crytic/slither/wiki/Detector-Documentation#exploit-scenario-26)数据结构以防止错误使用。
4.  断言和请求不应该修改状态。我们使用 assert 进行不变检查，用户需要检查用户输入和返回值。

**当你阅读你的代码的时候**

1.  请确保您没有交易订单依赖关系。(交易不应依赖于特定的订单)
2.  将变量设为私有意味着其他智能合约无法读取它。这并不意味着变量不能读取链上的数据。隐藏数据，加密或保存离线。
3.  重言式或矛盾重言式总是`true`矛盾`false`或在[条件](https://github.com/crytic/slither/wiki/Detector-Documentation#misuse-of-a-boolean-constant)中使用布尔常量值。
4.  验证所有地址输入都不是零地址，对于关键地址，分两步更改它们。第一个事务(来自旧/当前地址)注册新地址(即，授予所有权)。第二个事务(来自新地址)用新地址替换旧地址(即声明所有权)。
5.  避免在[循环](https://swcregistry.io/docs/SWC-113)内调用，确保用户不能控制任何数组大小，以避免 DOS [攻击](https://swcregistry.io/docs/SWC-128)。
6.  不要忘记保护 [ini](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializers) t()交易。
7.  不正确的遗传[顺序](https://swcregistry.io/docs/SWC-125)、[缺失](https://github.com/crytic/slither/wiki/Detector-Documentation#missing-inheritance)遗传。
8.  确保功能参数中正确的内存和存储使用，并精确所有数据位置。

**用于代币**

1.  批准比赛条件:使用 OpenZeppelin 的`SafeERC20`实现中的`safeIncreaseAllowance()`和`safeDecreaseAllowance()`到*来防止比赛条件*操纵津贴金额。
2.  `ERC20`功能`transfer()`和`transferFrom()`应返回`bool`或使用`SafeERC20`
3.  `transfer()`、`transferFrom()`不应收取费用。它可能会导致一些意想不到的行为。
4.  使用 openzeplin ERC721[contract](https://github.com/crytic/slither/wiki/Detector-Documentation#incorrect-erc721-interface)时，er c721 中的`ownerOf`功能可能会返回错误的地址。

以上笔记是我发现的最重要的笔记，当然，还有很多其他的要点，你需要练习去发现它们。在下一部分，我将添加所有学习和练习资源

# 资源

Secureum 是一家由 Ethereum 资助的优秀公司，致力于帮助您成为一名出色的合同审计员。他们提供训练营。我建议每个人都参与进来。他们的[不和谐频道](/coinmonks/discord.gg/MaV3N2DxpF)上有很多关于面试问题的小测验。

[](https://secureum.substack.com/archive?utm_source=menu-dropdown) [## 存档-安全博物馆

### Secureum 所有帖子的完整存档。

secureum.substack.com](https://secureum.substack.com/archive?utm_source=menu-dropdown) 

Secureum 的内容有点难。这个家伙简化并恢复了 Secureum 课程中的许多要点

[](https://github.com/danielrees-eth) [## danielrees-eth -概述

### 您现在不能执行该操作。您使用另一个选项卡或窗口登录。您在另一个选项卡上注销，或者…

github.com](https://github.com/danielrees-eth) 

然后，您就有了这两份包含所有常见漏洞的清单。您可以在合同中用您需要编辑的每个部分来引用它们(例如，您正在使用`delegateCall`去检查所有可能的安全问题)

 [## SWC-134 概述

### 带有硬编码气体量的消息调用 CWE-655:不正确的初始化 transfer()和 send()函数转发…

swcregistry.io](https://swcregistry.io/docs/SWC-134) [](https://github.com/crytic/slither/wiki/Detector-Documentation) [## 探测器文档 crytic/slither Wiki

### 公共检测器列表 solc 版本 0.4.7- 0.5.9 包含一个编译器错误，导致不正确的 ABI 编码器使用。使用…

github.com](https://github.com/crytic/slither/wiki/Detector-Documentation) 

要将所学付诸实践，你可以在这三个网站上解决挑战。

 [## 捕获以太

### 让我们来玩 chevron right icon Capture the Ether 是一个游戏，在这个游戏中，你可以破解以太坊智能合约来了解…

capturetheether.com](https://capturetheether.com/)  [## 该死的脆弱的 DeFi

### 该死的易受攻击的 DeFi 是学习 DeFi 智能合同的进攻安全的战争游戏。遍及无数](https://www.damnvulnerabledefi.xyz/)  [## 以太人

### 编辑描述

ethernaut.openzeppelin.com](https://ethernaut.openzeppelin.com/) 

最后但同样重要的是，我发现博客涵盖了许多重要的实践

[](/coinmonks/5-solidity-code-smells-87bb2f259dde) [## 5 Solidity Code 气味，每个区块链开发者都应该知道

### 智能合同漏洞检测的 5 个心理模型

medium.com](/coinmonks/5-solidity-code-smells-87bb2f259dde) [](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/) [## 停止使用 Solidity 的转移()现在| ConsenSys 勤奋

### 看起来 EIP 1884 号在伊斯坦堡硬岔道朝我们开来了。这一变化增加了空载的汽油成本…

consensys.net](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/) [](https://github.com/sigp/solidity-security-blog) [## GitHub-sigp/solidity-security-blog:已知攻击媒介和常见攻击的综合列表…

### 这个库是这篇博文的基础，这篇博文在这里找到:https://blog.sigmaprime.io/solidity-security.html. It forms…

github.com](https://github.com/sigp/solidity-security-blog) 

最后，这是一个审计报告的例子，以及它应该是什么样子

 [## Aave 协议 V2 |理事会尽职调查

### 执行摘要本报告介绍了我们参与 Aave 协议第 2 版 Aave 审查的结果…

consensys.net](https://consensys.net/diligence/audits/2020/09/aave-protocol-v2) 

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [本地比特币评论](/coinmonks/localbitcoins-review-6cc001c6ed56) | [加密货币储蓄账户](https://coincodecap.com/cryptocurrency-savings-accounts)
*   [什么是融资融券交易](https://coincodecap.com/margin-trading) | [成本平均法](https://coincodecap.com/dca)
*   [支持卡审核](https://coincodecap.com/uphold-card-review) | [信任钱包 vs 元掩码](https://coincodecap.com/trust-wallet-vs-metamask)
*   [Exness 回顾](https://coincodecap.com/exness-review)|[moon xbt Vs bit get Vs Bingbon](https://coincodecap.com/bingbon-vs-bitget-vs-moonxbt)
*   [如何开始用加密贷款赚取被动收入](https://coincodecap.com/passive-income-crypto-lending)
*   [BigONE 交易所评论](/coinmonks/bigone-exchange-review-64705d85a1d4) | [电网交易机器人](https://coincodecap.com/grid-trading)