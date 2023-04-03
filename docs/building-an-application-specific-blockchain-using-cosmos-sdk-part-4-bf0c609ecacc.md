# 使用 Cosmos SDK 第 4 部分构建特定于应用程序的区块链

> 原文：<https://medium.com/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc?source=collection_archive---------6----------------------->

![](img/67d22c1322a6792f7b1032f45d93352e.png)

Photo by [Launchpresso](https://unsplash.com/@launchpresso?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/cryptocurrency?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在第 3 部分中，我们完成了处理合同和交易的查询处理程序和商店管理员。现在让我们来处理`Msg server`。

运行命令创建`createDeal`消息-

```
starport scaffold message createDeal vendor commission --module deal --response idValue
```

该命令执行以下操作-

*   创建消息定义(`tx.proto`)。

```
message MsgCreateDeal {
string creator = 1; // added by starport, this is the msg creator
string vendor = 2; // will store vendor address
uint64 commission = 3; //vendor commission for each order completion
}message MsgCreateDealResponse {
string idValue = 1;
}
```

*   实现满足`sdk.Msg`接口(message_create_contract.go)的方法。
*   创建交易消息处理程序(`msg_server_create_deal.go`)。
*   生成 cli 命令来调用处理程序(`tx_create_deal.go`)。
*   注册处理程序(`handler.go`)。

让我们修改消息处理程序`msg_server_create_deal.go`，如下所示

```
// msg_server_create_deal.gopackage keeperimport (
 "context"
 "strconv"
 "github.com/Harry-027/deal/x/deal/types"
 sdk "github.com/cosmos/cosmos-sdk/types"
)func (k msgServer) CreateDeal(goCtx context.Context, msg *types.MsgCreateDeal) (*types.MsgCreateDealResponse, error) { ctx := sdk.UnwrapSDKContext(goCtx) dealCounter, found := k.Keeper.GetDealCounter(ctx)
 if !found {
  panic("DealCounter not found")
 } dealId := strconv.FormatUint(dealCounter.IdValue, 10) newDeal := types.NewDeal{
  DealId:     dealId,
  Owner:      msg.Creator,
  Vendor:     msg.Vendor,
  Commission: msg.Commission,
 }*// validate before processing the message* err := newDeal.Validate()
if err != nil {
 return nil, err
}k.Keeper.SetNewDeal(ctx, newDeal)
dealCounter.IdValue++
k.Keeper.SetDealCounter(ctx, dealCounter)*// Set the new contract counter for a newly created deal* contractCounter := types.ContractCounter{
 DealId:  dealId,
 IdValue: 0,
}k.Keeper.SetContractCounter(ctx, contractCounter)ctx.GasMeter().ConsumeGas(types.CREATE_GAS, "Create Deal")ctx.EventManager().EmitEvent(
sdk.NewEvent(sdk.EventTypeMessage,
sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
sdk.NewAttribute(types.IDVALUE, dealId),
sdk.NewAttribute(types.OWNER, newDeal.Owner),
sdk.NewAttribute(types.VENDOR, newDeal.Vendor),
),
)return &types.MsgCreateDealResponse{
IdValue: dealId,
}, nil
}
```

注意，在执行的最后，我们消耗了一定量的气体。这是为了激励验证者和阻止垃圾短信。我们在常量(`contract_utils.go`)下定义了气体单位。我们还发出一个自定义事件来通知客户端关于成功发送的详细信息。

注意，在逻辑处理部分，我们首先获取`dealCounter`以得到`dealId`，然后将`deal`保存在存储中。此外，在保存交易之前，我们将借助`Validate()`方法验证消息，该方法将验证`vendor`地址和`commission`

```
// deal_utils.go
package typesimport (
sdk "github.com/cosmos/cosmos-sdk/types"
sdkerrors "github.com/cosmos/cosmos-sdk/types/errors"
)*// utility funcs* func (newDeal *NewDeal) GetOwnerAddress() (owner sdk.AccAddress, err error) {
owner, errInvalidOwner := sdk.AccAddressFromBech32(newDeal.Owner)
return owner, sdkerrors.Wrapf(errInvalidOwner, ErrInvalidOwner.Error(), newDeal.Owner)
}func (newDeal *NewDeal) GetVendorAddress() (vendor sdk.AccAddress, err error) {
vendor, errInvalidVendor := sdk.AccAddressFromBech32(newDeal.Vendor)
return vendor, sdkerrors.Wrapf(errInvalidVendor,   ErrInvalidVendor.Error(), newDeal.Vendor)
}func (newDeal *NewDeal) ValidateCommission() (err error) {
  if 1 <= newDeal.Commission && 100 >= newDeal.Commission {
    return nil
  }
  return ErrInvalidCommission
}func (newDeal *NewDeal) Validate() (err error) {
_, err = newDeal.GetOwnerAddress()
if err != nil {
  return err
}_, err = newDeal.GetVendorAddress()
if err != nil {
  return err
}err = newDeal.ValidateCommission()
  return err
}
```

让我们为 cli 命令`tx_create_deal.go`编写代码

```
package cliimport (

 "github.com/Harry-027/deal/x/deal/types"
 "github.com/cosmos/cosmos-sdk/client"
 "github.com/cosmos/cosmos-sdk/client/flags"
 "github.com/cosmos/cosmos-sdk/client/tx"
 "github.com/spf13/cast"
 "github.com/spf13/cobra"
)func CmdCreateDeal() *cobra.Command {
 cmd := &cobra.Command{
 Use:   "create-deal [vendor] [commission]",
 Short: "Broadcast message createDeal",
 Args:  cobra.ExactArgs(2),
 RunE: func(cmd *cobra.Command, args []string) (err error) { argVendor := args[0]
  argCommission, err := cast.ToUint64E(args[1])
  if err != nil {
   return err
  } clientCtx, err := client.GetClientTxContext(cmd)
  if err != nil {
   return err
  } msg := types.NewMsgCreateDeal(
  clientCtx.GetFromAddress().String(),
   argVendor,
   argCommission,
 ) if err := msg.ValidateBasic(); err != nil {
  return err
 } return tx.GenerateOrBroadcastTxCLI(clientCtx, cmd.Flags(), msg)
 },
} flags.AddTxFlagsToCmd(cmd)
 return cmd
}
```

注意方法`msg.ValidateBasic()`(如上所用)也被 cosmos sdk 在`checkTx`方法中调用来验证 Tx，这样 tendermint 可以避免 mempool 中的无效 Tx。

现在，让我们为 createContract 命令搭建脚手架

```
starport scaffold message createContract dealId consumer desc ownerETA expiry fees --module deal --response idValue
```

我们的原型定义看起来像-

```
message MsgCreateContract {
string creator = 1;
string dealId = 2;
string consumer = 3;
string desc = 4;
string ownerETA = 5;
string expiry = 6;
uint64 fees = 7;
}message MsgCreateContractResponse {
string idValue = 1;
string contractStatus = 2;
}
```

`contractStatus`字段是后来手动添加的。添加字段`contractStatus`字段后，运行命令重新生成原型文件-

```
starport generate proto-go
```

修改处理器如下- ( `msg_server_create_contract.go`)

```
package keeper
import (
"context"
"strconv"
"time"
"github.com/Harry-027/deal/x/deal/types"
 sdk "github.com/cosmos/cosmos-sdk/types"
)*// CreateContract is the tx handler to handle create contract messages* func (k msgServer) CreateContract(goCtx context.Context, msg *types.MsgCreateContract) (*types.MsgCreateContractResponse, error) {
 ctx := sdk.UnwrapSDKContext(goCtx)
 deal, found := k.Keeper.GetNewDeal(ctx, msg.DealId) if !found {
  return nil, types.ErrDealNotFound
 } *// validate if the tx came from owner* if msg.Creator != deal.Owner {
  return nil, types.ErrInvalidOwner
 } contractCounter, found := k.Keeper.GetContractCounter(ctx,  msg.DealId)if !found {
  return nil, types.ErrDealNotFound
}contractCounter.IdValue++
contractId := strconv.FormatUint(contractCounter.IdValue, 10)
etaInMins, err := strconv.Atoi(msg.OwnerETA)if err != nil {
 return nil, types.ErrInvalidTime
}expiryInMins, err := strconv.Atoi(msg.Expiry)
if err != nil {
 return nil, types.ErrInvalidTime
}expiry := ctx.BlockTime().Add(time.Duration(expiryInMins) * time.Minute)*// create a new contract under the given dealId*newContract := types.NewContract{
DealId:     msg.DealId,
ContractId: contractId,
Consumer:   msg.Consumer,
Desc:       msg.Desc,
OwnerETA:   uint32(etaInMins),
Expiry:     expiry.UTC().Format(types.TIME_FORMAT),
Fees:       msg.Fees,
StartTime:  ctx.BlockTime().UTC().Format(types.TIME_FORMAT),
Status:     types.INITIATED,
}k.Keeper.SetNewContract(ctx, newContract)
k.Keeper.SetContractCounter(ctx, contractCounter)
ctx.GasMeter().ConsumeGas(types.CREATE_GAS, "Create Contract")ctx.EventManager().EmitEvent(
sdk.NewEvent(sdk.EventTypeMessage,
sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
sdk.NewAttribute(sdk.AttributeKeyAction, types.INITIATED),
sdk.NewAttribute(types.IDVALUE, newContract.ContractId),
sdk.NewAttribute(types.START_TIME, newContract.StartTime),
),
)return &types.MsgCreateContractResponse{IdValue: contractId, ContractStatus: types.INITIATED}, nil}
```

我们正根据关键字`NewContract/value/{contractId}/`将合同存储在前缀关键字为`NewContract/value/{dealId}/`的商店下。此外，我们确认只有当 tx 来自交易所有人时，才能处理`createContract`tx。

一旦交易所有人创建了合同，供应商需要提交，消费者需要在到期时间之前批准，否则合同将被视为到期。为此，我们将生成另外两条消息- `commitContract`和`approveContract`。tx `commitContract`将以分钟为单位输入发货时间(`vendorETA`)，这是卖方完成订单的承诺。搭建这两条消息留给您作为练习:)

