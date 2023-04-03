# 在 iOS 中创建以太坊钱包—第 2 部分

> 原文：<https://medium.com/coinmonks/create-an-ethereum-wallet-in-ios-part-2-9cb9baabfd8c?source=collection_archive---------9----------------------->

![](img/5f6623aef25267d6999d9b0e0eb5a66d.png)

关于第二部分已经推迟了一段时间，我在过去的 6 个月里一直很忙，所以让我们直奔主题吧！

简要回顾一下，第 1 部分包括以下主题:

[](/coinmonks/create-an-ethereum-wallet-in-ios-part-1-1e2f215226b7) [## 在 iOS 中创建以太坊钱包—第 1 部分

### 如今，区块链变得越来越受欢迎，在这十年中涌现了许多创业公司和应用程序…

medium.com](/coinmonks/create-an-ethereum-wallet-in-ios-part-1-1e2f215226b7) 

# 帐目

加载现有帐户

1.输入帐户私钥的十六进制字符串

2.输入 12 个单词的助记短语

生成、删除和导出账户

在第 2 部分中，我们将讨论以下主题:

**余额**

显示 ETH、DAI 和 USDC 的余额

您可以查看第 1 部分以了解更多关于帐户操作的信息，本文将重点介绍如何在以太坊中显示余额

那么，我们开始进入主题吧！

# 显示 ETH 余额

我们知道，ETH 是以太坊中的主要令牌，其他 20 令牌如戴、。两者都存在于以太坊上，你可以认为它们是 ETH 的一个分支。

有关 ERC-20 令牌的更多信息，可以查看这篇文章

[](https://www.investopedia.com/news/what-erc20-and-what-does-it-mean-ethereum/) [## 什么是 ERC-20，它对以太坊意味着什么？

### 流行的加密货币和区块链系统以太坊是基于代币的使用，代币可以买卖或…

www.investopedia.com](https://www.investopedia.com/news/what-erc20-and-what-does-it-mean-ethereum/) 

简而言之，ERC-20 代币在某些方面类似于比特币、莱特币和任何其他加密货币；ERC-20 代币是位于区块链的资产，具有价值，可以发送和接收。主要区别在于，ERC-20 代币不是在他们的区块链上运行，而是在以太坊网络上发行。

我们知道整个区块链就像一个巨大的不变的账本。如果要查询余额，首先要知道要查询哪个页面。我们没有页码或书签，但我们有一个钱包地址。根据地址，我们可以在分类账上查找，找到 ETH 余额。

使用 Web3 库很容易做到这一点，它看起来像:

```
func getETHBalance(wallet: Web3Wallet) throws -> String? { guard let walletAddress = EthereumAddress(wallet.address) else {
    throw Web3ServiceError.noAddress
  } web3.addKeystoreManager(try fetchKeyStoreManager(wallet: wallet)) let balance = try web3.eth.getBalance(address: walletAddress) return Web3.Utils.formatToEthereumUnits(
    balance,
    toUnits: .eth, 
    decimals: 3
  )
}
```

*   首先，输入是我们想要查询余额的钱包。
*   生成以太坊地址
*   获取包含钱包地址的密钥库，并将其添加到 web3 服务中
*   Web3 服务绑定到提供者，所以我们可以用它来查询余额
*   将余额格式化为 ETH 单位

# 显示戴和的平衡

正如我之前提到的，戴、或其他 20 代币在以太坊上发行，遵循 20 技术标准，可以通过智能合约执行。

关于智能合约，你可以查看[这篇文章](https://www.investopedia.com/terms/s/smart-contracts.asp#:~:text=A%20smart%20contract%20is%20a,a%20distributed%2C%20decentralized%20blockchain%20network.)了解更多信息。

也许这不是一个超级好的例子，但你可以这样想。这本名为以太坊的大账本有一个叫和戴的章节。

智能合同是指导你采取行动的指南。

首先，我们首先需要找到节来找到平衡。

```
func getERC20Balance(
  wallet: Web3Wallet, 
  token: ERC20Token
) throws -> String? {
  guard let walletAddress = EthereumAddress(wallet.address),
        let erc20ContractAddress = EthereumAddress(token.address, ignoreChecksum: true) else {
    throw Web3ServiceError.noAddress
  } guard let contract = web3.contract(Web3.Utils.erc20ABI, at: erc20ContractAddress, abiVersion: 2) else {
    throw Web3ServiceError.noContract
  } web3.addKeystoreManager(try fetchKeyStoreManager(wallet: wallet)) var options = TransactionOptions.defaultOptions options.from = walletAddress options.gasPrice = .automatic options.gasLimit = .automatic let tx = contract.read(
    TxMethod.balanceOf.rawValue,
    parameters: [walletAddress] as [AnyObject],
    extraData: Data(),
    transactionOptions: options
  ) let tokenBalance = try tx?.call() guard let balanceBigUInt = tokenBalance?[“0”] as? BigUInt else {
    throw Web3ServiceError.noBalance
  } return Web3.Utils.formatToEthereumUnits(
    balanceBigUInt, 
    toUnits: .eth, 
    decimals: 3
  )}
```

*   输入，即我们想要查询余额的钱包和我们想要查询的令牌
*   为钱包生成以太坊地址
*   为令牌生成以太坊地址，我们将使用它来查找智能合约
*   获取智能合同
*   获取包含钱包地址的密钥库，并将其添加到 web3 服务中
*   阅读合同，从钱包中取出余额
*   将其格式化为 eth 单位

让我们来看看，如果你想展示其他 ERC-20 代币，你也可以使用类似的方法。

本文可能还有一些不正确的地方，欢迎指正或与我讨论！

如果你觉得这篇文章有帮助，别忘了给我点掌声。

快乐编码，享受区块链技术🙂

> 如果你想联系我，请随时通过
> [Twitter](https://twitter.com/calvinchangtw) 或 [Linkedin](https://www.linkedin.com/in/calvin-chang-cc/) 联系我

干杯🍻

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [OKEx vs KuCoin](https://coincodecap.com/okex-kucoin) | [摄氏替代品](https://coincodecap.com/celsius-alternatives) | [如何购买 VeChain](https://coincodecap.com/buy-vechain)
*   [ProfitFarmers 点评](https://coincodecap.com/profitfarmers-review) | [如何使用 Cornix Trading Bot](https://coincodecap.com/cornix-trading-bot)
*   [如何匿名购买比特币](https://coincodecap.com/buy-bitcoin-anonymously) | [比特币现金钱包](https://coincodecap.com/bitcoin-cash-wallets)
*   [瓦济里克斯 NFT 评论](https://coincodecap.com/wazirx-nft-review)|[Bitsgap vs Pionex](https://coincodecap.com/bitsgap-vs-pionex)|[坦吉姆评论](https://coincodecap.com/tangem-wallet-review)
*   [如何使用 Solidity 在以太坊上创建 DApp？](https://coincodecap.com/create-a-dapp-on-ethereum-using-solidity)
*   [币安 vs FTX](https://coincodecap.com/binance-vs-ftx) | [最佳(SOL)索拉纳钱包](https://coincodecap.com/solana-wallets)
*   [如何在 Uniswap 上交换加密？](https://coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 审核](https://coincodecap.com/a-ads-review)
*   [加密货币储蓄账户](/coinmonks/cryptocurrency-savings-accounts-be3bc0feffbf) | [YoBit 评论](/coinmonks/yobit-review-175464162c62)