# 彩票 Dapp——可靠性智能合同分解

> 原文：<https://medium.com/coinmonks/lottery-dapp-solidity-smart-contract-breakdown-6f67e50739a3?source=collection_archive---------3----------------------->

![](img/1dfbaf8ca49034627dd4ec7198996bb7.png)

Photo by [Alejandro Garay](https://unsplash.com/@chinitogaray?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/lottery?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你可以在早先的文章[这里](/coinmonks/lottery-dapp-motivation-and-mechanics-36aba14f9034)中读到更多关于彩票机制如何运作以及创造分散型彩票背后的动机。

这篇文章将探讨管理分散型彩票 dApp ( [去分散型彩票](https://github.com/yan-man/lottery-dapp)——因其目标受众而得名)的智能合约，包括一些实现细节。

这里假设你已经有一些关于 Solidity、Javascript、单元测试(Chai 断言和 Waffle)的背景知识，以及智能契约在以太坊中如何工作的一般知识。

源代码可以在这里找到[。](https://github.com/yan-man/lottery-dapp)

您可以在根目录下的`./contracts`文件夹中找到`Lottery.sol`智能契约，以及一个`Random.sol`库来帮助实现基于块号的简单随机数生成。测试可以在`./test`文件夹中找到。

## 典型例子

将参考以下示例彩票场景来解释该合同:

*   a)彩票由`**Owner**` 初始化。造币期开放，允许购买彩票。在任何给定的时间，只允许一个有效的彩票。
*   B) (1) `**Player1**`买 20 张票；②`**Player2**`购买 70 张门票；(3) `**Player1**`再购买 10 张彩票(该彩票共购买 100 张彩票)。因此`**Player1**`有 30%的机会获胜(通过持有 30/100 的未兑现门票)，而`**Player2**`有 70%的机会获胜(通过持有 70/100 的未兑现门票)。
*   c)铸造窗口结束——通过来自`**Owner**`的紧急调用或自行决定。不能再买票了。
*   d)运行抽奖。A `**Winner**`是根据已购买的未兑现彩票的比例随机选择的。中奖资金被存入待提取账户(只有中奖者才能使用)
*   E) `**Winner**`从待处理的提款中提取奖金。

![](img/5e7d85bb5f43f366e19863783488a5d4.png)

a degenerate’s rendering

# `Lottery.sol`智能合同

## 页眉