让我们来看看`commitContract`的处理程序——

```
// msg_server_commit_contract.go
package keeperimport (
"context"
"strconv"
"time"
"github.com/Harry-027/deal/x/deal/types"
sdk "github.com/cosmos/cosmos-sdk/types"
)*// CommitContract is the tx handler to handle commit contract messages*func (k msgServer) CommitContract(goCtx context.Context, msg *types.MsgCommitContract) (*types.MsgCommitContractResponse, error) {
  ctx := sdk.UnwrapSDKContext(goCtx)
  deal, found := k.Keeper.GetNewDeal(ctx, msg.DealId)
  if !found {
     return nil, types.ErrDealNotFound
  }*// validate is the transaction is coming from vendor* if msg.Creator != deal.Vendor {
   return nil, types.ErrInvalidVendor
}contract, found := k.Keeper.GetNewContract(ctx, msg.DealId, msg.ContractId)if !found {
 return nil, types.ErrContractNotFound
}
expiry, err := time.Parse(types.TIME_FORMAT, contract.Expiry)if err != nil {
 panic("invalid expiry time")
}*// don't process the expired contracts* if ctx.BlockTime().After(expiry) {
 return nil, types.ErrContractExpired
}etaInMins, err := strconv.Atoi(msg.VendorETA)if err != nil {
 return nil, types.ErrInvalidTime
}*// validate the vendor ETA* if (contract.OwnerETA / 2) < uint32(etaInMins) {
 return nil, types.ErrVendorETA
}*// process and emit the custom event* contract.Status = types.COMMITTED
contract.VendorETA = uint32(etaInMins)
k.Keeper.SetNewContract(ctx, contract)ctx.GasMeter().ConsumeGas(types.PROCESS_GAS, "Commit Contract")ctx.EventManager().EmitEvent(
 sdk.NewEvent(sdk.EventTypeMessage,
 sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
 sdk.NewAttribute(sdk.AttributeKeyAction, types.COMMITTED),
 sdk.NewAttribute(types.IDVALUE, contract.ContractId),
 sdk.NewAttribute(types.VENDOR_ETA,  strconv.FormatUint(uint64(contract.VendorETA), 10)),
sdk.NewAttribute(types.OWNER_ETA,  strconv.FormatUint(uint64(contract.OwnerETA), 10)),
 ),
)return &types.MsgCommitContractResponse{IdValue: contract.ContractId, ContractStatus: contract.Status}, nil
}
```

