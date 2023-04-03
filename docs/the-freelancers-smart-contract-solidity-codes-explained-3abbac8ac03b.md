# 自由职业者的智能合同:可靠性代码解释

> 原文：<https://medium.com/coinmonks/the-freelancers-smart-contract-solidity-codes-explained-3abbac8ac03b?source=collection_archive---------3----------------------->

这是 4 部分系列的第 3 部分，记录了我为自由职业者构建一个[分散式应用程序](https://ethereum.org/en/dapps/) (DApp)的过程，该应用程序为他与客户一起承担的项目接收多个部分付款。

关于这个过程的业务逻辑的逐步指南，请参考本系列的第 1 部分。有关分散式应用程序如何工作的演示，请参考[第 2 部分](/coinmonks/the-freelancers-smart-contract-dapp-demo-6f5b23a82bfa)。该项目的源代码可以在该项目的 [Github 库](https://github.com/jacksonng77/freelancer)中找到。

在本系列的第三部分，我将介绍自由职业者智能合同背后的可靠性代码。

![](img/a481b31cdf94c96c35d3b58ddbb77c61.png)

Photo by [Woody Yan](https://unsplash.com/@woodyyan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/soil-hand?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

**状态**

```
enum ScheduleState {planned, funded, started, approved, released}
enum ProjectState {initiated, accepted, closed}
```

有两种状态`enum`——一种用于时间表，另一种用于项目。智能合同中的每个进度(如设计阶段、开发阶段、实施阶段)都有 5 种状态，即- `planned`、`funded`、`started`、`approved`和`released`。

该项目有三种状态，即`initiated`、`accepted`和`closed`。

**结构&全局变量**

```
struct schedule{
        string shortCode;
        string description;
        uint256 value;
        ScheduleState scheduleState;
}  

int256 public totalSchedules = 0;
address payable public freelancerAddress;
address public clientAddress;
ProjectState public projectState;

mapping(int256 => schedule) public scheduleRegister;
```

时间表结构包含以下变量，即:

*   `shortCode`:如设计阶段的“DSG”
*   `description`:例如“设计阶段”
*   `value` : 1e .例如 ETH
*   `scheduleState`:该日程当前所处的状态之一，即`planned`、`funded`、`started`、`approved`和`released`

变量`totalSchedule`跟踪这个项目的总进度数。变量`freelancerAddress`存储自由职业者的钱包地址。变量`clientAddress`存储客户端的钱包地址。变量`projectState`存储项目的当前状态。

地图用于存储项目的所有时间表。

**修改器**

```
modifier condition(bool _condition) {
		require(_condition);
		_;
}modifier onlyFreelancer() {
		require(msg.sender == freelancerAddress);
		_;
}modifier onlyClient() {
		require(msg.sender == clientAddress);
		_;
}

modifier bothClientFreelancer(){
		require(msg.sender == clientAddress || msg.sender == freelancerAddress);
		_;	    
}
```

这些在智能合同的功能中使用，以验证是否允许客户和/或自由职业者调用它们。有些功能，如`releaseFunds()`(允许在计划结束时释放资金)只能由自由职业者调用。其他函数，如`approveTask()`(批准向日程表添加新任务)只能由客户端调用。还有像`endProject()`这样的函数，客户和/或自由职业者都可以调用。

```
modifier inProjectState(ProjectState _state) {
		require(projectState == _state);
		_;
}
```

`inProjectState()` 修饰符检查项目当前是否处于特定的状态(例如，关闭)。某些功能只有在项目处于某种状态时才能执行。例如，只有当项目处于启动状态时，才能添加新的计划，而当项目已经关闭时，则不能添加。

```
modifier **in**ScheduleState(int256 _scheduleID, ScheduleState _state){
        require((_scheduleID <= totalSchedules - 1) && scheduleRegister[_scheduleID].scheduleState == _state);
        _;
}
```

`inScheduleState()`修改器检查所讨论的时间表是否处于特定状态(例如，已拨款)。这允许函数测试一个调度是否准备好进入下一个状态——例如，一个调度只有在当前处于`planned`状态时才能进入`funded`状态。

```
modifier ampleFunding(int256 _scheduleID, uint256 _funding){
        require(scheduleRegister[_scheduleID].value == _funding);
        _;
}modifier noMoreFunds(){
        require(address(**this**).balance == 0);
        _;
}
```

`ampleFunding()` 修饰符检查一个调度的资金是否等于它应该收到的资金。例如，“设计阶段”花费 1 ETH。此修改人检查以确保客户确实已将 1 ETH 资金投入该计划。

`noMoreFunds()`修饰符检查智能契约是否仍然持有任何 ETH 的托管权。

**功能**

```
constructor()
{
        freelancerAddress = payable(msg.sender);
        projectState = ProjectState.initiated;
}
```

`constructor()` 函数将启动该智能合约的人的钱包地址保存在`freelancerAddress`变量中，并将`projectState`设置为 initiated。

```
**function** **addSchedule**(string memory _shortCode, string memory _description, uint256 _value)
    **public**
    **inProjectState**(ProjectState.initiated)
    **onlyFreelancer**
{
        schedule memory s;
        s.shortCode = _shortCode;
        s.description = _description;
        s.scheduleState = ScheduleState.planned;
        s.value = _value;
        scheduleRegister[totalSchedules] = s;
        totalSchedules++;
        emit scheduleAdded(_shortCode);
}
```

`addSchedule()`只能在项目处于发起状态时调用。只能由发起此智能合约的人员执行(`onlyFreelancer`)。该函数初始化一个新的日程，并将该日程的`shortCode`、`description`和`value`保存到`scheduleRegister`映射中。它增加了变量`totalSchedule`,以跟踪这个项目中计划的总数。

```
**function** **acceptProject**()
    **public**
    **inProjectState**(ProjectState.initiated)
{
        clientAddress = msg.sender;
        projectState = ProjectState.accepted;
        emit projectAccepted(msg.sender);
}
```

当`acceptProject()`被调用时，它将执行它的人的钱包地址保存到`clientAddress`变量中。然后将`projectState`设置为`accepted`。调用`acceptProject()`的人成为这个项目的客户。

```
**function** **fundTask**(int256 _scheduleID)
    **public**
    **payable**
    **inProjectState**(ProjectState.accepted)
    **inScheduleState**(_scheduleID, ScheduleState.planned)
    **ampleFunding**(_scheduleID, msg.value)
    **onlyClient**
{
        scheduleRegister[_scheduleID].scheduleState = ScheduleState.funded;
        emit taskFunded(_scheduleID);
}
```

当客户准备好允许自由职业者按照特定的时间表开始工作(如设计阶段)时，他通过执行`fundTask()`来为任务提供资金。`fundTask()` 仅当满足以下条件时才可调用:

*   `payable` -调用 fundTask()时存放 ETH
*   `inProjectState`:接受——项目必须被客户接受。
*   `inScheduleState`:已计划——待拨款的进度处于计划状态
*   `ampleFunding` -存入智能合同的 ETH 等于待资助计划的价值(即，如果设计阶段花费 1 ETH，则必须存入 1 ETH)
*   `onlyClient` -该功能仅由客户端执行

当执行时，该时间表的状态从`planned`变为`funded`。

```
**function** **startTask**(int256 _scheduleID)
    **public**
    **inProjectState**(ProjectState.accepted)
    **inScheduleState**(_scheduleID, ScheduleState.funded)
    **onlyFreelancer**
{
        scheduleRegister[_scheduleID].scheduleState = ScheduleState.started;
        emit taskStarted(_scheduleID);
}
```

自由职业者执行`startTask()`功能是为了表明他已经开始从事一项特定的任务。`startTask()`只有满足以下条件时才可调用:

*   接受-客户必须已经接受了这个项目
*   `inScheduleState`:已拨款-客户必须已为此计划拨款
*   `onlyFreelancer`:只有自由职业者才能调用这个功能。

当执行时，该时间表的状态从`funded`变为`started`。

```
**function** **approveTask**(int256 _scheduleID)
    **public**
    **inProjectState**(ProjectState.accepted)
    **inScheduleState**(_scheduleID, ScheduleState.started)
    **onlyClient**
{
    scheduleRegister[_scheduleID].scheduleState = ScheduleState.approved;
    emit taskApproved(_scheduleID);
}
```

客户执行`approveTask()`功能来表明他已经看到并批准了一个任务。`approveTask()`仅当满足以下条件时才可调用:

*   `inProjectState`:已接受——客户必须接受这个项目
*   开始-自由职业者必须已经开始这项任务的工作
*   `onlyClient` -只有客户可以批准任务。

当执行时，该时间表的状态从`started`变为`approved`。

```
**function** **releaseFunds**(int256 _scheduleID)
    **public**
    **payable**
    **inProjectState**(ProjectState.accepted)
    **inScheduleState**(_scheduleID, ScheduleState.approved)
    **onlyFreelancer**
{
        freelancerAddress.transfer(scheduleRegister[_scheduleID].value);
        scheduleRegister[_scheduleID].scheduleState = ScheduleState.released;
        emit fundsReleased(_scheduleID, scheduleRegister[_scheduleID].value);
}
```

自由职业者执行`releaseFunds()` 功能，将智能合同保管的资金释放到他的钱包地址。这意味着一项任务的完成，因此，要向自由职业者支付报酬。`releaseFunds()`仅当满足以下条件时才可调用:

*   接受-客户必须已经接受了这个项目
*   批准-客户必须已经接受了自由职业者为这项任务所做的工作。
*   `onlyFreelancer`:只有自由职业者可以调用此功能向自己释放资金

执行时，`releaseFunds()`会将智能合同为此任务保管的 ETH 转移到自由职业者的钱包地址。它还将时间表的状态从`approved`更改为`released`。

```
**function** **endProject**()
    **public**
    **bothClientFreelancer**
    **noMoreFunds**
{
        projectState = ProjectState.closed;
        emit projectEnded();
}
```

`endProject()`功能标志着项目的完成。仅当满足以下条件时，此函数才可调用:

*   `noMoreFunds`:本项目不再托管任何 ETH。所有的 ETH 都被释放给了自由职业者。

执行时，`endProject()`将项目状态更改为关闭。

```
**function** **getBalance**()
    **public**
    **view**
    **returns** (uint256 balance)
{
        **return** address(**this**).balance;
}
```

`getBalance()`将智能合约持有的总余额返回给调用者。知道智能合约地址的可以打`getBalance()`。

下一步是什么？

这个项目的源代码可以在我的 [Github 库](https://github.com/jacksonng77/freelancer)中找到。

在本教程的最后一部分，我将解释自由职业者分散式应用程序的基于 Javascript 的代码。敬请期待！

1.  自由职业者的智能合同:如何运作
2.  [自由职业者的智能合同:DApp 演示](/coinmonks/the-freelancers-smart-contract-dapp-demo-6f5b23a82bfa)
3.  自由职业者的智能合同:可靠性代码解读(这一部分)
4.  自由职业者的智能合同:DApp 法典解读

如果您喜欢本教程，也许您也希望阅读:

*   [自由职业者智能合同](/coinmonks/the-freelancers-smart-contract-how-it-works-fda5e1fddf8d):自由职业者和他的客户之间的一个支付系统，以确保交货和付款。
*   [Ropsten 以太坊龙头](/coinmonks/ropsten-ethereum-faucet-web-app-cc9a50ee45fd):我做了一个以太坊龙头在 Ropsten 网络上发布 ETH。
*   [区块链投票](/coinmonks/voting-on-a-blockchain-how-it-works-3bb41582f403):以太坊投票 DApp 的实现。
*   [使用 Kaleido 在 10 分钟内部署一个私有以太坊区块链](/coinmonks/deploy-a-private-ethereum-blockchain-in-10-minutes-with-kaleido-73c21a26d5bb):在瞬间启动并运行一个私有以太坊区块链。
*   [演示解释智能合约](/coinmonks/smart-contract-explained-by-demonstration-93b06e938474):托管服务智能合约 DApp 的演示——在我看来，这是向外行人解释区块链是什么的最快方式。
*   [以太坊 IOT Kid Grounding Device](/coinmonks/ethereum-iot-kid-grounding-device-iv-arduino-in-retrospect-b7a32e5ec185) :我将区块链与物联网结合的尝试。
*   [彩票作为智能合约](/coinmonks/lottery-as-a-smart-contract-the-business-logic-3bd22d3a6c4e):去中心化彩票，在以太坊区块链上构建彩票系统的尝试。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

## 也阅读

[](https://coincodecap.com/best-telegram-channels) [## 40 个最佳电报频道，用于加密、电影、表演和演讲| CoinCodeCap

### 免费下载所有电影。德国免费加密信号。下载讲座。CoinCodeCap 经典，网飞电影等。是……

coincodecap.com](https://coincodecap.com/best-telegram-channels) [](https://coincodecap.com/keevo-wallet-review) [## Keevo 钱包点评:是最安全的硬件钱包吗？2022 | CoinCodeCap

### 在这篇 Keevo Wallet 评论中，我们将讨论他们如何改变我们看待硬件钱包的方式。基沃是…

coincodecap.com](https://coincodecap.com/keevo-wallet-review) [](https://coincodecap.com/best-social-trading-platforms) [## 2022 年 5 大最佳社交交易平台

### 5 个最佳社交交易平台阅读加密产品评论和比较，了解比特币交易和…

coincodecap.com](https://coincodecap.com/best-social-trading-platforms) [](https://coincodecap.com/blockfi-review) [## BlockFi 评论:2022 年的利弊和利率

### 今天，我们提出了一个全面的 BlockFi 评论，这是一个成立于 2017 年的加密贷款平台，拥有其…

coincodecap.com](https://coincodecap.com/blockfi-review) [](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) [## 如何在印度购买比特币？2021 年购买比特币的 7 款最佳应用[手机版]

### 如何使用移动应用程序购买比特币印度

medium.com](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) [](/coinmonks/best-crypto-tax-tool-for-my-money-72d4b430816b) [## 加密税务软件——五大最佳比特币税务计算器[2021]

### 不管你是刚接触加密还是已经在这个领域呆了一段时间，你都需要交税。

medium.com](/coinmonks/best-crypto-tax-tool-for-my-money-72d4b430816b) [](https://coincodecap.com/crypto-to-buy-in-2022) [## 9 个 2022 年最值得购买的密码| CoinCodeCap

### 9 个 2022 年最值得购买的加密产品阅读加密产品评论和比较，了解比特币交易和…

coincodecap.com](https://coincodecap.com/crypto-to-buy-in-2022) [](https://coincodecap.com/best-hardware-wallet-bitcoin) [## 存储比特币的最佳加密硬件钱包 2022 | CoinCodeCap

### 硬件钱包是我们存储加密资产的唯一可靠选择。在本文中，我们将讨论 8 个…

coincodecap.com](https://coincodecap.com/best-hardware-wallet-bitcoin) [](/coinmonks/pionex-review-exchange-with-crypto-trading-bot-1e459d0191ea) [## Pionex 评论 2021 |免费加密交易机器人和交换

### Pionex 是为交易自动化提供工具的后起之秀。Pionex 上提供了 9 个加密交易机器人…

medium.com](/coinmonks/pionex-review-exchange-with-crypto-trading-bot-1e459d0191ea) [](/coinmonks/top-3-telegram-channels-for-crypto-traders-in-2021-8385f4411ff4) [## 2022 年密码交易员的三大电报渠道

### 加密信号是来自专业交易者的交易想法，以特定的价格或价格买卖特定的加密货币

medium.com](/coinmonks/top-3-telegram-channels-for-crypto-traders-in-2021-8385f4411ff4) [](https://coincodecap.com/free-crypto-portfolio-trackers) [## 2022 年 5 个最佳免费加密投资组合追踪器

### 在这篇文章中，我们将带你通过一些最好的免费加密投资组合追踪器，让你选择最好的…

coincodecap.com](https://coincodecap.com/free-crypto-portfolio-trackers)