# 如何阅读智能合同

> 原文：<https://medium.com/coinmonks/how-to-read-smart-contracts-816d0da2b146?source=collection_archive---------0----------------------->

## 如何阅读智能合同系列文章的第一部分。本教程主要是为那些想学习如何理解密码世界，但对协议、区块链的内部机制等没有深入了解的爱好者编写的。

![](img/0d0eff6606ca87da878ceb2e61783737.png)

**此素材由 Alex Kruegger(Telegram:@ Kruegger)创作，** [**AK74-Lab 电报频道**](https://t.me/ak74lab) **。** [**译自 swap.net 项目组**](https://swap.net/) **。**

# DeFi 基础

## ***智能合约***

智能契约是在区块链节点上执行的代码，执行的结果(如果在程序中说明)存储在区块链的一个特殊存储库中，即**持久性数据**。智能合同代码一旦上传到区块链，就会被额外锁定，以防止对代码的任何意外或故意更改。

智能合约功能可以从外部(从用户的钱包或从另一个合约)调用，并分为两大组:
**-不改变持久性数据**(仅从区块链读取)
**-改变持久性数据**

调用第一组函数不会耗费任何汽油或金钱，也不会超出最近的节点(Balance of、TotalSupply、Allowance)。在 **BSC 扫描**中，这些功能在**读取**选项卡下。

调用第二组函数变成了一个完整的事务，它被挖掘，包含在块中，其结果被写入区块链(Approve，Transfer，TransferFrom)。在 **BSC 扫描**中，这些功能都在**写**选项卡下。

## ***状态区块链***

以太坊和基于以太坊的区块链(多边形，BSC 等。)都是**状态的区块链。**每个地址在区块链中存储其余额**的**值**为区块链(ETH、BNB、MATIC 等)的本币**。).每个**智能合约**在区块链中存储其持久变量的**值。区块链的当前状态由网络中所有现有地址的平衡和区块链中所有智能合约的持久性变量的当前值来描述。**

## ***账目***

你第一次创建钱包时写下的**种子短语** (12 个单词)使用 **BIP 39** 协议转换成私钥，使用 **ECDSA** (椭圆曲线数字签名算法)转换成公钥，使用哈希和修剪转换成你在区块链的地址。

**种子短语→私钥→公钥→地址**

您将总是从相同的种子短语中获得相同的地址和余额。将您的帐户转移到另一个钱包(MetaMask、Trust Wallet、SafePal、Coin98 等)。)您只需使用保存的种子短语在新钱包上恢复您的帐户。请小心使用此短语，因为它会提供您帐户的完整访问权限。

## ***代币在哪里？***

对于每个账户(地址)，区块链只存储该地址的区块链本地硬币余额，仅此而已。您在每个购买的令牌中的地址余额存储在该令牌的智能合约中的**余额**表中，即令牌中的地址/余额。

在 **BSC 扫描**中，该表显示在“**支架**选项卡上。

必须将代币添加到您的钱包中，才能显示余额。添加后，钱包会向令牌的智能合约查询您帐户的当前余额，并将其显示在界面中。

## ***一个地址—多条链***

以太坊是第一个围绕智能合约思想建立的区块链。它催生了许多只在共识算法和事务气体上互不相同的克隆体。这就是为什么你可以为 BSC，以太坊，多边形区块链使用相同的地址。

想象一下，拿着 0x…bc19 的车票站在火车站。你身边有很多平台叫以太坊，BSC，多边形等等。在他们附近是不同的铁路和火车:在煤上，一个核反应堆，一些仍然由马牵引。但是每个都站在铁轨上，到处都是机车和货车。你的票总是粘在任何站台上任何车厢的座位上。

## 综上所述

*   帐户的密钥是一个**种子短语/秘密密钥**，用于识别在线地址并提供帐户的完全访问权限
*   代币余额在该代币的智能合约中
*   你可以为所有基于以太网的区块链使用一个地址
*   **智能合约**是存储在区块链中的**可变程序+可变数据**
*   一个**智能契约**有两组可以从外部调用的函数——不改变区块链状态的函数(**读**)和改变状态的函数(**写**)

# ERC 20/BEP 20 接口作为令牌契约的基础，分解契约功能。

## 什么是接口

**界面—** 对某些对象的外部影响(控制)以及对象对这种控制的反应的描述。

比如汽车驾驶。界面是一组控件(方向盘、踏板、变速箱)和汽车对这些控件使用的响应。

## *ERC-20 接口*

目前，已经创建了许多令牌，并且每天都在创建。我们可以以同样的方式与任何令牌进行交互—发送、交换、批准等。**那么这种统一是怎么来的呢？**

令牌必须“实现”ERC 20/BEP 20 接口。实现意味着智能令牌协定必须包含一组定义好的函数和参数，并对这些函数做出明确的反应(智能协定应该做什么)。