在`commitContract`下，我们在将合同状态更改为已承诺之前验证以下内容-

*   如果交易来自供应商。
*   如果合同还没到期。
*   如果 vendorETA ≤ ownerETA /2。

让我们来看看`approveContract`处理器-

```
// msg_server_approve_contract.gopackage keeperimport (
 "context"
 "time"
 "github.com/Harry-027/deal/x/deal/types"
 sdk "github.com/cosmos/cosmos-sdk/types"
 sdkerrors "github.com/cosmos/cosmos-sdk/types/errors"
)*// ApproveContract is the tx handler for handling approve contract messages* func (k msgServer) ApproveContract(goCtx context.Context, msg *types.MsgApproveContract) (*types.MsgApproveContractResponse, error) {ctx := sdk.UnwrapSDKContext(goCtx)
contract, found := k.Keeper.GetNewContract(ctx, msg.DealId,  msg.ContractId)if !found {
 return nil, types.ErrContractNotFound
}*// handle validation before processing* err := msg.DealHandlerValidation(goCtx, &contract)
if err != nil {
 return nil, err
}expiryTime, err := time.Parse(types.TIME_FORMAT, contract.Expiry)
if err != nil {
 return nil, err
}*// don't process the expired contracts* if ctx.BlockTime().After(expiryTime) {
 return nil, types.ErrContractExpired
}*// store funds from user account to module escrow account and approve the contract*consumerAddress, err := contract.GetConsumerAddress()
if err != nil {
panic("Invalid consumer address")
}err = k.bank.SendCoinsFromAccountToModule(ctx, consumerAddress, types.ModuleName, sdk.NewCoins(contract.GetCoin(contract.Fees)))if err != nil {
 return nil, sdkerrors.Wrapf(err, types.ErrPaymentFailed.Error())
}contract.Status = types.APPROVED
k.Keeper.SetNewContract(ctx, contract)*// consume the gas to incentivize validators* ctx.GasMeter().ConsumeGas(types.PROCESS_GAS, "Approve Contract")*// emit custom event that clients can subscribe to* ctx.EventManager().EmitEvent(
sdk.NewEvent(sdk.EventTypeMessage,
sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
sdk.NewAttribute(sdk.AttributeKeyAction, types.APPROVED),
sdk.NewAttribute(types.IDVALUE, contract.ContractId),
),
)return &types.MsgApproveContractResponse{
IdValue:        contract.ContractId,
ContractStatus: contract.Status,
}, nil
}
```

