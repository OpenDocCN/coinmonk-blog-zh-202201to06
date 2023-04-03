# 使用 Cosmos SDK 第 5 部分构建特定于应用程序的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3?source=collection_archive---------7----------------------->

![](img/f19e3823d8d934d82e0773690e2b7474.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/data-migration?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在上一部分中，我们讨论了如何处理 msg 事务。希望您已经在本地测试了处理程序:)。在当前部分，我们将学习如何索引自定义事件&用户如何通过 tendermint rpc websocket 订阅它们。我们还将看到，如何在链升级期间处理状态迁移。

## 索引和订阅自定义事件:

Tendermint 允许我们索引事务和块，然后查询或订阅它们的结果。默认情况下，tendermint 使用 KV 存储器进行索引，默认情况下，`tx.height`、`tx.hash`始终被索引。让我们看看自定义事件索引的运行情况。

可以根据组合键对自定义事件进行索引。假设，我们在创建交易时发出一个自定义事件-

```
ctx.EventManager().EmitEvent(
 sdk.NewEvent(sdk.EventTypeMessage,
 sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
 sdk.NewAttribute(types.IDVALUE, dealId),
 sdk.NewAttribute(types.OWNER, newDeal.Owner),
 sdk.NewAttribute(types.VENDOR, newDeal.Vendor),
 ),
)
```

这里，上述自定义事件的组合键是-

*   message.module='deal '
*   message.action='create_deal '
*   message.idvalue={dealId}

等等…

让我们索引组合键`message.action=’create_deal’`

> 配置、genesis、私钥和存储文件一般存储在 home 目录下的一个隐藏文件夹中(`.appName`)。在我们的例子中，隐藏文件夹的名字是`.deal`，你可以在你的本地机器上找到相同的名字。在各种配置文件中，`*config.toml*`是包含与 tendermint 共识引擎相关的不同参数的文件，而`*app.toml*`包含特定于 app 的参数。json 包含每个模块的起源状态。

打开`config.toml`文件，在索引器=kv 下添加以下`tags`字段。

```
tags="message.action='create_deal'"
```

保存文件并重新启动链。在创建任何交易之前，让我们通过 web socket 订阅组合键`“message.action=’create_deal’”`。您可以使用任何 web socket cli 客户端或安装 one- `[https://github.com/oliver006/ws-client](https://github.com/oliver006/ws-client)`进行测试。

打开另一个终端并运行命令-

```
ws-client ws://localhost:26657/websocket
> { "jsonrpc": "2.0", "method": "subscribe", "params": ["message.action='create_deal'"], "id": 1 }
```

现在我们订阅了定制事件类型`create_deal`的`/subscribe` tendermint RPC 端点。让我们打开一个新的终端实例来发出 create deal tx -

```
deald tx deal create-deal cosmos19aurpre8j3zd5gkngupz830vz5ta8ye8deuyzh 50 --from owner
```

一旦执行完成，tendermint 将对事件进行索引，我们将通过 web-socket 获得响应。例如，我得到的回复如下:

