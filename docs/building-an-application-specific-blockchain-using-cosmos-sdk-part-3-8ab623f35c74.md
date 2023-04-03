# 使用 Cosmos SDK 第 3 部分构建特定于应用程序的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74?source=collection_archive---------4----------------------->

![](img/6384c98e8e2d54f523a65ba23cd15b98.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

到目前为止，在第 2 部分中，我们讨论了有关 Tendermint、Cosmos sdk 的技术细节，并安装了 starport 来搭建和运行链。我们还浏览了定制模块`deal`的业务流程。现在我们将首先从定义我们的数据类型开始。我们将使用 starport 来生成类型。注意，starport 将自动生成查询和消息处理程序以及类型。使用标志`--no-message`，这样 starport 就不会为我们的数据类型创建`sdk.Msg`和 msg 服务。如果给定类型不需要查询处理程序，可以随意删除。

让我们从一个`dealCounter`类型开始，它将负责在创建新交易时生成交易 id。

```
starport scaffold single dealCounter idValue:uint --module deal --no-message
```

`--no-message`标志帮助我们在没有`sdk.Msg`类型和消息处理程序的情况下生成类型。我们将使用`dealCounter`类型下的`idValue`字段作为增量计数器，在创建交易时生成交易 id。上面的`scaffold`命令执行以下操作-

*   为`dealCounter` ( `deal_counter.proto`)生成原型类型定义。
*   更新`genesis.proto`文件，使其包含起源状态下的`dealCounter`。
*   生成查询消息定义(`query.proto`)。
*   查询消息处理程序(在`keepers`目录下)。
*   query proto 和 query proto grpc 网关文件(`query.pb.go, query.pb.gw.go`)。
*   生成 cli 命令来调用查询处理程序(`query_new_deal.go`)。
*   测试文件和测试模拟参数(*用于模拟测试*)。

```
// deal_counter.protosyntax = "proto3";
package Harry027.deal.deal;option go_package = "github.com/Harry-027/deal/x/deal/types";message DealCounter {
uint64 idValue = 1;
}
```

```
// genesis.proto
option go_package = "github.com/Harry-027/deal/x/deal/types";*// GenesisState defines the deal module's genesis state.*message GenesisState {
Params params = 1 [(gogoproto.nullable) = false];
DealCounter dealCounter = 2;
}
```

注意，我们不要求用户查询计数器细节。因此我们应该从`query.proto`文件中删除与`dealCounter`相关的查询消息。同时删除`keepers`文件夹中搭建的`dealCounter`查询处理程序文件和`cli`文件夹中的`dealCounter`特定 cli 命令。并运行以下命令来重新生成原型定义(`*.pb.go`和`*.pb.gw.go`)。

```
starport generate proto-go
```

注意，我们不应该接触`*.pb.go`和`*.pb.gw.go`生成的文件，因为这些文件每次都会基于原型定义自动生成。此外，您会发现命令(在不同的文件中)类似于下面给出的命令

`*// this line is used by starport scaffolding # genesis/proto/state*`

不要删除此类命令，因为 starport 每次都会使用这些命令来确定代码生成的正确位置。

让我们生成 newDeal 映射类型-

```
starport scaffold map newDeal dealId owner vendor commission:uint --module deal --no-message
```

该命令执行以下操作-

*   为`newDeal` ( `new_deal.proto`)生成原型定义。
*   更新`genesis.proto`文件。
*   生成查询消息(`query.proto`)。
*   查询消息处理程序。(`grpc_query_new_deal.go`)。
*   query proto 和 query proto grpc 网关文件。(`query.pb.go, query.pb.gw.go`)。
*   生成 cli 命令来调用查询处理程序(`query_new_deal.go`)。
*   Keeper 方法来序列化/反序列化存储区上的数据和 crud 操作。(`new_deal.go`)。
*   测试文件和测试模拟参数。

```
// new_deal.protosyntax = "proto3";
package Harry027.deal.deal;
option go_package = "github.com/Harry-027/deal/x/deal/types";message NewDeal {
string dealId = 1;
string owner = 2;
string vendor = 3;
uint64 commission = 4;
}
```

```
// query.protomessage QueryGetNewDealRequest {
string index = 1;
}message QueryGetNewDealResponse {
NewDeal newDeal = 1 [(gogoproto.nullable) = false];
}message QueryAllNewDealRequest {
cosmos.base.query.v1beta1.PageRequest pagination = 1;
}message QueryAllNewDealResponse {
repeated NewDeal newDeal = 1 [(gogoproto.nullable) = false];
cosmos.base.query.v1beta1.PageResponse pagination = 2;
}
```

```
// new_deal.gopackage keeperimport (
"github.com/Harry-027/deal/x/deal/types"
"github.com/cosmos/cosmos-sdk/store/prefix"
sdk "github.com/cosmos/cosmos-sdk/types"
)*// SetNewDeal sets a specific newDeal in the store from its index* func (k Keeper) SetNewDeal(ctx sdk.Context, newDeal types.NewDeal) {store := prefix.NewStore(ctx.KVStore(k.storeKey), types.KeyPrefix(types.NewDealKeyPrefix))
b := k.cdc.MustMarshal(&newDeal)
store.Set(types.NewDealKey(
newDeal.DealId,
), b)
}*// GetNewDeal returns a newDeal from its index*func (k Keeper) GetNewDeal(
ctx sdk.Context,
index string,
) (val types.NewDeal, found bool) {store := prefix.NewStore(ctx.KVStore(k.storeKey), types.KeyPrefix(types.NewDealKeyPrefix))
b := store.Get(types.NewDealKey(
index,
))if b == nil {
return val, false
}
k.cdc.MustUnmarshal(b, &val)
return val, true
}*// RemoveNewDeal removes a newDeal from the store* func (k Keeper) RemoveNewDeal(
ctx sdk.Context,
index string,
) {store := prefix.NewStore(ctx.KVStore(k.storeKey), types.KeyPrefix(types.NewDealKeyPrefix))
store.Delete(types.NewDealKey(
index,
))
}*// GetAllNewDeal returns all newDeal*func (k Keeper) GetAllNewDeal(ctx sdk.Context) (list []types.NewDeal) { store := prefix.NewStore(ctx.KVStore(k.storeKey),  types.KeyPrefix(types.NewDealKeyPrefix))
 iterator := sdk.KVStorePrefixIterator(store, []byte{}) defer iterator.Close() for ; iterator.Valid(); iterator.Next() {
  var val types.NewDeal
  k.cdc.MustUnmarshal(iterator.Value(), &val)
  list = append(list, val)
 }
return
}
```

交易的获取、设置和删除操作已在 keeper 对象上定义(如上所示)。注意，我们使用前缀存储来存储带有前缀关键字`NewDeal/value/` ( `key_new_deal.go`)的交易。

让我们修改`grpc_query_new_deal.go`文件来处理交易查询。

`NewDeal`将根据给定的 dealId( `req.Index`)获取交易详情。我们将根据 dealId 保存交易对象。因此，根据给定的`req.index`获取交易，在我们的例子中是`dealId`。

```
*// NewDeal is the query handler to fetch the deal details for a given dealId*func (k Keeper) NewDeal(c context.Context, req *types.QueryGetNewDealRequest) (*types.QueryGetNewDealResponse, error) {
if req == nil {
return nil, status.Error(codes.InvalidArgument, "invalid request")
}ctx := sdk.UnwrapSDKContext(c)
val, found := k.GetNewDeal(
  ctx,
  req.Index,
)if !found {
return nil, status.Error(codes.InvalidArgument, "not found")
}
return &types.QueryGetNewDealResponse{NewDeal: val}, nil
}
```

`NewDealAll`将遍历 keyStore，从 Store 中获取所有保存的交易。它还包括分页功能，可以对响应进行分页。

```
*// NewDealAll is the query handler to fetch all the new deals*func (k Keeper) NewDealAll(c context.Context, req *types.QueryAllNewDealRequest) (*types.QueryAllNewDealResponse, error) {if req == nil {
  return nil, status.Error(codes.InvalidArgument, "invalid request")
}var newDeals []types.NewDeal
ctx := sdk.UnwrapSDKContext(c)
store := ctx.KVStore(k.storeKey)newDealStore := prefix.NewStore(store, types.KeyPrefix(types.NewDealKeyPrefix))pageRes, err := query.Paginate(newDealStore, req.Pagination,  func(key []byte, value []byte) error {
 var newDeal types.NewDeal
 if err := k.cdc.Unmarshal(value, &newDeal); err != nil {
  return err
 }
 newDeals = append(newDeals, newDeal)
 return nil
})if err != nil {
  return nil, status.Error(codes.Internal, err.Error())
}return &types.QueryAllNewDealResponse{NewDeal: newDeals,    Pagination: pageRes}, nil
}
```

现在类似于`dealCounter`和`newDeal`类型，让我们借助 starport scaffold 命令生成`contractCounter`和`newContract`类型。我们的 contractCounter 和 newContract proto 定义应该如下所示

```
// contract_counter.protomessage ContractCounter {
string dealId = 1; // id of the deal to which contract belongs to
uint64 idValue = 2; // counter to generate the contract id
}
```

```
// new_contract.protomessage NewContract {
string dealId = 1; // Id of the deal to which contract belongs to
string contractId = 2; // contractId
string consumer = 3; // consumer address
string desc = 4; // order description
uint32 ownerETA = 5; // estimated time of order delivery in mins
uint32 vendorETA = 6; // estimated time of order shipping in mins
string status = 7; // contract current status
uint64 fees = 8; // order payment figure
string expiry = 9; //expiry time before which it should get approved 
uint32 shippingDelay = 10; // shipping delay in mins 
string startTime = 11; // start time of order
uint32 deliveryDelay = 12; // // delivery delay in mins
}
```

我们将在这里使用带有前缀关键字`NewContract/value/{dealId}/`的前缀存储来存储合同。请注意，`dealId`这里是启动合同的交易 id。

让我们修改`new_contract.go`(处理契约的 getter、setter)和`grpc_query_new_contract.go`(查询处理器)，如下所示

```
// new_contract.go

package keeperimport (
"github.com/Harry-027/deal/x/deal/types"
"github.com/cosmos/cosmos-sdk/store/prefix"
sdk "github.com/cosmos/cosmos-sdk/types"
)*// SetNewContract set a specific newContract in the store -"NewContract/value/{dealId}"*func (k Keeper) SetNewContract(ctx sdk.Context, newContract types.NewContract) {key := types.NewContractKey(newContract.DealId)
store := prefix.NewStore(ctx.KVStore(k.storeKey), key)
b := k.cdc.MustMarshal(&newContract)store.Set(types.NewContractKey(
newContract.ContractId,
), b)
}*// GetNewContract returns a newContract from its index*func (k Keeper) GetNewContract(
ctx sdk.Context,
dealId string,
contractId string,
) (val types.NewContract, found bool) {
  storeKey := types.NewContractKey(dealId)
  store := prefix.NewStore(ctx.KVStore(k.storeKey), storeKey)
  b := store.Get(types.NewContractKey(
  contractId,
 ))if b == nil {
 return val, false
}k.cdc.MustUnmarshal(b, &val)
  return val, true
}*// RemoveNewContract removes a newContract from the store* func (k Keeper) RemoveNewContract(
ctx sdk.Context,
dealId string,
contractId string,
) {
  storeKey := types.NewContractKey(dealId)
  store := prefix.NewStore(ctx.KVStore(k.storeKey), storeKey)
  store.Delete(types.NewContractKey(
  contractId,
))
}*// GetAllNewContract returns all newContract*func (k Keeper) GetAllNewContract(ctx sdk.Context, dealId string) (list []types.NewContract) { storeKey := types.NewContractKey(dealId)
  store := prefix.NewStore(ctx.KVStore(k.storeKey), storeKey)
  iterator := sdk.KVStorePrefixIterator(store, []byte{}) defer iterator.Close()for ; iterator.Valid(); iterator.Next() {
  var val types.NewContract
  k.cdc.MustUnmarshal(iterator.Value(), &val)
  list = append(list, val)
}
  return
}
```

```
// grpc_query_new_contract.gopackage keeperimport (
"context"
"github.com/Harry-027/deal/x/deal/types"
"github.com/cosmos/cosmos-sdk/store/prefix"
sdk "github.com/cosmos/cosmos-sdk/types"
"github.com/cosmos/cosmos-sdk/types/query"
"google.golang.org/grpc/codes"
"google.golang.org/grpc/status"
)*// NewContractAll is the query handler to fetch all the contracts under given dealId*func (k Keeper) NewContractAll(c context.Context, req *types.QueryAllNewContractRequest) (*types.QueryAllNewContractResponse, error) {
 if req == nil {
  return nil, status.Error(codes.InvalidArgument, "invalid request")
 } var newContracts []types.NewContract
 ctx := sdk.UnwrapSDKContext(c) prefixStoreKey := types.NewContractKey(req.DealId)
 store := ctx.KVStore(k.storeKey)
 newContractStore := prefix.NewStore(store, prefixStoreKey) pageRes, err := query.Paginate(newContractStore, req.Pagination,  func(key []byte, value []byte) error {
 var newContract types.NewContract
 if err := k.cdc.Unmarshal(value, &newContract); err != nil {
 return err
}
 newContracts = append(newContracts, newContract)
 return nil
})if err != nil {
 return nil, status.Error(codes.Internal, err.Error())
} return &types.QueryAllNewContractResponse{NewContract: newContracts, Pagination: pageRes}, nil
}*// NewContract is the query handler to fetch the contract for a given specific dealId and contractId*func (k Keeper) NewContract(c context.Context, req *types.QueryGetNewContractRequest) (*types.QueryGetNewContractResponse, error) {
 if req == nil {
  return nil, status.Error(codes.InvalidArgument, "invalid request")
 }
  ctx := sdk.UnwrapSDKContext(c)
  val, found := k.GetNewContract( ctx,
  req.DealId,
  req.ContractId,
)if !found {
  return nil, status.Error(codes.InvalidArgument, "not found")
} return &types.QueryGetNewContractResponse{NewContract: val}, nil
}
```

让我们在模块- ( `module.go`)上注册查询服务器

```
*// RegisterGRPCGatewayRoutes registers the gRPC Gateway routes for the module.*func (AppModuleBasic) RegisterGRPCGatewayRoutes(clientCtx client.Context, mux *runtime.ServeMux) {
types.RegisterQueryHandlerClient(context.Background(), mux, types.NewQueryClient(clientCtx))
}
```

这将确保模块管理器注册我们定制的`deal`模块的查询服务器。

最后，我们完成了交易和合同的查询部分！在下一部分中，我们将负责处理事务和状态变化的消息服务。

参考这里的源代码- [*源代码*](https://github.com/Harry-027/deal)

系列
* [*第一部分*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*第二部分*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
* [*第三部分*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*第四部分*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc)
*[*第五部分*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3)

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[3 commas Review](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92)|[Pionex Review](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot)|[coin rule Review](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)*
*   *[莱杰 vs Ngrave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694) | [莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)*
*   *[Bybit 交易所评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)*
*   *[3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)*
*   *最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)*