在初始 Pragma 和 [OpenZeppelin](https://docs.openzeppelin.com/) 导入之后，首先要注意的是控制台导入。这个项目是用 [Hardhat](https://hardhat.org/) 创建的——一个方便的用于测试和前端集成的 Solidity 开发环境。

```
import "hardhat/console.sol";
```

Solidity 中的`console.log`类型特性非常有用——使用 [Truffle 套件](https://trufflesuite.com/)，您几乎需要创建自定义事件来进行测试和日志记录，以打印数据和进行调试。有了 Hardhat，这就简化了—您可以在合同内的任何地方记录数据。

Hardhat 也有使用 ethers.js 而不是 web3.js 的 web3 智能合约集成，我觉得 web 3 . js 更容易使用。

这个合同也是`Ownable` —用特权初始化合同所有者。在这份合同中，`**Owner**`有权创造新的彩票，强制关闭造币期，或者在紧急情况下取消彩票。

`Random.sol`库契约也被导入，通过自定义的`naiveRandInt`函数帮助实现简单的随机性。

## 状态变量

首先，定义`Structs`。

`LotteryStruct`代表每个单独的彩票实例——跨越一个在`startTime`和`endTime`之间定义的铸造周期(默认为 7 天)。`bool`用于跟踪特定彩票抽奖的状态:

*   `inActive`:彩票有效(即`inActive=false`)表示造币周期开放，无效(即`inActive=true`)时由`**Owner**`强制设定或自然结束(即当前时间戳大于`endTime`)。
*   `isCompleted`:默认为`false`。在一次成功的抽奖运行后，中奖奖金作为待提取的奖金被存入并可供中奖者取回，它被设置为`true`。
*   `isCreated`:彩票创建的显式标志，方便在前端用户界面内检查彩票是否已创建。这特别有帮助，因为`lotteries`(`LotteryStruct`结构的集合)是一个映射，[意味着您不能直接确定映射键索引](https://ethereum.stackexchange.com/questions/13021/how-can-you-figure-out-if-a-certain-key-exists-in-a-mapping-struct-defined-insi)是否存在——它们在技术上是存在的，并且被初始化为默认值。

`TicketDistributionStruct`用于表示根据每个彩票抽奖的参与者的彩票分配的指数。它仅在抽奖过程中调用，并帮助为每个玩家分配彩票指数(按玩家第一次购买彩票的顺序连续排列，1-indexed ),这决定了他们的中奖几率。

`WinningTicketStruct`用于表示每张彩票选中的中奖者(由账户地址标识)及其对应的中奖票索引。

> *注意:在这个最初的 v0.1 实现中，变量通常被默认设置为 public，以简化在前端读取它们的值(使用 [Solidity 内置的用于公共变量](https://docs.soliditylang.org/en/v0.8.13/contracts.html#state-variable-visibility)的 getters)。

`MIN_DRAWING_INCREMENT`是设置彩票底价的常量。

`NUMBER_OF_HOURS`是一个常量，如果在部署期间没有设置，则定义默认的制造周期(到 168 小时，一个简单计算的星期)。

`numTotalTickets`和`numActivePlayers`可能看起来没有必要，但它们有助于以有效的方式分别跟踪已购买的未完成彩票和当前彩票的活跃参与者数量:

*   `tickets`是用户地址和他们为给定彩票购买的彩票数量之间的映射。可以通过对活动用户地址上的票据求和来找到票据的总数，但是持续执行该操作的成本很高。
*   `listOfPlayers`是一个玩家数组，但是为了节省汽油，它的值在后续的抽奖中被覆盖而不是被删除。因此，它的长度不是确定玩家数量的可靠来源。想象一个场景，其中 5 个玩家在彩票 1 中是活跃的，但是在彩票 2 中只有 3 个玩家是活跃的。确定玩家 4(位于索引 3)和 5(位于索引 4)在彩票 2 中无效的唯一方法是使用`numActivePlayers`来标识该数组的最后一个有效索引(即`numActivePlayers-1`是最后一个索引，在我们当前的示例中`2`对应于玩家 3)。仅仅搜索给定索引的存在性是不够的。

`prizes`是一个映射，记录每张彩票的奖金数额(其关键字为 lotteryId)。

`winningTickets`是一个映射，记录每一次彩票的中奖者(其关键字为 lotteryId)。

`players`是标记用户是否是当前彩票的活跃玩家的映射。使用这种映射比每次搜索`listOfPlayers`数组来检查一个地址是否有效更方便。

`lotteries`是一个映射，记录了已经部署的彩票列表。

`pendingWithdrawals`是一个映射的映射，允许赢家提取他们的奖金。

# 执行

## 合同部署

合同可以通过 Hardhat 部署。没有显式定义构造函数，因为不需要初始契约参数。使用以下命令部署到本地 Hardhat 节点:

```
$ npx hardhat run scripts/deploy.js --network localhost
```

将运行`deploy.js`脚本(在`/scripts`目录中)，在控制台上打印一些部署信息，并保存合同地址以及 ABI 文件供前端访问。

## a)彩票初始化

彩票通过`initLottery`函数初始化，该函数允许任何用户帐户启动彩票，指定造币时间段的开始时间(作为一个 unixtime int，`startTime_`)和造币窗口允许打开的小时数(`numHours_`)。修饰符(`isNewLotteryValid`)首先检查当前彩票是否处于非活动状态——任何时候只允许一次活动彩票。

一个`LotteryStruct`类型被创建并保存到`lotteries`映射中，默认值被初始化。还会发出一个事件(`LogNewLottery`)。

## b)票据铸造

开奖期开始后，任何账户都可以通过`mintLotteryTickets`功能购买彩票。一个修饰符`isNewPlayerValid`首先检查用户包含的 Eth 数量是否大于底价(即他们至少能买 1 张票)。

然后，我们需要检查用户是当前彩票的回头客还是新玩家。`**Player1**`在我们的典型例子中是步骤(3)中的返回玩家，因为他们已经在步骤(1)中购买了一些门票。

如果他们是新玩家，则需要管理更多的细节——比如检查是否达到玩家限制，或者覆盖旧值或者追加到`listOfPlayers`数组。

然后更新跟踪变量，并发出另一个事件(`LogTicketsMinted`)。

## c)铸造期结束

铸造期可以自行结束，即`endTime`已到达，也可以通过紧急功能`setLotteryInactive`手动结束，该功能只能由合同`**Owner**`调用。

## d)执行抽奖

在铸造期结束后，不能再为该彩票购买更多的彩票。为了开始抽奖，`**Owner**`调用函数`triggerLotteryDrawing`，它执行一些动作。

首先，它通过`_playerTicketDistribution`私有函数将门票分配给活跃的玩家，该函数循环遍历玩家列表，将他们购买的门票合并在一起。根据每位玩家购买的门票数量，他们会被分配一个开始和结束索引。那么他们的简档将为下一次抽奖重置。

在典型的例子中，`**Player1**` 将有一个`startIndex = 1`和一个`endIndex = 30`，因为它们是第一个购买地址，并且在整个铸造期间总共购买了 30 张票(尽管这 30 张票不是一次购买的)。`**Player2**`会有一个`startIndex = 31`和一个`endIndex = 100`，因为他们已经购买了 70 张票。

接下来，调用`_performRandomizedDrawing`，它使用`Random.sol`库函数在所有玩家票券索引的集合中生成一个随机整数。

然后，基于这个生成的中奖投注单索引，它通过`findWinningAddress`函数搜索相应的用户地址。在这个函数中，它首先简化了 1 个活动玩家的琐碎情况。否则，调用递归二分搜索法函数(`_binarySearch`)来查找其票单分布中的开始和结束索引封装了获胜票单索引的用户。

`_binarySearch`还利用`_loopCount`变量作为另一项检查——它限制了递归搜索操作的执行次数。

发出另一个事件(`LogWinnerFound`)。

## e)赢家提取奖金

最后，在中奖者被识别之后，彩票中奖被存入`pendingWithdrawals`变量，并且可以根据[防止重入攻击的合同撤销模式](https://docs.soliditylang.org/en/v0.8.14/common-patterns.html#withdrawal-from-contracts)被分配到中奖账户(发出另一个事件)。

# 随机性

随机性是通过`Random.sol`库实现的，该库通过块号的 blockhash 创建简单的随机数，然后在期望的范围内归一化值。这是一个常见的实现，尽管不是完全安全的，因为它不是可验证的随机的——但只是作为一个基本的简单示例来帮助执行 v0.1 的抽奖。

这种形式的随机性也被用于著名的合同，如[Bored Apes Yacht Club(BAYC)](https://etherscan.io/address/0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d#code)token，目的是“重新索引”其 NFT 的顺序。

# 单元测试

单元测试可以在`./test`目录中找到。在 Hardhat 中使用 [Waffle](https://hardhat.org/guides/waffle-testing) 测试，它部署彩票合同，并在一个类似风格的规范示例的整个生命周期中执行各种检查。

需要进行更多的单元测试，以涵盖所有潜在的故障场景(尤其是访问控制)以及随后的实施 [Chainlink 的 VRF(可验证随机函数)](https://docs.chain.link/docs/chainlink-vrf/)以在绘图期间创建可验证的随机性。

就是这样！像你这样的德根斯的 v0.1 彩票 dApp。享受，并感谢阅读。