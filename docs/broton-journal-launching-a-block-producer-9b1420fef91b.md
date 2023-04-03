# Broton Journal:推出积木制作人

> 原文：<https://medium.com/coinmonks/broton-journal-launching-a-block-producer-9b1420fef91b?source=collection_archive---------24----------------------->

## 质子区块链的一个区块制作人的现场笔记

![](img/04f820f0d0fced2abc1ac29654d59026.png)

再见，亲爱的读者！谢谢你阅读我们！

[在上一篇文章](https://brotonbp.medium.com/broton-journal-introduction-a7e81f235c2c)中，我们进行了自我介绍，并讲述了我们是如何来到质子的。

今天，我想告诉你我们自己的经验，推出一个区块生产者(英国石油公司)对质子。我们不想深入技术细节，因为我们更有经验的同事、块生产人员和质子团队已经写了描述所有安装步骤的优秀文章。尽管如此，我们还是想把它们放在一起，让您了解全局。正如一位历史最悠久的质子 BPs 喜欢说的:

> 做一个 BP 不仅仅是运行一个节点然后遗忘它……—[EOS USA Michael](https://medium.com/u/7a99533ec178?source=post_page-----9b1420fef91b--------------------------------)。

我们将全程为您讲解，重点介绍我们使用的信息来源，并关注重要细节。

但首先，请阅读官方质子博客中的文章，以获得关于[如何成为质子](https://blog.protonchain.com/how-to-become-a-block-producer-on-proton/)块生产商的概述。

> 知道路和走在路上是有区别的。——莫斐斯。

# EOSIO？从未听说过…🤷‍♂️

在讨论具体问题之前，让我们先学习一下基本理论，以便更好地了解我们正在做的事情(实际上，如果您决定成为 Proton 的区块生产厂商，您应该已经了解 EOSIO，否则，您应该花些时间并利用提供的资源对此进行研究)。

质子号是基于 EOSIO 技术——一个用于建造区块链的复杂平台。许多受欢迎的区块链是基于它:EOS，Telos，Wax 和其他。不要将其与“叉子”混淆——质子不是 EOS 的叉子；它是一个基于 EOSIO 技术的独立的区块链。

EOSIO 共识机制被称为 DPoS(委托利益证明)，是对 PoS(利益证明)的一种修改。与最终用户充当验证者的 PoS 相反，在 dpo 中，创建块和验证事务的功能被委托给受信任的节点——块生产者。在质子公司，只有前 21 家区块生产商生产区块；其他人在待机模式下等待，必须准备好进入日程。区块生产商的评级是基于最终用户投票——当质子用户用他们的 XPR 美元换取 APR(年化利率)时，他们选择四个区块生产商进行投票。

砌块生产商为他们的工作赚取报酬，报酬是 XPR 美元——报酬来自 1%的年度通货膨胀。除此之外，1%的通货膨胀分给了所有的投资者，另外 1%——分给了[管理委员会](https://www.protonchain.com/governance/)。

一般来说就是这样。所以，如果你真的想成为一名街区制作人，你应该知道如何提高你的声誉。🔝不要指望人们会因为你在运营一个节点而投票给你。

幸运的是，EOSIO 在其[网站](https://eos.io)上有非常优秀的文档，你可以在那里获得所有的信息。此外，还有许多有用的视频、教程、网络研讨会，甚至免费的 [EOSIO 培训&认证](https://eos.io/training-certification/)课程。

# 言归正传！

我们想让您的生活更轻松一点，所以我们根据我们的知识和经验编制了这个详细的计划:

1.  加入质子测试网电报组。
2.  为您的 BP 创建一个质子帐户。
3.  创建一个网站和社交媒体账户。
4.  提供关于您的 BP 的信息。
5.  创建加入质子测试网的节点。
6.  请求在 Testnet 上注册生产者节点的权限。
7.  在 Testnet 上注册您的生产者节点。
8.  为您的 Testnet producer 节点获得一些投票，以便进入日程。
9.  在 Testnet 上成功签名至少两周。
10.  创建连接到质子主网的节点。
11.  请求在 Mainnet 上注册生产者节点的权限。
12.  在 Mainnet 上注册您的生产者节点，并准备生产块！
13.  要求奖励。

一步一步来，我们会在自己经历过程中遇到的一些不明显的事情上做强调。

## 1.加入质子测试网电报组

[质子测试网](https://t.me/ProtonTestnet)是一个为区块生产者和候选人的官方电报组。在这里，如果你遇到问题，你可以依靠其他业务伙伴的帮助。但是请确保你在提问之前已经做了调查。☝️

## 2.为您的 BP 创建一个质子帐户。

你应该在 Testnet 和 Mainnet 上都保留一个名字，因为它可以被任何人注册。

您可以使用质子浏览器检查帐户是否免费:

*   [测试网](https://testnet.protonscan.io)
*   [Mainnet](https://www.protonscan.io)

如果你还没有质子帐户，下载[Webauth.com 移动钱包](https://www.protonchain.com/wallet)并在 Mainnet 上创建它。如果你已经有一个个人帐户，最好使用[质子资源](https://protonresources.com/create-account) dApp 为你的 BP 注册一个单独的帐户。

在 Testnet 上，你可以在这里创建一个账户[。](https://monitor.testnet.protonchain.com/#account)

## 3.创建网站和社交媒体账户

网站是你 BP 的门面——它显示在 [protonscan.io](https://www.protonscan.io/vote) 上的区块生产商列表中。所以，买一个域名，创建一个网站，让人们知道你是谁，你在做什么。

有一些要求:

1.  你必须在你的域名的根目录下有一个名为 [*bp.json*](https://github.com/eosrio/bp-info-standard) 的文件。我们使用了两个不同的子域在 Testnet 和 Mainnet 上注册，所以我们将两个 bp.json 文件放在以下 URL:[testnet.brotonbp.com/bp.json](https://testnet.brotonbp.com/bp.json)和[mainnet.brotonbp.com/bp.json](https://mainnet.brotonbp.com/bp.json)。所有其他的网址都被重定向到主域名——[brotonbp.com](https://brotonbp.com)，所以普通用户可以看到我们的网站。如果使用单个域，可以创建一个 [*chains.json*](https://github.com/eosrio/bp-info-standard) 文件，描述哪些 bp.json 文件与每个网络相关。
2.  此外，您必须在您的网站上提供所有权披露信息，并就您的 BP 和使命说几句话。

当你创建一个 *bp.json* 文件时，你可以指定你的社交网络账户——一定要这样做，至少是 Twitter。你需要和你的支持者沟通的渠道。

## 4.提供关于您的 BP 的信息

只需完成[这张表格](https://docs.google.com/forms/d/e/1FAIpQLSeJZGdcDQy61t-k_wHxHP0rWFcNKyv64LWpnePfbhn-vxDS4g/viewform)——提供你的数据并写出你的意图。

## 5.创建加入质子测试网的节点

有几种类型的节点。

主要基础设施(必需):

*   生产者节点—负责生产块。生产者节点应该没有公开的公共服务。❗️
*   标准 [v1 链 API](https://developers.eos.io/manuals/eos/latest/nodeos/plugins/chain_api_plugin/api-reference/index) (需要专用服务器)。

二级基础设施(非必需，但首选):

*   EOS Rio 为质子上的 dApps 开发者提供了从区块链提取各种历史数据的历史 API。

此外，您不应该忘记在单独的位置拥有备份节点和负载平衡。您必须保证节点的正常运行时间。

这次我们只讨论主要的基础设施。当我们运行 Hyperion 节点时，我们将在下面的文章中介绍它的设置。

如前所述，我们在创建节点时使用了几个编写良好的指令:

*   [github.com/ProtonProtocol/proton-testnet.start](https://github.com/ProtonProtocol/proton-testnet.start)—宝腾官方测试网手册。
*   [https://medium . com/EO sphere/proton-technical-how-to-1-6 dab 1c 2 a 394 a](/eosphere/proton-technical-how-to-1-6dab1c2a394a)—手动由 [Ross Dold](https://medium.com/u/eb1aa3f4d9cf?source=post_page-----9b1420fef91b--------------------------------) 发自 [EOSphere](https://medium.com/u/6a21a6208ebb?source=post_page-----9b1420fef91b--------------------------------) BP。

❗️ **从手册中可能看不清楚，所以我想指出，出于安全原因，你不应该使用你的帐户的“所有者/活动”密钥来运行“regproducer”和在 *config.ini* 文件中——相反，你应该为签名块生成一个单独的密钥对。**

请记住，这些信息在阅读时可能已经部分过时，因为软件的新版本会定期发布，或者需求会发生变化。不过，文档更新可能需要一些时间。

虽然手册中提到了这一点，但人们经常会忽略这一点:不要忘记禁用 BP 节点的超频:

> 注释掉 eos-vm-oc-enable 和 EOS-VM-OC-compile-threads(EOS VM OC 不能在块签名节点上使用)

❗️ **重要提示:没有 VPS 和车库托管的硬件，只有裸机服务器和数据中心级服务适合签署区块！**

不同手册的技术要求可能有所不同，但宝腾在[这篇官方文章](https://blog.protonchain.com/how-to-become-a-block-producer-on-proton/)中规定的技术要求对于此时的生产者节点来说是最准确的:

*   CPU:针对性能模式调整的 3.5 Ghz 以上处理器
*   内存:64GB 以上
*   驱动器:1TB+固态硬盘(NVMe 首选)
*   带宽:50 兆比特/秒+

我们使用与 Core i9 11900K 类似的配置。

**❗️And 还有一件更重要的事情:你必须让你的 Testnet 节点一直运行——在你开始在 Mainnet 上运行之前，它不仅仅是用来玩的！**

## 6.请求在 Testnet 上注册生产者节点的权限

有一个特殊的[许可门户](https://permission.testnet.protonchain.com/login)，你必须在那里申请许可来注册你的 BP。您需要连接您的钱包并请求“注册制作人”权限。官方的 WebAuth.com 质子钱包不是为 Testnet 设计的，所以你需要一个通用的 EOSIO [锚钱包](https://greymass.com/en/anchor/)，由 [Greymass](https://medium.com/u/92f7ec102e17?source=post_page-----9b1420fef91b--------------------------------) 生产，质子块生产商之一。

在你请求许可之后，它必须被批准。获得批准有两种方式:

*   这个简单又长的问题:问质子测试网电报组 EOSUSA 的 Michael。
*   推荐的方法:创建一个多签名交易-这是 EOSIO 提供的一种机制，用于提出可以由一组活跃的区块生产者或委员会成员批准的提案。[下面是](/@eosusa.michael/creating-multisig-for-proton-regprod-permissions-3cb46b0ea235) [EOSUSA Michael](https://medium.com/u/7a99533ec178?source=post_page-----9b1420fef91b--------------------------------) 写的手册，避免人们使用第一种方式。😂

创建提案后，您必须获得提案中指定的至少两方(Mainnet 为三方)的批准。你必须找到 Telegram 里的那些人，给他们链接，让他们批准你的提议。这可能不容易，但你必须熬过来。😁

## 7.在 Testnet 上注册您的生产者节点

这肯定是所有步骤中最容易的一步——当您获得许可后，您需要执行" *cleos regproducer"* 命令，这在手册的第 5 步中有所描述。

> ✅我们的第一个里程碑——我们于 2021 年 12 月 3 日在 Testnet 上注册了 BROTON BP。

## 8.为您的 Testnet producer 节点获得一些投票，使其进入时间表

要开始生产积木，你需要一些投票才能进入前 21 名。为了获得选票，你应该问问 EOSUSA 的 Michael。

简单介绍一下工作流程…迈克尔负责审查所有区块生产商候选人，并为由管理委员会成员组成的委员会准备信息。委员会会议每两周举行一次。迈克尔本人可以添加投票，但要确保迈克尔知道你。您的节点可能随时开始产生数据块，您必须做好准备。

## **9。在 Testnet 上成功签署至少两周的区块**

当您完成前面的所有步骤后，您的工作就是监视您的节点，并等待您获得在 Mainnet 上注册的批准。

我们利用这段时间在我们的网站上填充内容，并在社交网络上建立一个社区——这就是我建议你去做的。

**你应该知道的❗️Some 必备知识:**

*   创建一个块有一个推荐的执行时间——**0.35 ms**。确保不要超过它！起初，我们使用了一个不太强大的服务器，平均约为 0.37——这是拒绝的原因，因此我们因为额外的迭代损失了近一个月的时间。
*   不要错过查房！错过回合也是不批准你进入 Mainnet 的原因。如果需要运行维护，应该取消注册节点，并在维护完成后重新注册。请记住，在执行*“unregprod”*之后，应该过一段时间，您的节点才会脱离计划。

【Mainnet 的大部分实际情况是:当您注销一个节点时，您仍然保留您的投票，但是如果有人决定在此期间更新他们的投票，您的节点将从 block producers 列表中消失，在这种情况下，您将失去投票。

以下是一些有用的链接:

*   [质子测试网监控器](https://api.monitor.testnet.protonchain.com/#home)由[密码器](https://medium.com/u/3f09092182c5?source=post_page-----9b1420fef91b--------------------------------)控制
*   [区块生产商基准](https://www.alohaeos.com/tools/benchmarks#networkId=19&timeframeId=1&outliers=0)由 [Aloha EOS](https://medium.com/u/149648a0ecfe?source=post_page-----9b1420fef91b--------------------------------) 提供
*   [Testnet Aloha 可靠性跟踪器](https://t.me/Proton_Testnet_Aloha_Tracker)由 [Aloha EOS](https://medium.com/u/149648a0ecfe?source=post_page-----9b1420fef91b--------------------------------)
*   [EOSIO 仪表盘](https://proton-testnet.eosio.online)由 [EOS 哥斯达黎加](https://medium.com/u/6c93bf741549?source=post_page-----9b1420fef91b--------------------------------)

## 10.创建连接到质子主网的节点

当我们得到批准时，我们用我们的 Testnet 两个星期的时间来设置 Mainnet 节点。

与第 5 步相同，但有具体的手册:

*   [https://github.com/ProtonProtocol/proton.start](https://github.com/ProtonProtocol/proton.start)—质子官方维护网手册。

## 11.请求在 Mainnet 上注册生产者节点的权限

在等待批准的同时，提前请求*“Reg producer”*权限——Mainnet 有一个不同的[权限门户地址。](https://permission.protonchain.com/login)

在我们的案例中，我们不需要创建一个多签名提案来获得批准——当时机成熟时，Michael 亲自批准了它，所以也许你会像我们一样幸运…😁

✅ *我们的第二个里程碑——我们于 2022 年 3 月 9 日在宝腾 Mainnet 上注册。*🍾哇，我们花了三个多月才来到这里！虽然，有一些原因…

## 12.在 Mainnet 上注册您的生产者节点，并准备生产块！

执行" *cleos regproducer"* 命令—这次是在 Mainnet 上。就是这样！

庆祝一点，但不要太多，因为现在你对质子区块链的运营负有重大责任——在任何时候，你都必须准备好开始生产积木。然而，这只是理论上的——实际上，你必须努力说服人们为你的 BP 投票。

## 13.要求奖励

关于奖励，你应该知道以下几点:

1.  奖励有两种:“投票工资”和“整块工资”。所有区块制作人根据自己的票数赚取投票奖励；区块奖励只支付给生产区块最多的 21 家区块生产商。(砌块生产商生产砌块…🤯)
2.  你应该每天申请一次奖励，因为如果你不这样做，你的投票奖励将在其他申请的制作人之间分配。查看[这篇文章](https://github.com/TelosGlobal/claim_rewards)(为 Telos 编写，但也适用于 Proton)了解如何自动完成申请程序。

不要使用您的"*所有者/活动"*密钥申领奖励或任何其他脚本，这是不安全的。最好为每个场景创建不同的具有有限权限的密钥。要申领奖励，请创建一个单独的密钥，仅包含一个“申领奖励”权限。

希望我们的经历对某个人有帮助。与此同时，这次阅读即将结束，但我们不是在说再见——这只是一个开始…🚀⚛️🤙

***下次我们来总结一下作为一个区块制作人一个月的工作成果。敬请关注——这会很有趣的！🤙***

要了解更多关于质子和不要错过重要的更新，我们建议你:

*   跟随我们的媒体页面
*   [在 Twitter 上关注我们](https://twitter.com/brotonbp)
*   加入我们的电报组

此外，你可以在我们的网站上看到入门指南，快速浏览宝腾。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [AscendEx 保证金交易](https://coincodecap.com/ascendex-margin-trading) | [Bitfinex 赌注](https://coincodecap.com/bitfinex-staking) | [bitFlyer 点评](https://coincodecap.com/bitflyer-review)
*   [Bitget 回顾](https://coincodecap.com/bitget-review)|[Gemini vs block fi](https://coincodecap.com/gemini-vs-blockfi)cmd |[OKEx 期货交易](https://coincodecap.com/okex-futures-trading)
*   [AscendEx Staking](https://coincodecap.com/ascendex-staking)|[Bot Ocean Review](https://coincodecap.com/bot-ocean-review)|[最佳比特币钱包](https://coincodecap.com/bitcoin-wallets-india)
*   [霍比评论](https://coincodecap.com/huobi-review) | [OKEx 保证金交易](https://coincodecap.com/okex-margin-trading) | [期货交易](https://coincodecap.com/futures-trading)
*   [网格交易机器人](https://coincodecap.com/grid-trading) | [Cryptohopper 审查](/coinmonks/cryptohopper-review-a388ff5bae88) | [Bexplus 审查](https://coincodecap.com/bexplus-review)