```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "query": "message.action='create_deal'",
    "data": {
      "type": "tendermint/event/Tx",
      "value": {
        "TxResult": {
          "height": "38235",
          "tx": "CogBCoUBCiEvSGFycnkwMjcuZGVhbC5kZWFsLk1zZ0NyZWF0ZURlYWwSYAotY29zbW9zMXh5cG4zZWw4bW1wOHA4Y3YyanR2ZXE1ODdwaHZ5eHl6OThsaHNnEi1jb3Ntb3MxOWF1cnByZThqM3pkNWdrbmd1cHo4MzB2ejV0YTh5ZThkZXV5emgYMhJYClAKRgofL2Nvc21vcy5jcnlwdG8uc2VjcDI1NmsxLlB1YktleRIjCiEDKxIThp2LiM3qZnARSu1Ve1E+mRsEks2ebAJYI+AvgskSBAoCCAEYEBIEEMCaDBpAdbvWanujmmFUVf8Nm0IM8V/8q5nxqykEHINi20tzRP8rd+x0SAu04yjW93LOldF1zvAqxISDL/fA9ytE+didFA==",
          "result": {
            "data": "CigKIS9IYXJyeTAyNy5kZWFsLmRlYWwuTXNnQ3JlYXRlRGVhbBIDCgE3",
            "log": "[{\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"create_deal\"},{\"key\":\"module\",\"value\":\"deal\"},{\"key\":\"IdValue\",\"value\":\"7\"},{\"key\":\"Owner\",\"value\":\"cosmos1xypn3el8mmp8p8cv2jtveq587phvyxyz98lhsg\"},{\"key\":\"Vendor\",\"value\":\"cosmos19aurpre8j3zd5gkngupz830vz5ta8ye8deuyzh\"}]}]}]",
            "gas_wanted": "200000",
            "gas_used": "48707",
            "events": [
              {
                "type": "tx",
                "attributes": [
                  {
                    "key": "ZmVl",
                    "value": "",
                    "index": true
                  }
                ]
              },
              {
                "type": "tx",
                "attributes": [
                  {
                    "key": "YWNjX3NlcQ==",
                    "value": "Y29zbW9zMXh5cG4zZWw4bW1wOHA4Y3YyanR2ZXE1ODdwaHZ5eHl6OThsaHNnLzE2",
                    "index": true
                  }
                ]
              },
              {
                "type": "tx",
                "attributes": [
                  {
                    "key": "c2lnbmF0dXJl",
                    "value": "ZGJ2V2FudWptbUZVVmY4Tm0wSU04Vi84cTVueHF5a0VISU5pMjB0elJQOHJkK3gwU0F1MDR5alc5M0xPbGRGMXp2QXF4SVNETC9mQTl5dEUrZGlkRkE9PQ==",
                    "index": true
                  }
                ]
              },
              {
                "type": "message",
                "attributes": [
                  {
                    "key": "YWN0aW9u",
                    "value": "Y3JlYXRlX2RlYWw=",
                    "index": true
                  }
                ]
              },
              {
                "type": "message",
                "attributes": [
                  {
                    "key": "bW9kdWxl",
                    "value": "ZGVhbA==",
                    "index": true
                  },
                  {
                    "key": "SWRWYWx1ZQ==",
                    "value": "Nw==",
                    "index": true
                  },
                  {
                    "key": "T3duZXI=",
                    "value": "Y29zbW9zMXh5cG4zZWw4bW1wOHA4Y3YyanR2ZXE1ODdwaHZ5eHl6OThsaHNn",
                    "index": true
                  },
                  {
                    "key": "VmVuZG9y",
                    "value": "Y29zbW9zMTlhdXJwcmU4ajN6ZDVna25ndXB6ODMwdno1dGE4eWU4ZGV1eXpo",
                    "index": true
                  }
                ]
              }
            ]
          }
        }
      }
    },
    "events": {
      "message.Owner": [
        "cosmos1xypn3el8mmp8p8cv2jtveq587phvyxyz98lhsg"
      ],
      "tx.hash": [
        "84264CAE7C5A99A495BDA5DECD2CC40562EFC524BF2CF6128522C1362D8254A9"
      ],
      "tx.acc_seq": [
        "cosmos1xypn3el8mmp8p8cv2jtveq587phvyxyz98lhsg/16"
      ],
      "tx.signature": [
        "dbvWanujmmFUVf8Nm0IM8V/8q5nxqykEHINi20tzRP8rd+x0SAu04yjW93LOldF1zvAqxISDL/fA9ytE+didFA=="
      ],
      "message.IdValue": [
        "7"
      ],
      "message.Vendor": [
        "cosmos19aurpre8j3zd5gkngupz830vz5ta8ye8deuyzh"
      ],
      "tm.event": [
        "Tx"
      ],
      "tx.height": [
        "38235"
      ],
      "tx.fee": [
        ""
      ],
      "message.action": [
        "create_deal"
      ],
      "message.module": [
        "deal"
      ]
    }
  }
}
```

您还可以使用 config.toml-中的`tags`字段索引多个事件

```
tags="message.action='create_deal',message.action='create_contract'"
```