用户将启动`approveContract` tx。该 tx 将执行以下步骤-

*   验证 tx 是否由消费者签名。
*   验证合同是否已提交。
*   验证合同是否尚未到期。
*   将资金从消费者账户转移到模块托管账户。

注意处理程序中使用的`msg.DealHandlerValidation`的定义如下-

```
// message_approve_contract.gofunc (msg *MsgApproveContract) DealHandlerValidation(goCtx context.Context, contract *NewContract) error {if msg.Creator != contract.Consumer {
 return ErrInvalidConsumer
}if contract.Status != COMMITTED {
 return ErrNotCommitted
}return nil
}
```

我们在这里使用银行保管员进行资金转移操作。为了访问银行保管员公开的任何功能，我们需要在我们的具体保管员类型中注入银行保管员接口-

```
// keeper.go
*// concrete keeper type for deal module also includes bank & account keeper interface for handling fund related transactions*type (
Keeper struct {
auth       types.AccountKeeper
bank       types.BankKeeper
cdc        codec.BinaryCodec
storeKey   sdk.StoreKey
memKey     sdk.StoreKey
paramstore paramtypes.Subspace
})
```

因此，我们的`keeper`构造函数将改变如下-

```
func NewKeeper(
auth types.AccountKeeper,
bank types.BankKeeper,
cdc codec.BinaryCodec,
storeKey,
memKey sdk.StoreKey,
ps paramtypes.Subspace,
) *Keeper {
*// set KeyTable if it has not already been set* if !ps.HasKeyTable() {
ps = ps.WithKeyTable(types.ParamKeyTable())
}return &Keeper{
 auth:       auth,
 bank:       bank,
 cdc:        cdc,
 storeKey:   storeKey,
 memKey:     memKey,
 paramstore: ps,
 }
}
```

让我们在`app.go`的初始化阶段通过我们的 keeper 构造中的银行 keeper 接口

```
// app.goapp.DealKeeper = *dealmodulekeeper.NewKeeper(
app.AccountKeeper,
app.BankKeeper,
appCodec,
keys[dealmoduletypes.StoreKey],
keys[dealmoduletypes.MemStoreKey],
app.GetSubspace(dealmoduletypes.ModuleName),
)
```

