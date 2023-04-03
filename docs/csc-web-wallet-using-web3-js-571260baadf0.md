# 使用 Web3.js 的 CSC 网络钱包

> 原文：<https://medium.com/coinmonks/csc-web-wallet-using-web3-js-571260baadf0?source=collection_archive---------39----------------------->

嘿嘿嘿！

0xlive 在这里😃

在本教程中，我们将使用 web3.js 开发简单的网络钱包

**web3.js**

web3.js 是一组用 javascript 实现的加密和网络工具

**安装**

要在终端类型中安装 web3.js:

```
npm install web3
```

您可以使用 yarn 安装 web3.js:

```
yarn add web3
```

我们可以将 web3.js 导入 html:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.7.3/web3.min.js"></script>
```

**设置项目**

创建 index.html，把这个放进去:

```
<!DOCTYPE html>
<head>
<meta charset="utf-8">
<title>CSC Web Wallet</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.7.3/web3.min.js"></script>
</head>

<body>

</body>
</html>
```

我们已经创建了一个 html 文件并导入了 pure web3.js。

**钱包制作**

首先我们需要设置提供者:

```
const w3 = new Web3("https://testnet-rpc.coinex.net");
```

然后创建一个钱包:

```
const account = w3.eth.accounts.create();
```

它将为我们生成一个随机钱包，其中包含钱包地址和私钥。您可以在浏览器控制台中检查它们:

```
console.log(account)
```

注意:当你刷新页面时，web3.js 会生成新的随机钱包。因此，如果我们希望存储钱包以备将来使用，我们需要将其存储在浏览器本地存储中:

```
localStorage.setItem("address", account.address);
localStorage.setItem("privateKey", account.privateKey);
```

现在让我们在页面中显示钱包地址:

```
<p>Your Address  is:</p>
<p id="address"></p>

//js 
document.getElementById("address").innerHTML = localStorage.getItem("address");
```

一切都好！让我们做个交易

**进行交易**

我们需要以标准格式进行交易。

一笔正常的交易有以下内容:

1-收件人地址

2-随机数

3-金额

4-气体

5-私钥(它不是交易的一部分，但我们需要它来签署交易)

让我们开始吧:

```
const transaction = {
     'to': 'recipient address', // recipient's address
     'value': 1,
     'gas': 30000,
     'maxPriorityFeePerGas': 1000000108,
     'nonce': nonce,
     // optional data field to send message or execute smart contract
    };
```

要获得 nonce，我们可以这样做:

```
const nonce = await w3.eth.getTransactionCount(localStorage.getItem("address"), 'latest');
```

现在是签署交易的时候了:

```
const signedTx = await w3.eth.accounts.signTransaction(transaction, localStorage.setItem("privateKey", account.privateKey));

    w3.eth.sendSignedTransaction(signedTx.rawTransaction, function(error, hash) {
    if (!error) {
      console.log("TX Hash is ", hash);
    } else {
      console.log("a mistake was made", error)
    }
   });
```

耶！我们做到了。我们需要在交易后使用 getBalance 检查余额:

```
w3.eth.getBalance(localStorage.getItem("address"), function(err, result) {
  if (err) {
    console.log(err)
  } else {
    console.log(web3.utils.fromWei(result, "ether") + " CSC")
  }
})
```

祝贺🥳

我们使用 web3.js 创建了一个非托管的

注意:出于安全原因，我们必须加密私钥。我们可以使用 AES-256 加密来做到这一点。但是怎么做呢？这是你探索更多的责任😉

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [如何在 Uniswap 上交换加密？](https://coincodecap.com/swap-crypto-on-uniswap) | [A-Ads 审查](https://coincodecap.com/a-ads-review)
*   [WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [本地比特币评论](/coinmonks/localbitcoins-review-6cc001c6ed56) | [加密货币储蓄账户](https://coincodecap.com/cryptocurrency-savings-accounts)
*   [什么是融资融券交易](https://coincodecap.com/margin-trading) | [美元成本平均法](https://coincodecap.com/dca)
*   [拥护卡审核](https://coincodecap.com/uphold-card-review) | [信任钱包 vs MetaMask](https://coincodecap.com/trust-wallet-vs-metamask)
*   [Exness 评测](https://coincodecap.com/exness-review)|[moon xbt Vs bit get Vs Bingbon](https://coincodecap.com/bingbon-vs-bitget-vs-moonxbt)