# 使用 PHP 和 Coinex.net API 的简单加密支付系统

> 原文：<https://medium.com/coinmonks/simple-crypto-payment-system-using-php-and-coinex-net-api-45d38cf2131?source=collection_archive---------6----------------------->

嘿嘿嘿！

0xlive 在这里😃

在本教程中，我们将使用 php 和 coiex.net API 开发一个简单的加密支付系统

**web3.js 安装**

要在终端类型中安装 web3.js:

```
npm install web3
```

您也可以安装纱线:

```
yarn add web3
```

如果您想在不安装任何东西的情况下使用 web3.js，请将其导入浏览器:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.7.3/web3.min.js" integrity="sha512-Ws+qbaGHSFw2Zc1e7XRpvW+kySrhmPLFYTyQ95mxAkss0sshj6ObdNP3HDWcwTs8zBJ60KpynKZywk0R8tG1GA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```

**项目设置**

让我们创建一个名为 payment.html 的文件

```
<!DOCTYPE html>
<html>
<head>
<title>Payment Gateway</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.7.3/web3.min.js" integrity="sha512-Ws+qbaGHSFw2Zc1e7XRpvW+kySrhmPLFYTyQ95mxAkss0sshj6ObdNP3HDWcwTs8zBJ60KpynKZywk0R8tG1GA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<<link rel="stylesheet" href="style.css">
</head>
<body>

     <section id="payment" class="payment">
<form class="credit-card">
  <div class="form-header">
    <h4 class="title">Payment</h4>
  </div>
  <div class="form-body">
    <input class="card-number" id="Amount" type="number" placeholder="Amount">
    <div class="date-field">
      </div>
    <button class="pay-button" type="submit"> <a href="#">Buy</a></button>
        <div id="status"></div>
  </div>
</form>
</section>

</body>
</html>
```

我们已经创建了一个付款形式的部分，现在我们想使用 metamask + JS 进行交易

```
window.addEventListener('load', async () => {
      if (window.ethereum) {
        window.web3 = new Web3(ethereum);
        try {
          await ethereum.eth_requestAccounts;
          initPayButton()
        } catch (err) {
          $('#status').html('User denied account access', err)
        }
      } else if (window.web3) {
        window.web3 = new Web3(web3.currentProvider)
        initPayButton()
      } else {
        $('#status').html('No Metamask (or other Web3 Provider) installed')
      }
    })
```

首先，我们要求许可，如果用户接受，我们将进一步，如果没有状态标签将显示“`No Metamask (or other Web3 Provider) installed".`

**付款**

我们从输入中获取值，然后存储到支付地址。如果交易成功，它会将数据传递给 pay.php，否则会显示错误消息。

```
const initPayButton = () => {
      $('.pay-button').click(() => {
        const paymentAddress = 'YOUR ADDRESS'
        const amountEth = document.getElementById("Amount").value;

        web3.eth.sendTransaction({
          to: paymentAddress,
          value: web3.toWei(amountEth, 'ether')
        }, function(err, transactionHash) {
    if (err) { 
        console.log('Payment failed', err)
            $('#status').html('Payment failed')
    } else {

 document.getElementById("status").innerHTML = transactionHash;
            $('#status').html('Payment successful')
 var httpc = new XMLHttpRequest(); 
    var url = "pay.php";
    httpc.open("POST", url, true);

    httpc.onreadystatechange = function() {.
        if(httpc.readyState == 4 && httpc.status == 200) {
            alert(httpc.responseText);
        }
    };
    httpc.send(transactionHash);
      }})
```

**Coinex.net API**

要与 coinex.net api 服务交互，我们需要 API 密钥！

打开[https://testnet.coinex.net/register](https://testnet.coinex.net/register)

![](img/cd328f820399d1661d66d9e343aa58fb.png)

coinex.net

注册后，转到“api 密钥”

注意:不要和任何人分享你的 api 密匙！

**Pay.php**

让我们配置我们的脚本:

```
<?php

$tx= $_POST['Amount'];

$curl = curl_init();
curl_setopt_array($curl, [
	CURLOPT_URL => "https://www.coinex.net/api/v1/transactions/".$tx,
	CURLOPT_RETURNTRANSFER => true,
	CURLOPT_FOLLOWLOCATION => true,
	CURLOPT_ENCODING => "",
	CURLOPT_MAXREDIRS => 10,
	CURLOPT_TIMEOUT => 30,
	CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
	CURLOPT_CUSTOMREQUEST => "GET",
	CURLOPT_HTTPHEADER => [
		"apikey: YOUR KEY",
	],
]);

$response = curl_exec($curl);
$err = curl_error($curl);
curl_close($curl);
$data = json_decode($response, true);

if ($err) {
	echo "cURL Error #:" . $err;
} else {
	if  (strlen($data["data"]["error"]) == 0) {
            echo "successful";
    else{
        echo"a mistake was made";
}}}
?>
```

我们首先从输入中获得数量。然后我们去请求 api 服务。

我们从 api 获取数据并解码成 json 格式。

如果事务的错误部分有任何数据，则表示事务失败，如果没有任何数据，则表示事务成功！

祝贺🥳

我们已经使用 web3.js、metamask、coinex.net API 服务和 php 为 csc 创建了一个简单的加密支付

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [3 商业评论](/coinmonks/3commas-review-an-excellent-crypto-trading-bot-2020-1313a58bec92) | [Pionex 评论](https://coincodecap.com/pionex-review-exchange-with-crypto-trading-bot) | [Coinrule 评论](/coinmonks/coinrule-review-2021-a-beginner-friendly-crypto-trading-bot-daf0504848ba)
*   [莱杰 vs n rave](/coinmonks/ledger-vs-ngrave-zero-7e40f0c1d694)|[莱杰 nano s vs x](/coinmonks/ledger-nano-s-vs-x-battery-hardware-price-storage-59a6663fe3b0) | [币安评论](/coinmonks/binance-review-ee10d3bf3b6e)
*   [Bybit 交易所评论](/coinmonks/bybit-exchange-review-dbd570019b71) | [Bityard 评论](https://coincodecap.com/bityard-reivew) | [Jet-Bot 评论](https://coincodecap.com/jet-bot-review)
*   [3 commas vs crypto hopper](/coinmonks/3commas-vs-pionex-vs-cryptohopper-best-crypto-bot-6a98d2baa203)|[赚取加密利息](/coinmonks/earn-crypto-interest-b10b810fdda3)
*   最好的比特币[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [BitBox02 回顾](/coinmonks/bitbox02-review-your-swiss-bitcoin-hardware-wallet-c36c88fff29)
*   [block fi vs Celsius](/coinmonks/blockfi-vs-celsius-vs-hodlnaut-8a1cc8c26630)|[Hodlnaut 审核](/coinmonks/hodlnaut-review-best-way-to-hodl-is-to-earn-interest-on-your-bitcoin-6658a8c19edf) | [KuCoin 审核](https://coincodecap.com/kucoin-review)