当我们传递非具体类型的银行保管员接口时，我们的保管员具体类型需要理解将使用银行保管员接口中的哪个方法。因此，在`expected_keepers.go`下定义一个`interface`用于我们要从银行保管员那里访问的方法-

```
*// BankKeeper defines the expected interface needed to retrieve account balances.*type BankKeeper interface {
 SpendableCoins(ctx sdk.Context, addr sdk.AccAddress) sdk.Coins
 GetBalance(ctx sdk.Context, addr sdk.AccAddress, denom string)  sdk.Coin
 SendCoinsFromModuleToAccount(ctx sdk.Context, senderModule string,  recipientAddr sdk.AccAddress, amt sdk.Coins) error
 SendCoinsFromAccountToModule(ctx sdk.Context, senderAddr sdk.AccAddress, recipientModule string, amt sdk.Coins) error*// Methods imported from bank should be defined here* }*// AccountKeeper defines the expected account keeper used for simulations (noalias)*type AccountKeeper interface {
 GetAccount(ctx sdk.Context, addr sdk.AccAddress) types.AccountI
 GetModuleAddress(name string) sdk.AccAddress
*// Methods imported from account should be defined here* }
```

请注意，我们还将在`orderDelivered`处理程序中使用记账员。因此，在我们的具体保管员类型中传递相同的，就像我们为银行保管员接口所做的一样。

在合同被批准后，我们必须发出自定义事件，让 FE 客户端了解合同状态。这将通知卖方合同批准，以便卖方可以开始处理订单。一旦订单准备就绪，供应商将启动 tx，将合同状态更改为`INDELIVERY`。该 tx 还将根据初始发货承诺时间(`vendorETA`)计算是否有任何发货延迟。让我们来看看汉德勒-

```
//msg_server_ship_order.go*// ShipOrder is the tx handler for shipOrder messages from Vendor* func (k msgServer) ShipOrder(goCtx context.Context, msg *types.MsgShipOrder) (*types.MsgShipOrderResponse, error) {ctx := sdk.UnwrapSDKContext(goCtx)
deal, found := k.Keeper.GetNewDeal(ctx, msg.DealId)
if !found {
 return nil, types.ErrDealNotFound
}*// validate if the tx is from vendor* if msg.Creator != deal.Vendor {
  return nil, types.ErrInvalidVendor
}contract, found := k.Keeper.GetNewContract(ctx, msg.DealId,
msg.ContractId)
if !found {
 return nil, types.ErrContractNotFound
}if contract.Status != types.APPROVED || contract.Status == types.COMPLETED {
 return nil, types.ErrNotApprovedOrCompleted
}startTime, err := time.Parse(types.TIME_FORMAT, contract.StartTime)
if err != nil {
 panic("invalid start time")
}*// Calculate shipping delay if any (will be used later to calculate delay penalty)* shippingExpectedTime := startTime.Add(time.Duration(contract.VendorETA))shippingActualTime := ctx.BlockTime()
if shippingActualTime.After(shippingExpectedTime) {
shippingTimeDelay :=  shippingActualTime.Sub(shippingExpectedTime).Minutes()
contract.ShippingDelay = uint32(shippingTimeDelay)
}*// mark the contract status as in delivery* contract.Status = types.INDELIVERY
k.Keeper.SetNewContract(ctx, contract)ctx.GasMeter().ConsumeGas(types.PROCESS_GAS, "Order shipped")ctx.EventManager().EmitEvent(
 sdk.NewEvent(sdk.EventTypeMessage,
 sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
 sdk.NewAttribute(sdk.AttributeKeyAction, types.INDELIVERY),
 sdk.NewAttribute(types.IDVALUE, contract.ContractId),
 ),
)return &types.MsgShipOrderResponse{IdValue: contract.ContractId,  ContractStatus: contract.Status}, nil
}
```

在将合同状态更改为`INDELIVERY`之前，我们在此记录运输延迟(如果有)。这将有助于我们计算订单交付后的延迟费用。请注意，我们有从`ctx.BlockTime()`开始的当前可用时间。根据延期费用，将为交易所有人和供应商计算付款。和延期费用(如果有的话)将退还给消费者账户。

一旦订单到达消费者家门口，他需要启动一个 tx 来完成订单。该 tx 将订单标记为已完成，并将根据供应商佣金和延期费用结算所有资金。让我们简单了解一下`orderDelivered`汉德勒。