## *EIP 中定义的 ERC20 标准的接口。*

**功能**

*   [totalSupply()](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-totalSupply--)
*   [(账户)余额](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-balanceOf-address-)
*   [转账(收款人，金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-)
*   [转账人(发件人、收件人、金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transferFrom-address-address-uint256-)
*   [津贴(所有者、支出者)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-allowance-address-address-)
*   [批准(支出者，金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-approve-address-uint256-)

**事件**

*   [转移(从、到、值)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-Transfer-address-address-uint256-)
*   [批准(所有者、支出者、价值)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-Approval-address-address-uint256-)

**每个函数调用还有两个参数:
msg.sender** —交易来自的地址(谁调用了函数)
**msg . value**—随交易发送的令牌数量(ETH/BNB)

**事件—** 一种将信息从智能合约向外传递到调用该合约的 web3 程序的方式。作为一个复选框，表示已经进行了这样的操作。

## ERC 20 功能描述

让我们将 6 个功能分为两组:

读取功能(仅在区块链上读取):

*   [totalSupply()](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-totalSupply--) —显示令牌的发行总量
*   [(账户)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-balanceOf-address-)余额—显示地址[账户](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-balanceOf-address-)的余额
*   [津贴(所有者、支出者)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-allowance-address-address-) —显示允许[支出者](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-allowance-address-address-)借记[所有者](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-allowance-address-address-)的代币总额(检查[批准](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-approve-address-uint256-)

编写函数(更改区块链):

*   [转账(收款人，金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-) -从发件人向[收款人](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-)转账令牌[金额](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-)
*   [transferFrom(汇款人、收款人、金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transferFrom-address-address-uint256-) -转账令牌[金额](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-)从[汇款人](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transferFrom-address-address-uint256-)到[收款人](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-transfer-address-uint256-)
*   [批准(支出者，金额)](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-approve-address-uint256-) -允许[支出者](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-approve-address-uint256-)从 msg.sender 余额中借记令牌[金额](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-approve-address-uint256-)。(检查[余量](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#IERC20-allowance-address-address-)

## 综上所述

*   有一个 ERC-20 标准描述了接口(函数、它们的参数和返回值)，该接口必须实现智能合约才能被称为令牌。
*   如果智能合约实现了 ERC-20 接口，那么我们就可以在任何可以使用令牌的地方使用它——将其交换给 DEX，互相转发，烧掉等等。合同实际上是什么并不重要。
*   如果某样东西看起来像鸭子，走路像鸭子，叫起来像鸭子，我们可以把它当作鸭子，不管它实际上是什么

# 处理合同/示例时会发生什么

**示例**:

*   本决定创建自己的令牌。他采用了 ERC20 的最标准实现，更改了名称、编号(1，000)，规定在创建合同时必须将所有 1，000 个令牌转让给他，并将智能合同部署到区块链中。

*智能合同执行一个构建器函数(在部署合同时执行一次的特殊函数)，该函数初始化内部变量，创建两个空表—* ***余额和容差*** *，然后调用****mint****函数，该函数在* ***余额中创建第一行:
-* BEN — 1000**

他正在完成这项工作。合同准备好了。

*   **本决定给他的朋友伊万和杰克每人 100 枚代币。**

*本的钱包向智能令牌合约发起两笔交易:* ***转账(伊凡，100)*** *和* ***转账(杰克，100)*** *。在这种情况下，谁应该被记入硬币的借方由谁发送交易来确定——本的余额****(msg . sender)****。*

*智能合约简单地通过添加两行并在 Ben 处更改金额来更改表格:* **-Ben-800
-IVAN-100
-JAKE-100**

*   **本决定将代币放在兑换处，所以他去了煎饼店(例如)并创建了代币-BNB 流动性对(800 个代币-2 个 BNB)。**

*煎饼路由器创建了一个流动性对，本将 800 个令牌和 2 个 BNB 转移到其中，结果在另一个宇宙的某个地方，一行****CAKE-LP-Token—2****出现在 BNB 契约中，令牌契约表现在看起来是这样的:*
**-本— 0
-伊万— 100
-杰克—100
-CAKE-LP-Token/煎饼路由器— 800**

*   **伊凡决定再买 100 个代币，他去煎饼店，说“我想给 BNB 买 100 个代币”**

*pancake 路由器向流动性对询问对 BNB 的令牌的当前汇率(使用* ***AMM 算法*** *)，并告诉 Ivan* — **“这将花费你 0.25 BNB +费用。”**

*   伊凡给煎饼送去 0.25 BNB，然后等着他的代币。

*pan ckake 路由器看到钱已经到了，在智能令牌契约上创建一个交易:* **代表 LP 对的 transfer(Kolya，100)。**

智能合约通过借记这对夫妇的账户和贷记 Ivan 的账户来完成请求。结果:
***-*BEN—0
-IVAN—200
-JAKE—100
-CAKE-LP-Token—700**

***pan ckae 路由器将 0.25 BNB*** *发送到宇宙的另一端，在 LP 对的另一部分上，BNB 契约中****CAKE-LP-Token****对* ***的值从 2 增加到 2.25***

*   此时，杰克决定卖掉所有的代币，买下比纳蒙。他走向煎饼，说:“我想卖 100 个代币”。

*pancake 路由器向 LP 询问到 BNB 的令牌的当前汇率(使用 AMM 算法)，并告诉杰克* — **这将花费你 0.37 BNB +的费用。**

*然后，Pancake 向智能令牌合约询问 JAKE 是否允许他(Pancake)从他的账户中借记令牌，为此，它向智能令牌合约询问:* **津贴(Jake，Pancake-router)函数**的结果

*Pancake 路由器逻辑上不信任任何人，所以所有借记交易都以他的名义进行，这就是为什么 Jake 必须说他信任 Pancake 来借记他的令牌余额*

*杰克以前没有卖出过任何东西，结果= 0。Pancake 看到这一点，在 swap 界面为 Jake 画了一个* **【批准】** *按钮。*

*   **杰克推送“批准”**

*杰克的钱包向智能令牌合同发起交易:approve(pancake 路由器，99999999999999999)，允许路由器用他(路由器)需要的任意多的令牌记入他的账户的借方。*

*实际上，更正确的做法是，只对每笔交易的金额给予许可，但人们都是懒惰的动物，因此通常没有人会费心将最大可能数量作为允许借记的代币数量。在我们的例子中，为了简单起见，有很多 9。*

*智能令牌合同通过向津贴表添加一行来执行操作:* **杰克— (Pancake 路由器，99999999)并生成批准事件**

*Pancake 路由器看到此事件，并再次查询智能合同以获得函数的结果:* **津贴(JAKE，punk 路由器)** *。*

*如果智能合约返回 9999999999，并且该值大于或等于当前交易的金额，则路由器将从界面中移除* **【批准】** *按钮，并启用* **【交换】** *按钮。如果返回 0，* **【批准】** *按钮不消失，* **【互换】** *按钮仍然不活动。*

*   **杰克推出“交换”**

*pan ckake 路由器命令 LP 对的 BNB 部分向 Jake 发送 0.37 BNB，并通过调用* **transferFrom(JAKE，punk ruther，100)** *函数在智能令牌合同上创建一个交易。*

智能合约检查允许 Pancake 从 Jakes 的地址借记硬币的津贴行表，找到它并执行操作。

*现在表是这样的:* ***-* 本— 0
-伊万— 200
-杰克— 0
-蛋糕—LP—令牌— 800**

*   **一切都解决了，每个人都很开心，所有的操作都已经执行了**

总而言之:

*   使用**转移**功能将代币从交易发送方的余额(通常是用户的钱包)转移到任何其他地址。
*   令牌可以从任何地址发送到任何地址，只要通过批准功能允许借记债务人的地址。
*   函数 **approve** 由地址的所有者调用，他允许另一个地址从他的余额中扣除代币。
*   权限可以通过**权限**功能查看。
*   在任何转移中，代币只是从资产负债表的一行移到另一行，永远不会离开智能合约的范围。
*   如果你想预批准代币出售，那么进入**代币**智能合约，**写**标签，在那里寻找**批准**功能，插入你想交换的地方的智能**路由器**合约的地址。**在我们的例子中，这是 Pancake 路由器的地址:0x 10 ed 43 c 718714 EB 63 D5 aa 57 b 78 b 54704 e 256024 e**

在本教程中，我们已经了解了关于你的账户、合同的基本内容，并了解了它们之间交互的要点。强烈建议你参加一个基础编程课程，以便能够阅读最低水平的合同代码，并至少大致了解特定代码的作用。

**非常感谢从**[**Swap.net 团队**](https://twitter.com/NFTSwapnet) **到** [**亚历克斯·克鲁格**](https://t.me/ak74lab)

## 作者:Alex Kruegger[(TG @ Kruegger)](https://t.me/ak74lab)，频道—[https://t.me/ak74lab](https://t.me/ak74lab)

## 由 SWAP.NET 团队
翻译官方网站—[https://swap.net/](https://swap.net/)推特—[https://twitter.com/NFTSwapnet](https://twitter.com/NFTSwapnet)不和—[https://t.co/uzz0Qt12tf](https://t.co/uzz0Qt12tf)中—[https://medium.com/@NFTSwapnet](/@NFTSwapnet)Docs&白皮书—[http://docs.swap.net](https://t.co/5qc7Mxt2p5)