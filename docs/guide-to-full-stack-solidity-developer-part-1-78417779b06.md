# 全栈坚固性开发指南-第 1 部分

> 原文：<https://medium.com/coinmonks/guide-to-full-stack-solidity-developer-part-1-78417779b06?source=collection_archive---------9----------------------->

接下来:[全栈 Solidity 开发者指南—第二部分](https://takshilp.medium.com/guide-to-full-stack-solidity-developer-part-2-c11b8c14ea20)

下面是成为一名完整栈 Solidity 开发者应该具备的技能。这意味着你要擅长 web 开发(React，Typescript) +区块链开发(Solidity)。本文的目标不是保存所有资源的存储库，而只是一个路径和一些您应该知道的参考。我建议寻找更多更好的资源。

我一般用 Solidity，React 写 Dapps(分布式区块链应用程序)。JS，Typescript。因此，本文将更侧重于这些技术，但是您仍然可以使用这种方法，并为您的特定技术找到类似的对应技术。

我已经给出了示例参考，您可以搜索更好的 github 项目。除了这些笔记中给出的内容，您还可以从 youtube 和 github 上搜索其他资源。

在实践中，阅读和分析下面的智能合同将会了解更多关于加密生态系统以及如何使用 solidity 来构建真正的世界应用程序。

# 1.固态

ref:[https://www . Reddit . com/r/solidity/comments/s 6259 q/what _ are _ some _ good _ beginner _ projects/](https://www.reddit.com/r/solidity/comments/s6259q/what_are_some_good_beginner_projects/)

你应该做所有的巩固基础(从这个开始)，然后巩固中级项目(然后这个)，最后巩固高级项目。一般来说，你会从事高级项目。

## 1.1 先决条件

*   区块链工作概述。什么是以太坊区块链。mainnet 和 testnet 的区别。
*   什么是智能合约。为什么需要它们。
*   使用 Remix IDE &使用 Hardhat 的智能合约开发基础。

如果你刚到区块链，那么请使用这个网站了解更多关于区块链[区块链基础知识](https://ludu.co/course/ethereum/what-is-ethereum/)。

## 1.2 可靠性智能合同编程

在这种情况下，你应该能够编写简单的 solidity 项目(此时无需创建前端),并在本地区块链环境或实时以太坊测试网中运行它们。

*   我收集的实践项目灵感来自[安基特学校](https://github.com/Aniket-Engg/solidity-school):[https://github.com/Le4kno3/Solidity-Contracts-Practice](https://github.com/Le4kno3/Solidity-Contracts-Practice)
*   你至少需要阅读一次完整的 Solidity 文档，这是一个写得很好的指南，涵盖了所有细节，包括示例代码:[https://docs.soliditylang.org](https://docs.soliditylang.org/en/v0.8.17/)
*   然后，我会建议浏览[可靠性实例网站](https://solidity-by-example.org) & [可靠性实例视频](https://www.youtube.com/@smartcontractprogrammer/videos)中的每个合同主题
*   最后，我强烈推荐你阅读[以太坊白皮书](https://ethereum.org/en/whitepaper/)。

如果你完成了以上内容，你就对 Solidity 编程知识及其语法有了很好的实践知识。

## 1.3 错误处理

现在，在写合同时，可能会出现错误**和异常**。

最大的问题是找到错误的根本原因。以下几点可能会有所帮助

*   如果您使用 hardhat framework 进行开发，您将会看到触发该错误的所有文件和这些文件的行号。
*   如果异常是像从`require()`或`revert()`这样的程序触发的，那么确保错误字符串在错误消息中容易给出根本原因。

以下是我所面临的几点错误的根本原因:

1.  **用户输入类型**:合同要求输入字节，但您发送的是字符串，或者合同要求输入整数，但您发送的是字符串。在某些情况下，你输入了 16 个字节，但你只发送了 15 个字节，那么在这些情况下，你会得到错误，就像在**地址**的情况下。实际上，您需要为契约中的所有这些输入编写代码，记下来，以后用作参考。
2.  **按正确顺序排列的函数参数编号**:如果一个函数有 3 个参数，而您错误地将第二个参数发送到了第三个位置，那么在处理它时将会触发错误或不需要的结果。

伟大的 [github 库](https://github.com/xf97/JiuZhou)中有一个完整的错误分类列表。关于关键类别，请参考这篇 [linkedin 文章](https://www.linkedin.com/posts/patrick-sfeir-353260174_blockchain-defi-ethereum-activity-6990650195621355520-6Fpy/?utm_source=share&utm_medium=member_android)。

## 1.4 坚固性调试(如果需要)

如果您无法找到错误的根本原因，那么要解决问题，您需要逐行查看合同的执行情况。

我强烈推荐使用 [Remix IDE 调试器](/remix-ide/remix-debugger-b542ea24a0d)，因为它简单且易于排除故障。但是对于更全面的测试和调试，请使用 hardhat 测试框架，并使用 vscode 扩展进行调试。

## 1.5 区块链开发 VScode 插件

这些插件使得 solidity 的开发更加用户友好。

ref:[https://medium . com/web 3-magazine/visual-studio-code-区块链-开发-插件-4ea1918e6b4f](/web3-magazine/visual-studio-code-blockchain-development-plugins-4ea1918e6b4f)

## 1.6 区块链开发工具

这些工具(大部分是在线的)有助于区块链的发展和互动。

ref:[https://takshilp . medium . com/solidity-tools-collection-development-testing-CD 4 f 028d 72 f 2](https://takshilp.medium.com/solidity-tools-collection-development-testing-cd4f028d72f2)

# 2.Solidity 智能合同项目

类似文章:[https://sm 4 rty . medium . com/roadmap-for-web 3-smart-contract-hacking-2022-229 E4 e 1565 F9](https://sm4rty.medium.com/roadmap-for-web3-smart-contract-hacking-2022-229e4e1565f9)

这些项目的目标首先是学习区块链发展的新课题。其次，在智能合同方面有更多的实践经验，以便从头开始编写新合同变得简单快捷。

> 注意:这些智能契约类似于 API，您可以通过编程方式与契约进行交互，以发送一些输入并接收一些输出。但要设计一个漂亮的 GUI 网页，请参考本指南的第 2 部分，在那里你将学习 react typescript web 开发，以及 ethers.js 和 web3.js 等 web3 库，所有这些都是创建去中心化区块链应用所需要的。

## 2.1 通过构建简单的游戏来学习使用加密僵尸

参考:https://cryptozombies.io/

## 2.2 智能合同项目-1 级

参赛作品:[https://openquest.xyz/tracks/build-on-ethereum](https://openquest.xyz/tracks/build-on-ethereum)

*   [简单银行(客户、取款、存款)](https://openquest.xyz/quest/building-a-bank-with-solidity-that-isnt-a-toy)
*   [推出你自己的硬币](https://openquest.xyz/quest/launching-your-own-coin)。还要练习铸币和烧币。
*   推出你自己的 NFT。还要练习铸币和埋币。
*   [创建融资智能合同](https://dev.to/muratcanyuksel/creating-a-fundme-smart-contract-in-remix-ide-notes-from-freecodecamp-3imm) (freecodecamp)
*   [打造俄罗斯轮盘 App。](https://openquest.xyz/quest/Building-a-Russian-Roulette-dapp-on-Ethereum)
*   [建立一个标桩合同。](https://openquest.xyz/quest/Building-your-own-Staking-Contract)
*   [使用 ECM 发送通知。](https://openquest.xyz/quest/Sending-notifications)
*   [Merkle 树项目 1](https://github.com/Harzu/merkle-tree-for-solidity-proof) & [Merkle 树项目 2](https://github.com/ameensol/merkle-tree-solidity)

其他类似合同项目参见[链接](https://openquest.xyz/tracks/build-on-ethereum)。

## 2.3 智能合同项目- 2

使用 site:github.com dork 进行谷歌搜索，你可以找到其他人完成的类似项目。

参考:[DApp 实用教程集](https://www.linkedin.com/posts/shubham0850_react-css-programming-activity-6992311080593055744-kzlk/?utm_source=share&utm_medium=member_android)

*   某种形式的游戏，比如密码猫。[举例](https://www.youtube.com/playlist?list=PL16WqdAj66SBFRgReM34ChxfZoYuzbjdx)。
*   一款玩家可以进行回合制战略战斗的游戏。
*   宠物店
*   斯蒂米特的克隆体。
*   投票
*   高产农业
*   授权和投资项目
*   多签名钱包
*   建立一个去中心化的交易所
*   建立价格预测。
*   撰写与使用 oracle 和 exchange 的平台相关的合同。就像借硬币合同一样。

## 2.4 有趣的真实世界项目(Real World Projects)

Ref: [区块链 10 大精彩用例](https://www.linkedin.com/posts/wsdt_web3-blockchain-usecase-activity-7007043389896458240-6EjA/?utm_source=share&utm_medium=member_android)

## 2.5 其他合同收款

*   [GitHub—raineorshine/solidity-by-example:一组简短但功能齐全的契约，展示了 Solidity 的语言特性。](https://github.com/raineorshine/solidity-by-example)
*   [https://github.com/FStanczyk?tab=repositories](https://github.com/FStanczyk?tab=repositories)

# 3.标准合同(图书馆)

在本主题中，我将向您介绍一些安全、经过全面测试并在区块链开发中广泛使用的标准合同。

## 3.1 您应该深入了解的 Smarts 合同:

资源:[https://bytescout.com/blog/top-5-smart-contracts.html](https://bytescout.com/blog/top-5-smart-contracts.html)

你不必记住或编写它们，这些只是一些重要的智能合同，你应该深入分析和理解它们的工作原理。

*   [ERC20 代币](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol)(用于硬币和代币)
*   [ERC721 代币](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol)(针对 NFT)
*   [ERC1155 令牌](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC1155/ERC1155.sol) s(用于 NFT)
*   [UniswapV2Pair.sol](https://github.com/Uniswap/v2-core/blob/master/contracts/UniswapV2Pair.sol) (重要合约)
*   [政府采购](https://github.com/compound-finance/compound-protocol/blob/master/contracts/Governance/GovernorAlpha.sol)(重要合同)
*   [总厨](https://github.com/pancakeswap/pancake-farm/blob/master/contracts/MasterChef.sol)(重要合同)
*   [Uniswap v2。v3](https://github.com/harendra-shakya/uniswap-unwrapped)
*   [永久协议](https://0xkowloon.substack.com/p/dissecting-the-perpetual-protocol)
*   [平衡器 V2 协议](https://0xkowloon.substack.com/p/dissecting-the-balancer-v2-protocol)
*   [奥林巴斯](https://0xkowloon.substack.com/p/dissecting-the-olympus-protocol)
*   [部分协议](https://0xkowloon.substack.com/p/dissecting-the-fractional-protocol)

关于使用的顶级合同，请参考:[前 5 名智能合同](https://bytescout.com/blog/top-5-smart-contracts.html)

# 下一步是什么？

*   Solidity 语言正在积极开发中，每隔几个月就会发布一个次要版本。主要版本有新的特性和突破性的变化，所以你可能会遇到一些在 solidity 以前的版本中可以用，但在新版本中不能用的东西，反之亦然。作为一名区块链开发者，你需要**阅读版本发布说明中的每一个新变化**。
*   在这篇文章中，我故意没有包括一个非常重要的部分，即**智能合同安全**和审计，这甚至比 web3 世界中的开发更重要。这将在本指南的第 4 部分中介绍。这将包括 CTF、挑战等。
*   此处未包含的另一个主题是**智能合约升级**功能。是啊！这是实际存在的，我们可以升级(而不是修改)智能合同。这将在本指南的[第 3 部分](https://takshilp.medium.com/guide-to-full-stack-solidity-developer-part-3-2a5892969fe9)中介绍。
*   另一个不在本文中的重要话题是**气体优化**。我已经写了一篇详细讨论[气体优化](https://takshilp.medium.com/solidity-gas-optimisation-91ada7d86ee7)的博客。
*   看看这个伟大的知识库:[以太坊——我知道的一切](https://wiki.nikiv.dev/databases/blockchain/ethereum)
*   [智能合同开发最佳实践。](https://yos.io/2019/11/10/smart-contract-development-best-practices/)
*   很少有关于可靠性模式的文章，你可以经常阅读这样的文章和博客。本指南第 3 部分中给出了几个链接。

> 加入 coin monks[Telegram group](https://t.me/joinchat/Trz8jaxd6xEsBI4p)学习加密交易和投资