```
// msg_server_order_delivered.gopackage keeperimport (
"context"
"strconv"
"time"
"github.com/Harry-027/deal/x/deal/types"
sdk "github.com/cosmos/cosmos-sdk/types"
sdkerrors "github.com/cosmos/cosmos-sdk/types/errors"
)func (k msgServer) OrderDelivered(goCtx context.Context, msg *types.MsgOrderDelivered) (*types.MsgOrderDeliveredResponse, error) {
 ctx := sdk.UnwrapSDKContext(goCtx)
 logger := k.Logger(ctx)
 deal, found := k.Keeper.GetNewDeal(ctx, msg.DealId)if !found {
 return nil, types.ErrDealNotFound
}*// validate before processing the message* contract, found := k.Keeper.GetNewContract(ctx, msg.DealId, msg.ContractId)
if !found {
 return nil, types.ErrContractNotFound
}if msg.Creator != contract.Consumer {
 return nil, types.ErrInvalidConsumer
}if contract.Status != types.INDELIVERY || contract.Status == types.COMPLETED {
 return nil, types.ErrNotShipped
}startTime, err := time.Parse(types.TIME_FORMAT, contract.StartTime)
if err != nil {
 panic("invalid start time")
}deliveryExpectedTime := startTime.Add(time.Duration(contract.OwnerETA))
deliveryActualTime := ctx.BlockTime()
logger.Debug("deliveryExpectedTime :: ", deliveryExpectedTime)
logger.Debug("deliveryActualTime :: ", deliveryActualTime)*// calculate the delivery delay in case if any* if deliveryActualTime.After(deliveryExpectedTime) {
deliveryTimeDelay := deliveryActualTime.Sub(deliveryExpectedTime).Minutes()
logger.Debug("deliveryTimeDelay :: ", deliveryTimeDelay)if contract.ShippingDelay != 0 {
*// subtract the shipping delay if any* deliveryTimeDelay = deliveryTimeDelay - float64(contract.ShippingDelay)
logger.Debug("deliveryTimeDelay after subtracting shipping delay", deliveryTimeDelay)
}contract.DeliveryDelay = uint32(deliveryTimeDelay)
}timeTaken := deliveryActualTime.Sub(startTime).Minutes()
logger.Debug("timeTaken :: ", timeTaken)var refundAmount float64 = 0
orderPayment := float64(contract.Fees)*// calculate the penalty for late delivery/shipping for owner & vendor respectively* if timeTaken != 0 {
vendorSlashPercent := float64(contract.ShippingDelay) / timeTaken
logger.Debug("vendorSlashPercent :: ", vendorSlashPercent)ownerSlashPercent := float64(contract.DeliveryDelay) / timeTakenlogger.Debug("ownerSlashPercent :: ", ownerSlashPercent)refundAmount = (vendorSlashPercent + ownerSlashPercent) * orderPayment * 0.01
logger.Debug("refundAmount :: ", refundAmount)
}*//deduct delay charges from payment* totalPay := uint64(orderPayment - refundAmount)
logger.Debug("TotalPay :: ", totalPay)
moduleAccount := k.auth.GetModuleAddress(types.ModuleName)
moduleBalance := k.bank.GetBalance(ctx, moduleAccount, types.TOKEN)if moduleBalance.IsLT(contract.GetCoin(totalPay)) {
 panic("Escrow account insufficient balance")
}*// calculate the vendor payment for given order based on deal commission* vendorPay := uint64(0.01 * float64(deal.Commission*totalPay))
logger.Debug("vendorPay :: ", vendorPay)*// calculate the owner payment* ownerPay := totalPay - vendorPay
logger.Debug("ownerPay :: ", ownerPay)*// validate the addresses for different parties involved in the contract* consumerAddress, err := contract.GetConsumerAddress()
if err != nil {
 panic("Invalid consumer address")
}ownerAddress, err := deal.GetOwnerAddress()
if err != nil {
 panic("Invalid owner address")
}
vendorAddress, err := deal.GetVendorAddress()if err != nil {
panic("Invalid vendor address")
}*// process the payment for all the parties
// refund the delay charges to consumer*err = k.bank.SendCoinsFromModuleToAccount(ctx, types.ModuleName, consumerAddress, sdk.NewCoins(contract.GetCoin(uint64(refundAmount))))
if err != nil {
return nil, sdkerrors.Wrapf(err, types.ErrPaymentFailed.Error())
}err = k.bank.SendCoinsFromModuleToAccount(ctx, types.ModuleName, ownerAddress, sdk.NewCoins(contract.GetCoin(ownerPay)))
if err != nil {
return nil, sdkerrors.Wrapf(err, types.ErrPaymentFailed.Error())
}err = k.bank.SendCoinsFromModuleToAccount(ctx, types.ModuleName, vendorAddress, sdk.NewCoins(contract.GetCoin(vendorPay)))
if err != nil {
return nil, sdkerrors.Wrapf(err, types.ErrPaymentFailed.Error())
}*// mark the contract status as completed as order has been delivered to consumer and settlement is complete* contract.Status = types.COMPLETED
k.Keeper.SetNewContract(ctx, contract)ctx.GasMeter().ConsumeGas(types.SETTLEMENT_GAS, "Order delivered")ctx.EventManager().EmitEvent(
sdk.NewEvent(sdk.EventTypeMessage,
sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
sdk.NewAttribute(sdk.AttributeKeyAction, types.COMPLETED),
sdk.NewAttribute(types.IDVALUE, contract.ContractId),
sdk.NewAttribute(types.CONSUMER, contract.Consumer),
sdk.NewAttribute(types.OWNER, deal.Owner),
sdk.NewAttribute(types.VENDOR, deal.Vendor),
sdk.NewAttribute(types.REFUND_PAY, strconv.FormatUint(uint64(refundAmount), 10)),
sdk.NewAttribute(types.OWNER_PAY, strconv.FormatUint(ownerPay, 10)),
sdk.NewAttribute(types.VENDOR_PAY, strconv.FormatUint(vendorPay, 10)),
),
)
return &types.MsgOrderDeliveredResponse{IdValue: contract.ContractId, ContractStatus: contract.Status}, nil
}
```

