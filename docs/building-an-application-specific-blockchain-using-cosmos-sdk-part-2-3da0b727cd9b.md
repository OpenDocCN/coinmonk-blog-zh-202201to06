# 使用 Cosmos SDK Part-2 构建特定于应用程序的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b?source=collection_archive---------3----------------------->

在第 1 部分中，我们实现了我们的用例，并决定了应用特定的区块链路线，以实现我们的目标。现在我们将开始深入应用程序的技术方面。

![](img/0b852d903a0cad918cdf627247ad4307.png)

Photo by [Nick Morrison](https://unsplash.com/@nickmorrison?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technical-design?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

要开始使用 cosmos sdk 构建区块链，您应该非常熟悉围绕[](https://docs.tendermint.com/v0.35/tutorials/go-built-in.html)**和[**Cosmos SDK**](https://docs.cosmos.network/v0.44/core/)**架构的基本概念。我强烈建议浏览给定的链接(*文档*)以获得更好的理解。另外，了解一下 starbort[](https://docs.starport.com/)**也很有帮助，因为我们将使用 Starport cli 作为构建链的开发工具。******

******在我们继续开发之前，我希望您已经阅读了关于 Cosmos SDK 设计的文档。基本上，它为我们提供了 ABCI 接口的样板实现，帮助我们与 Tendermint 共识引擎进行交互。请注意，我们将使用 golang 编写我们的应用程序。由于 Tendermint 是用 golang 编写的，我们的应用程序可以很容易地编译成 Tendermint 二进制文件，否则我们将需要一个 unix 套接字连接来与 Tendermint 进程通信。******

******在我们开始开发之前，让我们总结一下 cosmos SDK 设计的要点******

*   ******Tendermint 通过 ABCI ( *应用区块链接口*)与应用进行通信。因此，从我们的应用服务器到外部互联网应该没有其他开放端口。所有交互都应通过 tendermint 核心引擎进行。不通过 Tendermint 发生的任何状态转换都是安全漏洞。******
*   ******以下是 ABCI 的重要方法，一个 app 必须实现-
    * **CheckTx-** 当 Tendermint 接收到一个事务时，在将它添加到 mempool 之前，通过`CheckTx`将其传递给应用程序以验证它是否有效。这是为了保护内存池免受垃圾事务的影响。应该调用名为`AnteHandler`的处理程序来执行验证步骤，比如检查是否有足够的费用和签名验证。注意，这并不保证无效的 Tx 不会到达内存池。因此，在交易处理步骤(`DeliverTX`)期间，应用程序应该重新验证消息，并强制执行一定的气体消耗，以阻止垃圾交易。
    * **DeliverTx-** 状态转换发生在此阶段。给定块中的每个事务都通过`DeliverTx`传递给应用程序，以便进行处理。Cosmos sdk 负责解码事务并将 rpc 消息路由到相应的模块。
    ***begin block/end block**:这些方法在每个块的开头和结尾执行。触发自动逻辑执行是有用的。注意，这里必须避免昂贵的操作。******
*   ****使用 Cosmos SDK 的最大好处是我们不必实现 ABCI 接口。Cosmos SDK 以 [baseapp](https://docs.cosmos.network/v0.44/intro/sdk-design.html#baseapp) 的形式提供了样板实现。作为应用程序开发人员，我们应该通过将 baseapp 嵌入到我们的自定义应用程序中来扩展它。****
*   ****一个 ABCI 应用基本上是一个对象，由 baseapp ( *来自 sdk* )、存储键列表(访问模块存储的键)、模块保持器列表(为自己的模块存储处理读写的对象)、appCodec(序列化和反序列化数据结构，以便将数据存储为模块存储中的`[]byte`)组成。****
*   ****一个 app 由各种内置和自定义模块组成。每个模块都有自己的`KVStore`。模块间的交互通过能力原则发生。这确保了跨模块的安全性。一个模块可以定义一组预定义的功能，其他模块可以通过导入它们的`keeper`接口来使用这些功能。例如，我们的自定义模块的`keeper`结构需要嵌入银行模块的`keeper`接口，以处理与资金转移相关的功能。****
*   ****moduleManager 是 sdk 中的一个重要实体。它基本上是一个包含所有应用程序模块列表的对象。它决定了`InitChain`、`BeginBlocker`和`EndBlocker`等各种功能模块之间的执行顺序。它负责注册每个模块的`Msgservice`和`grpc query`服务。它还有助于初始化和导出所有模块的 genesis。****
*   ****作为应用程序开发人员，我们将主要关注定制模块的`Msg`、`Query`服务和`Genesis`状态。****
*   ****我们将在所有脚手架操作中使用 Starport cli。使用 starport 是开始使用 cosmos sdk 最简单的方法。它帮助我们搭建代码、生成类型定义、原型定义、下载依赖项、将代码编译成二进制、测试模拟等。****

****不再拖延，让我们安装 starport cli！****

****安装 starport 之前，请确保 Golang 已正确安装在您的机器上。****

******星港安装-******

****在您的终端中执行以下命令-****

****`curl [https://get.starport.com/starport](https://get.starport.com/starport)! | bash`****

****这将在`/usr/local/bin`目录下安装 starport 二进制文件。要验证 cli 是否安装正确，请运行命令`starport --version`。如果它抛出一个错误而不是打印版本，可能是安装有问题。如果错误显示- `command not found`，那么很可能终端无法找到 starport 二进制文件，因为机器上的路径设置不正确。****

****注意，我们在本教程中使用的是 starport 版本(`v0.19.5`)。一旦安装了 starport，运行命令来搭建链****

****`starport scaffold chain github.com/harry-027/deal`****

****这将使用名称`deal`搭建链。随意更改用户名`harry-027`。理想情况下，这应该是您将在其中部署源代码的 github 帐户用户名。注意，该命令还会生成一个自定义模块，其名称`deal`与链的名称相同。如果您现在不想生成定制模块，那么运行上面带有标志`--no-module`的命令。你可以稍后通过命令`starport scaffold module [name] [flags]`生成模块。如果需要，后一选项还提供了通过标志启用`ibc`的灵活性。****

****现在让我们将根目录更改为`deal`文件夹，并运行命令`starport chain serve`。这将在开发模式下启动我们的单节点集群区块链。我们现在将专注于开发我们自己的定制模块`deal`，并将其与应用程序集成。****

****在我们开始为我们的定制`deal`模块编写功能代码之前，让我们了解一下业务流程****

## ****概念-****

****![](img/76b5a076913c7e7f4a41d82b15a78c61.png)****

****Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/blockchain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)****

## ****用例-****

****通常，大型在线电子商务商店与供应商合作，在给定的期限内为消费者完成订单交付。在线商店所有者负责处理在线商店和订单交付，而供应商负责准备和运送产品(将其交给商店所有者以交付给最终用户)。这里的目标是处理区块链的交易和订单的资金，以便按照最初的协议在各方之间分配公平的佣金。****

## ****成交-****

****在这里，交易基本上是两个业务方围绕订单完成的佣金率达成的协议。在我们的用例中，基本上一个商店老板与供应商达成一个特定的固定佣金率(`1% <= r% <= 100%`)的交易，该佣金率将在每次订单交付后适用。这意味着在给定的期限内成功交付给定的交易后，固定金额的佣金将被转移到卖方账户。****

```
**// proto definition
message NewDeal {
  string dealId = 1;
  string owner = 2;
  string vendor = 3;
  uint64 commission = 4;
}**
```

## ****合同-****

****这里，来自终端用户的每个订单都由一个合同表示。基于在线购物车和用户细节，在线商店所有者在交易下在区块链上发起合同，该合同包括某些细节，诸如最终用户钱包地址、合同描述下的订单细节、开始时间、所有者交付所用的时间以及合同到期时间。为了成功执行合同，供应商需要在合同到期前提交合同。请注意，供应商需要输入提交合同的运输时间。只有当运输时间少于交付时间的一半时，合同才能标记为已提交。****

```
**// proto definition
message NewContract {
  string dealId = 1;
  string contractId = 2;
  string consumer = 3;
  string desc = 4;
  uint32 ownerETA = 5;
  uint32 vendorETA = 6;
  string status = 7;
  uint64 fees = 8;
  string expiry = 9;
  uint32 shippingDelay = 10;
  string startTime = 11;
  uint32 deliveryDelay = 12;
}**
```

## ****合同审批-****

****一旦供应商签订了合同，最终用户就应该付款，以便订单能够按时处理。最终用户的付款基本上保存在托管账户中，该账户基本上是交易模块账户。最终用户成功付款后，合同被标记为已批准，这也会触发一个自定义事件，通知供应商合同已批准。请注意，最终用户需要在到期时间之前批准合同，以便订单处理可以开始。****

## ****合同运输-****

****一旦合同获得批准，供应商就可以开始处理订单，并为消费者做好准备。将产品移交给店主时，供应商可以启动 tx，将合同状态更改为`IN-DELIVERY`。这标志着此处的供应商角色已完成。使用此 tx，还会记录与承诺运输时间相关的运输延迟(如果有)。****

## ****订单已交付-****

****一旦订单到达最终用户入口步骤，他需要启动一个 tx，将订单标记为完成。该 tx 将计算是否有任何交付延迟，并根据计算的延迟费用(运输/交付)和佣金率从托管账户向各方发放资金。请注意，在运输或交付延迟的情况下，消费者将获得与延迟成比例的退款(延迟费用)。延迟费用将从双方佣金中扣除(如果运输延迟，从卖方佣金中扣除；如果交货延迟，从店主佣金中扣除)。****

## ****订单已取消-****

****如果交货时间延迟超过或等于 20 分钟，消费者可以将订单标记为取消。请注意，如果订单取消成功，用户将获得全额退款(资金从托管账户转移回用户账户)****

****暂时这样就够了:)。在下一节中，我们将为自定义的`deal`模块处理数据类型和查询处理程序。****

****参考这里的源代码- [*源代码*](https://github.com/Harry-027/deal)****

****系列
*[*Part-1*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*Part-2*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
*[*Part-3*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*Part-4*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc) ***[*Part-5*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3) *******

> *****加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*****

# ****另外，阅读****

*   ****[3 commas Review](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92)|[Pionex Review](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot)|[coin rule Review](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)****
*   ****[莱杰 vs Ngrave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)****
*   ****[by bit Exchange Review](/coinmonks/bybit-exchange-review-dbd570019b71)|[bit yard Review](https://coincodecap.com/bityard-reivew)|[Jet-Bot Review](https://coincodecap.com/jet-bot-review)****
*   ****[3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)****
*   ****最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)****