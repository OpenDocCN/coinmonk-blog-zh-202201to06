# Hyperledger 结构的测试环境演示

> 原文：<https://medium.com/coinmonks/test-environment-demo-of-hyperledger-fabric-587905eedb16?source=collection_archive---------14----------------------->

在我之前的[帖子](https://iwasnothing.medium.com/hyperledger-fabric-privacy-illustration-1a275af403da)中，我使用了我的简单应用程序来说明 Hyperledger Fabric 中的隐私控制。在这篇文章中，我将详细解释链码的发展。完整的代码可以从[这里](https://github.com/iwasnothing/hlf_toy_app/blob/main/sharebook/sharebook.go)下载。

# 测试环境设置

Hyperledger Fabric 为代码开发和测试提供了简单的测试环境。安装步骤总结如下:

1.  下载[hyperledger/fabric-samples](https://github.com/hyperledger/fabric-samples)存储库。
2.  下载并执行安装脚本。该脚本将`cd`到`fabric-samples`文件夹，并将 docker 映像和可执行文件下载到/bin 和/config 目录中。

```
curl **-**sSL https:**//**bit**.**ly**/**2ysbOFE **|** bash **-**s
```

3.通过运行以下命令启动测试网络，这将启动订购服务、两个对等节点:org1.example.com 和 org2.example.com，并创建默认通道:“mychannel”。两个成员节点将加入该通道。

```
cd fabric**-**samples**/**test**-**network
./network.sh up createChannel
```

4.安装链码“`book`”。golang 代码存储在文件夹:`hlf_toy_app/sharebook/`

```
cd hlf_toy_app/sharebook/
go mod tidy
go mod vendor
go build
cd ../../fabric**-**samples**/**test**-**network
./network.sh deployCC -ccn book -ccp ../../hlf_toy_app/sharebook/
```

命令 deployCC 将 go 包部署到默认通道`mychannel`，然后从每个成员节点调用代码背书和提交。

对于链码的后续更新，您需要指定版本号和序列号。比如说。

```
./network.sh deployCC -ccn book -ccp ../../hlf_toy_app/sharebook/ -ccl go -ccv 2.0 -ccs 2-verbose
```

# 共享图书图书馆演示

1.  从 org1 创建一本书。在命令:`peer chaincode invoke`中，我们需要指定两个成员(ora1 和 org2)的端点和 CA cert 来签署事务，因为通道需要所有成员签名。否则，图书状态无法存储在渠道分类账中。

```
export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=$PWD/../config/
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org1MSP"
export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
export CORE_PEER_ADDRESS=localhost:7051peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n book --peerAddresses localhost:7051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt" --peerAddresses localhost:9051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt" -c '{"function":"CreateBook","Args":["my book","matthew","123456"]}'
```

命令`‘{“function”:”CreateBook”,”Args”:[“my book”,”matthew”,”123456"]}’` 将调用链码中定义的[功能](https://github.com/iwasnothing/hlf_toy_app/blob/462b5adf8fe8df83b1e0cedc8a5409ca52e2d475/sharebook/sharebook.go#L144)。

```
func (s *SmartContract) CreateBook(ctx contractapi.TransactionContextInterface, title string, author string, isbn string ) error {
...
...
```

命令结果将是:

```
2022-05-15 12:02:31.887 HKT 0001 INFO [chaincodeCmd] chaincodeInvokeOrQuery -> Chaincode invoke successful. result: status:200
```

2.查询图书信息。Org1 作为所有者可以查询图书信息，但是 Org2 还不在授权列表中，所以它不能查询图书。该查询将不会返回任何内容。

```
test-network %peer chaincode query -C mychannel -n book -c '{"Args":["GetAllBooks"]}'[{"ID":"book_2","Title":"my book","Author":"matthew","Isbn":"123456","Owner":"[Admin@org1.example.com](mailto:Admin@org1.example.com)","Holder":{"Org":"","StudentID":""},"IsBorrowed":false,"RequestQueue":[],"EntitleList":["[Admin@org1.example.com](mailto:Admin@org1.example.com)"],"ReaderList":[]}]
```

***吸取的额外教训:*** *本来想用 uuid 作为图书 id，但是发现交易会造成背书错误。这是因为 chaincode 将在所有成员节点中执行，每个成员执行返回的 uuid 将是随机的，并导致输出状态不匹配。交易将被拒绝。所以我需要使用图书数量作为 ID 中的序列号。*

3.在 org2 中注册学生。由于学生信息只会保存在 Org2 私有数据集合中，所以我们不需要添加 org1 来签署交易。此外，传递私有数据集合的参数应该用 base64 编码，并通过`--transient`传递。

```
export STUDENT_PROPERTIES=$(echo -n "{\"Name\":\"kaka\",\"Phone\":\"94071234\",\"Email\":\"a@b.com\"}" | base64 | tr -d \\n)peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n book    -c '{"function":"RegStudent","Args":[]}' --transient "{\"student_properties\":\"$STUDENT_PROPERTIES\"}"peer chaincode query -C mychannel -n book -c '{"Args":["GetAllStudents"]}'[{"Org":"[Admin@org2.example.com](mailto:Admin@org2.example.com)","StudentID":"[student_2@org2.example.com](mailto:student_1@org2.example.com)","Name":"kaka","Phone":"94071234","Email":"[a@b.com](mailto:a@b.com)"}]
```

如果我们在 org1 中运行查询，它将不会显示学生信息，也不会返回任何内容。

函数 RegStudent 是在 chaincode 中定义的，这里展示了它如何使用`ctx.GetStub().GetTransient()`从瞬态输入中获取参数

```
func (s *SmartContract) RegStudent(ctx contractapi.TransactionContextInterface) error {
  // Get new asset from transient map
  transientMap, err := ctx.GetStub().GetTransient()
  if err != nil {
        return fmt.Errorf("error getting transient: %v", err)
  }// Asset properties are private, therefore they get passed in transient field, instead of func args
  transientStudentJSON, ok := transientMap["student_properties"]
  if !ok {
        return fmt.Errorf("asset not found in the transient map input")
  }type StudentTransientInput struct {
                Name           string `json:"Name"`
                Phone          string `json:"Phone"`
                Email          string `json:"Email"`
  }var studentInput StudentTransientInput
err = json.Unmarshal(transientStudentJSON, &studentInput)
```

**:在根据学生人数创建新的学生 ID 时，我发现不能通过查询所有学生来计算学生人数。是因为通过范围搜索查询所有学生后，不允许再次更新学生状态。**

*4.如果新注册的学生想要运行 BorrowBook，将返回错误(500 ),因为我们还没有授予该学生和 org2 访问该书的权限。*

```
*test-network % peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n book --peerAddresses localhost:7051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt" --peerAddresses localhost:9051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt" -c '{"function":"BorrowBook","Args":["book_1","[student_2@org2.example.com](mailto:student_2@org2.example.com)"]}'Error: endorsement failure during invoke. response: status:500 message:"the book book_1 not entitled"*
```

*5.授予学生和组织 2 访问该书的权限。*

```
*export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=$PWD/../config/
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org1MSP"
export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
export CORE_PEER_ADDRESS=localhost:7051peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n book --peerAddresses localhost:7051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt" --peerAddresses localhost:9051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt" -c '{"function":"GrantBook","Args":["book_1","Admin@org2.example.com","student_2@org2.example.com"]}'2022-05-15 12:21:26.415 HKT 0001 INFO [chaincodeCmd] chaincodeInvokeOrQuery -> Chaincode invoke successful. result: status:200*
```

*6.如果我们再次运行之前的借书，就会成功。*

*在下一篇文章中，我将尝试在 AWS 管理的区块链上运行相同的链代码。*

> *加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资*

# *另外，阅读*

*   *[3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)*
*   *[莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)*
*   *[Bybit 交易所评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)*
*   *[3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)*
*   *最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)*
*   *[block fi vs Celsius](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630)|[Hodlnaut 审核](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 审核](https://coincodecap.com/kucoin-review)*