在上面的`orderDelivered`处理程序中，在订单开始时间和发货延迟的帮助下，我们计算交货延迟(如果有)。计算出的延误费用与运输延误费用相加，并退还给消费者。鉴于卖方和业主根据卖方佣金和延期费用获得报酬。

让我们添加一个处理程序来取消订单，以防订单交付需要更多时间，用户可能想要取消订单。

```
// msg_server_cancel_order.go*// CancelOrder is the tx handler for handling cancel order messages*func (k msgServer) CancelOrder(goCtx context.Context, msg *types.MsgCancelOrder) (*types.MsgCancelOrderResponse, error) {ctx := sdk.UnwrapSDKContext(goCtx)
contract, found := k.Keeper.GetNewContract(ctx, msg.DealId, msg.ContractId)if !found {
 return nil, types.ErrContractNotFound
}
err := msg.DealHandlerValidation(goCtx, &contract)if err != nil {
 return nil, err
}consumerAddress, err := contract.GetConsumerAddress()
if err != nil {
  panic("Invalid consumer address")
}*// Validate is the escrow account has enough balance to process the refund* moduleAccount := k.auth.GetModuleAddress(types.ModuleName)
moduleBalance := k.bank.GetBalance(ctx, moduleAccount, types.TOKEN)if moduleBalance.IsLT(contract.GetCoin(contract.Fees)) {
 panic("Escrow account insufficient balance")
}*// Send coins from contract account to the consumer account*err = k.bank.SendCoinsFromModuleToAccount(ctx, types.ModuleName, consumerAddress, sdk.NewCoins(contract.GetCoin(contract.Fees)))if err != nil {
 return nil, sdkerrors.Wrapf(err, types.ErrPaymentFailed.Error())
}*// mark contract status as cancelled* contract.Status = types.CANCELLED
k.Keeper.SetNewContract(ctx, contract)ctx.GasMeter().ConsumeGas(types.PROCESS_GAS, "Cancel Contract")ctx.EventManager().EmitEvent(
sdk.NewEvent(sdk.EventTypeMessage,
sdk.NewAttribute(sdk.AttributeKeyModule, types.ModuleName),
sdk.NewAttribute(sdk.AttributeKeyAction, types.CANCELLED),
sdk.NewAttribute(types.IDVALUE, contract.ContractId),
),
)return &types.MsgCancelOrderResponse{IdValue: contract.ContractId, ContractStatus: contract.Status}, nil
}
```

