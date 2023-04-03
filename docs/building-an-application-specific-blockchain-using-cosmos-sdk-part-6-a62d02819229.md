# 使用 Cosmos SDK Part-6 构建特定于应用程序的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-6-a62d02819229?source=collection_archive---------26----------------------->

欢迎来到这个系列的最后一部分，这里我们将讨论一个非常重要的特性。

![](img/57cc2722895d28e4ac48ddcce2fca679.png)

Photo by [Jeswin Thomas](https://unsplash.com/@jeswinthomas?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/testing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

类似于模块管理器，我们在`app.go`中定义了一个模拟管理器。它基本上是一个对象，包含了实现模拟包的所有模块的列表。每个模块都有自己的`simulation`包，其中包含测试模拟的主要功能:`store decoders, randomized genesis state and parameters, weighted operations and proposal contents`。在星港的帮助下，我们已经在`module`注册了这些方法(在`simulation.go`下)

注意，除了消息，starport 还为每种消息类型搭建了模拟加权操作。(`module_simulation.go`)。让我们更改每种消息类型的加权数字-

```
//module_simulation.goconst (
opWeightMsgCreateDeal = "op_weight_msg_create_chain"
defaultWeightMsgCreateDeal int = 90opWeightMsgCreateContract = "op_weight_msg_create_chain"
defaultWeightMsgCreateContract int = 90opWeightMsgCommitContract = "op_weight_msg_create_chain"
defaultWeightMsgCommitContract int = 50opWeightMsgApproveContract = "op_weight_msg_create_chain"
defaultWeightMsgApproveContract int = 40opWeightMsgShipOrder = "op_weight_msg_create_chain"
defaultWeightMsgShipOrder int = 40opWeightMsgOrderDelivered = "op_weight_msg_create_chain"
defaultWeightMsgOrderDelivered int = 40opWeightMsgCancelOrder = "op_weight_msg_create_chain"
defaultWeightMsgCancelOrder int = 20
*// this line is used by starport scaffolding # simapp/module/const* )
```

我们将为每种消息类型定义随机参数，然后签名并将事务发送到模拟链，以验证事情是否如预期那样工作。注意，模拟还帮助我们测试注册在任何模块上的不变量。

> `Invariant`是一个帮助我们在早期检测到错误并采取行动限制其潜在后果的功能(例如，通过中止链)。

我们将使用小的效用函数来签署和发送交易到模拟链-

```
// simap.go*// SendMsg sends a transaction with the specified message.*func SendMsg(
r *rand.Rand, app *baseapp.BaseApp, ak types.AccountKeeper, bk types.BankKeeper, msg sdk.Msg, ctx sdk.Context, chainID string, gasValue uint64, privkeys []cryptotypes.PrivKey,
) error {
 addr := msg.GetSigners()[0]
 account := ak.GetAccount(ctx, addr)
 coins := bk.SpendableCoins(ctx, account.GetAddress())
 fees, err := simtypes.RandomFees(r, ctx, coins)
 if err != nil {
  return err
 }
 txGen := simappparams.MakeTestEncodingConfig().TxConfig
 tx, err := helpers.GenTx(
 txGen,
 []sdk.Msg{msg},
 fees,
 gasValue,
 chainID,
 []uint64{account.GetAccountNumber()},
 []uint64{account.GetSequence()},
 privkeys...,
)if err != nil {
 return err
}
_, _, err = app.Deliver(txGen.TxEncoder(), tx)if err != nil {
 return err
}
 return nil
}
```

我们还将为每个消息定义模拟功能-

```
// simulation/create_deal.gofunc SimulateMsgCreateDeal(ak types.AccountKeeper,
bk types.BankKeeper,
k keeper.Keeper,
) simtypes.Operation {
return func(r *rand.Rand, app *baseapp.BaseApp, ctx sdk.Context, accs []simtypes.Account, chainID string,
) (simtypes.OperationMsg, []simtypes.FutureOperation, error) {creatorAccount := accs[0]
vendorAccount := accs[1]
commission := r.Intn(80) + 5msg := &types.MsgCreateDeal{
Creator: creatorAccount.Address.String(),
Vendor: vendorAccount.Address.String(),
Commission: uint64(commission),
}err := SendMsg(r, app, ak, bk, msg, ctx, chainID, DefaultGasValue, []cryptotypes.PrivKey{creatorAccount.PrivKey})if err != nil {
return simtypes.NoOpMsg(types.ModuleName, msg.Type(), "CreateDeal"), nil, nil
}return simtypes.NewOperationMsg(msg, true, "create deal", nil), nil, nil
}
}
```

```
// simulation/create_contract.gofunc SimulateMsgCreateContract(
ak types.AccountKeeper,
bk types.BankKeeper,
k keeper.Keeper,
) simtypes.Operation {
return func(r *rand.Rand, app *baseapp.BaseApp, ctx sdk.Context, accs []simtypes.Account, chainID string,
) (simtypes.OperationMsg, []simtypes.FutureOperation, error) {creatorAccount := accs[0]
consumerAccount := accs[2]
dealId := strconv.Itoa(r.Intn(30))
ownerETA := strconv.Itoa(r.Intn(501))
fees := r.Uint64()
expiry := strconv.Itoa(r.Int())msg := &types.MsgCreateContract{
Creator: creatorAccount.Address.String(),
DealId: dealId,
Consumer: consumerAccount.Address.String(),
Desc: "some random order desc",
OwnerETA: ownerETA,
Expiry: expiry,
Fees: fees,
}err := SendMsg(r, app, ak, bk, msg, ctx, chainID, DefaultGasValue, []cryptotypes.PrivKey{creatorAccount.PrivKey})if err != nil {
return simtypes.NoOpMsg(types.ModuleName, msg.Type(), "CreateContract"), nil, nil
}return simtypes.NewOperationMsg(msg, true, "create contract", nil), nil, nil
}
}
```

```
// simulation/commit_contract.gofunc SimulateMsgCommitContract(
ak types.AccountKeeper,
bk types.BankKeeper,
k keeper.Keeper,
) simtypes.Operation {
return func(r *rand.Rand, app *baseapp.BaseApp, ctx sdk.Context, accs []simtypes.Account, chainID string,
) (simtypes.OperationMsg, []simtypes.FutureOperation, error) {
simAccount := accs[1]
dealId := strconv.Itoa(r.Intn(20))
contractId := strconv.Itoa(r.Intn(5))
vendorETA := strconv.Itoa(r.Intn(101))msg := &types.MsgCommitContract{
Creator: simAccount.Address.String(),
DealId: dealId,
ContractId: contractId,
VendorETA: vendorETA,
}err := SendMsg(r, app, ak, bk, msg, ctx, chainID, DefaultGasValue, []cryptotypes.PrivKey{simAccount.PrivKey})if err != nil {
return simtypes.NoOpMsg(types.ModuleName, msg.Type(), "CommitContract"), nil, nil
}
return simtypes.NewOperationMsg(msg, true, "approve contract", nil), nil, nil
}
}
```

一旦为每个消息定义了模拟方法，我们就可以测试 200 个块的模拟-

```
starport chain simulate -v --numBlocks 200 --blockSize 50 --seed 33 --exportStatsPath ./stats.json --exportStatePath ./state.json
```

这将模拟块高度为 200 的链，并将调用每个模块的模拟。我们将获得所有不同模块模拟和自定义事务消息模拟的输出。它还将生成`stats.json`(每个测试用例的状态)和`state.json`(模拟后的区块链状态)文件。

交易模块模拟的测试结果-

```
"deal": {
"approve_contract": {
 "failure": 146
 },
"cancel_order": {
  "failure": 77
 },
"commit_contract": {
 "failure": 145,
 "ok": 26
 },
"create_contract": {
 "failure": 20,
 "ok": 303
 },
"create_deal": {
 "ok": 316
 },
"order_delivered": {
 "failure": 128
 },
"ship_order": {
 "failure": 134
 }
}
```

keepers、client CLI 和 genesis 的其他测试用例可以参考[源代码](https://github.com/Harry-027/deal)。

## 接下来是什么-

太棒了。你坚持到了最后。我们可以进一步改进我们的 dapp，使其更适合生产。其他有用的任务可以继续-

*   为在线商店开发前端，并将其与`deal` dapp 集成。通过 Keplr 钱包运行 txs。
*   为从区块链获取的查询详细信息创建仪表板。
*   通过 tendermint web-socket 在前端订阅自定义事件。
*   创建评级服务，方便消费者对订单交付服务进行评级。
*   优化数据结构，并从模块方法`EndBlock`本身的存储中删除过期合同。
*   使用 docker-compose 在具有 5 个不同节点的测试网络上部署 dapp，并在本地测试它。
*   使`ibc`能够与`bandchain` oracle 集成。从 oracle 获取价格信息，以规范不同类型订单的价格。

参考这里的源代码- [*源代码*](https://github.com/Harry-027/deal)

系列
*[*Part-1*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*Part-2*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
*[*Part-3*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*Part-4*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc) ***[*Part-5*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3)

## *有用的链接-*

*   *[*嫩薄荷*](https://docs.tendermint.com/)*
*   *[*Cosmos SDK*](https://docs.cosmos.network/)*
*   *[*星港*](https://docs.starport.network/)*
*   *[*IBC*](https://ibc.cosmos.network/)*
*   *[频段协议](https://docs.bandchain.org/)*

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[我的密码交易经验](/coinmonks/my-experience-with-crypto-copy-trading-d6feb2ce3ac5) | [比特币基地评论](/coinmonks/coinbase-review-6ef4e0f56064)*
*   *[CoinFLEX 评论](https://coincodecap.com/coinflex-review) | [AEX 交易所评论](https://coincodecap.com/aex-exchange-review) | [UPbit 评论](https://coincodecap.com/upbit-review)*
*   *[AscendEx 保证金交易](https://coincodecap.com/ascendex-margin-trading) | [Bitfinex 赌注](https://coincodecap.com/bitfinex-staking) | [bitFlyer 评论](https://coincodecap.com/bitflyer-review)*
*   *[麻雀交换评论](https://coincodecap.com/sparrow-exchange-review) | [纳什交换评论](https://coincodecap.com/nash-exchange-review)*
*   *[支持卡审核](https://coincodecap.com/uphold-card-review) | [信任钱包 vs 元掩码](https://coincodecap.com/trust-wallet-vs-metamask)*
*   *[Exness 点评](https://coincodecap.com/exness-review)|[moon xbt Vs bit get Vs Bingbon](https://coincodecap.com/bingbon-vs-bitget-vs-moonxbt)*