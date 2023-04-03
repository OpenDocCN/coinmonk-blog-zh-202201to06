# Hyperledger 结构隐私插图

> 原文：<https://medium.com/coinmonks/hyperledger-fabric-privacy-illustration-1a275af403da?source=collection_archive---------16----------------------->

在我之前的[帖子](/coinmonks/cordapp-example-to-illustrate-privacy-fbc51ce87f78)中，我用 R3 Corda 展示了隐私是如何在私有区块链中得到保护的。在这篇文章中，我想对另一个流行的私有区块链平台 Hyperledger Fabric 做同样的事情。

# 超级分类帐结构体系

Hyperledger Fabric 由订购服务组成，该服务提供关于区块链事务的一致服务，然后将事务块广播到每个成员的对等节点。每个成员都在成员资格服务提供程序中注册了自己的成员资格，X509 证书将在该服务提供程序中授予。每个成员至少有一个对等节点，它保存分类帐的副本并执行名为 chiancode 的智能契约。

总账只是一个简单的<key>数据库。chaincode 调用只是调用`GetState`和`PutState`通过实体键字符串(state-id)读写数据库。通常，状态将被封送到 json 字符串中作为实体值存储。</key>

# Hyperledger 结构中的隐私

在 Hyperledger Fabric 网络中，数据受渠道范围的保护。每个频道都有自己的分类账。相互信任和沟通的多个成员将加入通道并共享分类帐数据的副本。分类帐数据操作的应用程序逻辑以名为 chaincode 的智能契约的形式实现。每个渠道成员的对等节点将执行链码来更新分类帐数据。每个分类账交易必须由所有渠道成员或渠道配置中预定义的成员子集进行验证和签名。

如果您希望将一些私有数据限制在每个成员本身，可以使用私有数据集合。每个成员都有一个隐式的默认私有数据集合(命名为“_implicit_org_ <mspid>”)，该集合仅限于成员自身，因此每个组织成员都可以存储一些仅由自己共享的私有数据。可以用不同的共享规则来定义额外的私有数据收集，这些规则允许数据被通道内的成员子集共享。</mspid>

# Croda 和 Hyperledger 面料的区别

Hyperledger Fabric 和 R3 Corda 之间的一个关键区别是，Corda 交易可以由不同方签署。比如交易 001 是甲乙双方签字，而交易 002 是甲乙丙双方签字，那么，甲方只能看到交易 001，看不到交易 002，而乙方可以同时看到交易 001 和交易 002。在 Hyperledger Farbic 中，隐私在频道范围内受到保护。同一渠道的所有交易数据都存储在所有渠道成员的总账中。交易由所有渠道成员或渠道配置中预定义的成员子集进行验证和签名。

我的经验是 R3 Corda 更灵活，因为事务数据是在流执行运行时根据共享逻辑共享的。但是，在 Hyperledger Frabic 中，共享规则必须在创建渠道时使用交易背书政策或私人数据收集定义进行预设。

# 隐私插图

这里我用我之前的例子 app(共享学校图书馆)来说明这一点。在这个例子中，每本书都有自己授权列表。只有授权列表中的当事人可以查看和借阅图书。

在 Corda 中，图书创作由权利列表中的各方签署。由于不同的书籍可以有不同的权限列表，因此不同书籍的数据由不同的当事人子集存储，但不是所有当事人。

在 Hyperledger Fabric 中，所有帐簿数据都存储在所有渠道成员的分类帐中。尽管我们仍然为每本书定义了授权列表，但我们只能阻止不在授权列表中的成员查询书的详细信息和借书/还书。图书信息仍然存储在每个渠道成员的分类帐数据库中，即使该成员不能查询图书信息。下面是访问控制检查的代码。

```
for _, v := range book.EntitleList {
           if v == caller {
                books = append(books, &book)
                break;
           }}
```

`caller`是成员节点用户运行的查询图书命令的通用名。Hyperledger Fabric 提供了获取成员节点身份的 API:`ctx.GetStub().GetCreator()`，身份是一个 X.509 证书。为了便于阅读，我从证书中提取了 CommonName。

```
func (s *SmartContract) GetClientName(ctx contractapi.TransactionContextInterface) (string,error) {
  caller,err := ctx.GetStub().GetCreator()
  if err != nil {
    return "",err
  }
  re := regexp.MustCompile("-----BEGIN CERTIFICATE-----[^ ]+-----END CERTIFICATE-----\n")
  match := re.FindStringSubmatch(string(caller))
  pemBlock, _ := pem.Decode([]byte(match[0]))
  cert, err := x509.ParseCertificate(pemBlock.Bytes)
  if err != nil {
    return "",err
  }
  owner := cert.Subject.CommonName
  return owner,nil
}
```

# 学生个人信息如何保护？

图书信息通常可以在所有组织(学校)之间共享，但学生信息应该保存在每个组织(学校)内部，而不应该共享。这样的私有信息可以通过调用`PutPrivateData`存储在隐式默认私有数据集合中。这是代码。

```
student := Student{
    Org:            caller,
    StudentID:      id,
    Name:           studentInput.Name,
    Phone:          studentInput.Phone,
    Email:          studentInput.Email,
  }
  studentJSON, err := json.Marshal(student)
  if err != nil {
    return err
  }return ctx.GetStub().PutPrivateData(PrivateCollection,id, studentJSON)
```

其他成员节点不能读取学生信息，但是它们可以通过从学生 id 获取数据散列来检查是否存在。

```
studentHash,err := ctx.GetStub().GetPrivateDataHash(PrivateCollection, student)
  if err != nil {
    return "",err
  }
  if studentHash == nil {
    return "",fmt.Errorf("cannot find the student")
  }
```

理论上，如果用户提供私有信息，每个节点可以通过比较信息的 SHA 哈希来验证信息的正确性。

完整的代码可以在这里找到[。](https://github.com/iwasnothing/hlf_toy_app/blob/main/sharebook/sharebook.go)

在下一篇文章中，我会解释更多关于代码的内容。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit Exchange 审查](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 审查](https://coincodecap.com/bityard-reivew) | [Jet-Bot 审查](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)
*   [BlockFi vs 摄氏度](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630) | [Hodlnaut 审核](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 审核](https://coincodecap.com/kucoin-review)