如果订单交付延迟 20 分钟，我们允许用户取消订单，并将全部金额退还到用户帐户地址。

最后，我们完成了 Msg 服务器处理程序。请确认我们的消息处理程序已经被模块注册-

```
//module.gofunc (am AppModule) Route() sdk.Route {
 return sdk.NewRoute(types.RouterKey, NewHandler(am.keeper))
}
```

现在，在启动区块链并测试消息和查询之前，让我们纠正起源状态以初始化交易计数器值。

```
// types/genesis.gofunc DefaultGenesis() *GenesisState {
return &GenesisState{
DealCounter: &DealCounter{
 IdValue: uint64(1),
},
NewDealList:     []NewDeal{},
ContractCounter: nil,
NewContractList: []NewContract{},
*// this line is used by starport scaffolding # genesis/types/default* Params: DefaultParams(),
}
}
```

确保我们正确初始化和导出创世状态-

```
// x/deal/genesis.gopackage dealimport (
"github.com/Harry-027/deal/x/deal/keeper"
"github.com/Harry-027/deal/x/deal/types"
sdk "github.com/cosmos/cosmos-sdk/types"
)
*// InitGenesis initializes the capability module's state from a provided genesis state.* func InitGenesis(ctx sdk.Context, k keeper.Keeper, genState types.GenesisState) {*// Set if defined* if genState.DealCounter != nil {
  k.SetDealCounter(ctx, *genState.DealCounter)
}*// Set all the newDeal* for _, elem := range genState.NewDealList {
 k.SetNewDeal(ctx, elem)
}for _, elem := range genState.ContractCounter {
  k.SetContractCounter(ctx, *elem)
}*// Set all the newContract* for _, elem := range genState.NewContractList {
 k.SetNewContract(ctx, elem)
}*// this line is used by starport scaffolding # genesis/module/init* k.SetParams(ctx, genState.Params)
}*// ExportGenesis returns the capability module's exported genesis.* func ExportGenesis(ctx sdk.Context, k keeper.Keeper) *types.GenesisState {
genesis := types.DefaultGenesis()
genesis.Params = k.GetParams(ctx)
*// Get all dealCounter* dealCounter, found := k.GetDealCounter(ctx)
if found {
 genesis.DealCounter = &dealCounter
}genesis.NewDealList = k.GetAllNewDeal(ctx)
*// Get all contractCounter* contractCounter, err := k.GetAllContractCounter(ctx)
if err == nil {
 genesis.ContractCounter = contractCounter
}for _, counter := range contractCounter {
contractsForDealId := k.GetAllNewContract(ctx, counter.DealId)
 genesis.NewContractList = append(genesis.NewContractList,  contractsForDealId...)
}*// this line is used by starport scaffolding # genesis/module/export* return genesis
}
```

运行命令`starport chain serve`来加速我们的开发节点。

打开另一个终端并运行命令`starport chain build`，这将生成`deald`二进制文件，用于测试 txs 并查询正在运行的节点。

在下一部分中，我们将了解自定义事件索引以及用户如何订阅自定义索引事件。

这里引用源代码- [*源代码*](https://github.com/Harry-027/deal)

系列
*[*Part-1*](/coinmonks/building-an-application-specific-blockchain-using-cosmos-sdk-part-1-1f8388902fc8) ***[*Part-2*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-2-3da0b727cd9b)
*[*Part-3*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-3-8ab623f35c74) ***[*Part-4*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-4-bf0c609ecacc) ***[*Part-5*](/@harish0y2j/building-an-application-specific-blockchain-using-cosmos-sdk-part-5-e22c9a6debe3) ***

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [交易信号是什么？](https://coincodecap.com/trading-signal) | [Bitstamp vs 比特币基地](https://coincodecap.com/bitstamp-coinbase) | [买索拉纳](https://coincodecap.com/buy-solana)
*   [ProfitFarmers 点评](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix Trading Bot](https://coincodecap.com/cornix-trading-bot)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [my constant Review](https://coincodecap.com/myconstant-review)|[8 款最佳摇摆交易机器人](https://coincodecap.com/best-swing-trading-bots)
*   [MXC 交易所评论](/coinmonks/mxc-exchange-review-3af0ec1cba8c) | [Pionex vs 币安](https://coincodecap.com/pionex-vs-binance) | [Pionex 套利机器人](https://coincodecap.com/pionex-arbitrage-bot)