请注意，tendermint 将实现`psql`索引器& `kv`将来将被弃用，因为查询语法仅限于`kv`索引器类型，而`psql`索引器将能够将事件代理到外部配置的 Postgresql 实例。这将利用 SQL 来执行一系列丰富而复杂的查询，这些查询不受`kv`索引器类型的支持。很高兴很快看到更多有趣的功能:)

## 通过就地商店迁移处理连锁升级:

假设我们的产品链已经投入使用，我们希望对其进行升级。例如，为了增加新的特性，我们可能需要改变状态结构。或者让我们考虑一个简单的任务，从商店中删除过期的合同。我们确实有一个**升级链指南**，作为 cosmos sdk 文档的一部分-*[*doc*](https://docs.cosmos.network/v0.44/building-modules/upgrade.html)。对于我们的迁移示例，我们将引用相同的内容。*

*让我们在 keeper 包中创建一个 migrator 具体类型。*

```
*//migrator.go
package keepertype Migrator struct {
 keeper Keeper
}*// NewMigrator returns a new Migrator.*func NewMigrator(keeper Keeper) Migrator {
 return Migrator{keeper: keeper}
}*
```

*迁移器环绕保持器，这对迁移脚本中的状态转换很有用。我们将按照指南中的建议，把我们的迁移脚本放在`v01`包下的遗留文件夹中。*

```
*//v01.go
package v01import (
 "fmt"
 "github.com/Harry-027/deal/x/deal/types"
 "github.com/cosmos/cosmos-sdk/codec"
 "github.com/cosmos/cosmos-sdk/store/prefix"
 sdk "github.com/cosmos/cosmos-sdk/types"
)func MigrateDealStore(ctx sdk.Context, storeKey sdk.StoreKey, cdc codec.BinaryCodec) error {
 store := ctx.KVStore(storeKey)
  return pruneOldContracts(store, cdc)
}func pruneOldContracts(store sdk.KVStore, cdc codec.BinaryCodec) error {
  dealStore := prefix.NewStore(store, []byte(types.NewDealKeyPrefix))
  dealStoreIter := dealStore.Iterator(nil, nil) defer dealStoreIter.Close()

  var deals []types.NewDeal
  for ; dealStoreIter.Valid(); dealStoreIter.Next() {
   var val types.NewDeal
   cdc.MustUnmarshal(dealStoreIter.Value(), &val)
   deals = append(deals, val)
  }for _, deal := range deals {
  contractStorePrefixKey := fmt.Sprintf("%s%s/",    types.NewContractKeyPrefix, deal.DealId)
  contractStore := prefix.NewStore(store,  []byte(contractStorePrefixKey))
  iterator := sdk.KVStorePrefixIterator(contractStore, []byte{})
  defer iterator.Close()for ; iterator.Valid(); iterator.Next() {
  var val types.NewContract
  cdc.MustUnmarshal(iterator.Value(), &val)
  if val.Status == "DELIVERED" {
   contractKey := fmt.Sprintf("%s%s/", types.NewContractKeyPrefix,    val.ContractId)
   contractStore.Delete([]byte(contractKey))
 }
}
}
 return nil
}*
```

*我们对每笔交易的合同进行迭代，以识别和删除过期的合同。我们将通过迁移对象上的方法调用此脚本-*

```
*// migrations.gopackage keeperimport (
v01 "github.com/Harry-027/deal/x/deal/legacy/v01"
sdk "github.com/cosmos/cosmos-sdk/types"
)*// Migrate2to3 - Migrating deal module from version 2 to 3*func (m Migrator) Migrate2to3(ctx sdk.Context) error {
 return v01.MigrateDealStore(ctx, m.keeper.storeKey, m.keeper.cdc) *// v01 is package `x/deal/legacy/v01`.* }*
```

*我们现在将通过`registerMigration`方法为一致版本`3`注册配置器下的`Migrate2to3`方法。注:可通过模块方法- `RegisterServices`访问配置器*

```
*// module.gofunc (am AppModule) RegisterServices(cfg module.Configurator) {
types.RegisterQueryServer(cfg.QueryServer(), am.keeper)
 m := keeper.NewMigrator(am.keeper)
 if err := cfg.RegisterMigration(types.ModuleName, 3, m.Migrate2to3); err != nil {
   panic(fmt.Sprintf("failed to migrate x/deal from version 2 to 3:
%v", err))
 }
}*
```

*用户可以在 configurator 上注册多个迁移。*

*x/upgrade 模块跟踪`VersionMap`存储中的所有模块共识版本。为了在升级期间触发迁移，我们还需要更新模块的一致版本。让我们把它从 2 改成 3-*

```
**// ConsensusVersion implements ConsensusVersion.*func (AppModule) ConsensusVersion() uint64 { return 3 }*
```

*在从模块共识版本 2 的链升级期间，将触发在版本 3 的配置器上注册的任意数量的迁移。*

*连锁升级通常通过对提案进行投票来实现。提案通常由利益相关方通过对应于`gov`模块的 tx 提交。一旦验证人和授权人参与并投票支持提交的提案，投票期结束后，升级将通过升级管理员处理程序在某个区块高度进行。因此，我们需要设置升级处理程序来执行迁移。*

```
*// app.goapp.UpgradeKeeper.SetUpgradeHandler("migrateOldContracts", func(ctx sdk.Context, plan upgradetypes.Plan, fromVM module.VersionMap) (module.VersionMap, error) {
*// Register the consensus version in the version map* fromVM["deal"] = dealmodule.AppModule{}.ConsensusVersion()
 return app.mm.RunMigrations(ctx, cfg, fromVM)
})*
```

*`upgradeHandler`将调用模块管理器上的`RunMigrations`方法，该方法将在内部调用我们的模块迁移脚本。`RunMigrations`也将返回新的一致版本，该版本将保存在`x/upgrade`模块的`VersionMap`商店中。从而确认模块的稳定升级和最新一致版本。*

*可以将提案提交到治理模块-*

```
*deald tx gov submit-proposal software-upgrade migrateOldContracts --title migrateOldContracts --description migrateOldContracts --upgrade-height 100 --from validator --yes*
```

*并投票支持它*

```
*deald tx gov deposit 1 10000000stake --from validator --yes
deald tx gov vote 1 yes --from validator --yes*
```

*升级将在块高度为 100 时自动进行。*

*作为本地开发的一部分，可能需要在本地测试迁移脚本，而不需要通过提议的方式。为了实现这一点，其中一个方法是调用模块`EndBlock`方法中的迁移脚本(由于`EndBlock`在每个块之后自动执行，我们将能够在本地测试我们的迁移脚本，但是这种方法不适合大量的迁移数据)*

```
*//module.gofunc (am AppModule) EndBlock(ctx sdk.Context, _ abci.RequestEndBlock) []abci.ValidatorUpdate {
*// for testing if migration scripts run properly
   m := keeper.NewMigrator(am.keeper)
   m.Migrate2to3(ctx)* return []abci.ValidatorUpdate{}}*
```

*今天的学习足够了:)将在下一部分介绍区块链测试模拟。*

*参考这里的源代码- [*源代码*](https://github.com/Harry-027/deal)*

*系列
*[*Part-1*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*Part-2*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
*[*Part-3*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*Part-4*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc)
*[*Part-5*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3)*

> **加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资**

# **另外，阅读**

*   **[加密货币储蓄账户](/coinmonks/cryptocurrency-savings-accounts-be3bc0feffbf) | [加密交易机器人](https://coincodecap.com/best-crypto-trading-bots)**
*   **[BigONE 交易所评论](/coinmonks/bigone-exchange-review-64705d85a1d4) | [CEX。IO 审查](https://coincodecap.com/cex-io-review) | [交换区审查](/coinmonks/swapzone-review-crypto-exchange-data-aggregator-e0ad78e55ed7)**
*   **[最佳比特币保证金交易](/coinmonks/bitcoin-margin-trading-exchange-bcbfcbf7b8e3) | [比特币保证金交易](https://coincodecap.com/bityard-margin-trading)**
*   **[加密保证金交易交易所](/coinmonks/crypto-margin-trading-exchanges-428b1f7ad108) | [赚取比特币](/coinmonks/earn-bitcoin-6e8bd3c592d9)**
*   **[WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)**