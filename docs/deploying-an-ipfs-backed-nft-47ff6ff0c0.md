# 部署 IPFS 支持的 NFT

> 原文：<https://medium.com/coinmonks/deploying-an-ipfs-backed-nft-47ff6ff0c0?source=collection_archive---------2----------------------->

有许多方法可以部署 NFTs。您可以在自己的服务器上托管资源、仅发布图像、附加属性等。这篇博文将介绍我所见过的最典型的项目设置，即:

*   上传到 IPFS 的图片
*   托管在 IPFS 上的 JSON 元数据
*   手工制作的合同(实实在在，废话)

# TL；速度三角形定位法(dead reckoning)

*   撰写可靠性合同
*   将图像上传到 Pinata
*   将 JSON 数据上传到 Pinata
*   将合同部署到 rinkeby
*   验证 rinkeby 上的合同
*   将您的`baseTokenURI`设置为`ipfs://<your json folder CID>/`
*   在 OpenSea 上列出你的项目:[https://testnets.opensea.io/get-listed](https://testnets.opensea.io/get-listed)

在开始之前，我已经将我的所有代码推送到这里的这个公共模板:[https://github.com/keyboard-clacker/ERC-721](https://github.com/keyboard-clacker/ERC-721)请随意使用它作为您的基本起点——除了像您的 IPFS CID 或 NFT name/ticker 这样的几行代码之外，您可能不需要修改这些代码，除非您想要在您的合同中添加功能。

# 写你的合同

这里真的没有你需要担心的特别的事情。我使用了一个典型的 OpenZeppelin 设置，这里基本上没有定制代码。如果你想要一个样板文件开始，这里你去:

我推荐使用 hardhat 来部署这个，因为你也可以很容易地使用它来验证你的合同(比我使用 truffle 时更容易)。为此，我使用了【https://etherscan.io/myapikey 】,这需要你创建一个以太扫描 API 密钥，但在这里可以非常容易和自由地做到这一点，只要你有一个以太扫描帐户:

至于你的安全帽配置，你也不需要什么特殊的东西。这里是我正在使用的，我真的只是在顶部添加了那个 etherscan 导入，它注册了`verify`命令，但基本上就是这样。

# 将图像上传到 Pinata

我建议这样做，并在随后的步骤中将这两个文件夹上传到 Pinata(或者您选择的 ipfs 门户)，因为您在部署合同时传递给合同构造函数的基本 URI 将是您的 JSON 文件夹的 ipfs URL，并且所有这些文件都将具有指向 IPFS 文件夹中的图像以及所有图像本身的`image`属性。所以你真的可以在任何时候这样做，你可以把你的基本 URI 设置成任何你想要的随机字符串，只是当你想在 opensea 上发布的时候，可能把它改成你的 JSON 文件夹 IPFSURI 或者什么都不会起作用。也就是说，让我们开始上传图片到 Pinata。

这一步看似简单。基本上你要做的是把你所有的图片放在一个文件夹里，然后把整个文件夹上传到 Pinata。您之所以要这样做，是因为当您将整个文件夹上传到 Pinata 时，它会创建一个 CID 或内容 ID 哈希，这是您的文件夹中所有文件的实际内容的哈希结果。这将让你做一些类似于`ipfs://<your cid>/1.png`的事情或者你想在那个文件夹中引用的任何文件。这对于 images 文件夹来说没什么用，因为 JSON 会直接指向每个文件，所以这真的没关系，但是最好保持一致。

回到上传到皮纳塔。下面是你想做的一些步骤:

*   把你所有的图片放在一个文件夹里。文件夹名称无关紧要，以后您可以随意命名。
*   点击这里进入 Pinata pin manager 仪表盘:[https://app.pinata.cloud/pinmanager](https://app.pinata.cloud/pinmanager)
*   点击上传按钮
*   选择“文件夹”选项
*   选择包含所有图像文件的文件夹
*   下一步，随便你怎么命名，真的无所谓。我选择了我的合同的名称，skewer case，然后在下一步我做了同样的事情，只是在它的末尾添加了`-json`,这样我就很容易知道哪个是哪个。另外，当按名称排序时，它们在列表中是有序的。

这就是上传图片到 Pinata。很容易，只是因为我对简洁缺乏信心而变得更难。

# 将 JSON 元数据上传到 Pinata

我发现网上对这一部分的描述/记录很差。也是将您的合约令牌与您的 IPFS 资产联系起来的基石。

为了理解这一步，你需要知道两件事。

1.  当 opensea 为一个令牌获取数据时，它会用给定的 ID 调用你的契约上的`tokenURI`。如果您在浏览器中导航到这个 URI，这最终应该是一个 JSON 对象，它遵守由 opensea 描述的元数据规范。如果是 IPFS·URI，你可能需要一个 chrome 扩展来查看。
2.  这个 JSON 文件没什么特别的——它只是一个遵守 opensea 元数据规范的文件，通过 IPFS 提供服务。OpenSea 负责 JSON 文件和图像本身的所有 IPFS 获取和所有花哨的东西(如果你遵循本指南，它还有一个 IPFS·URI)。

我想这里有一些自动生成这些 JSON 文件的方法，但是我喜欢在告诉计算机为我做之前手工做一些事情。必须为我们未来的机器人霸主建立同情心。

回到正题。首先，你要创建一个 JSON 文件，它的名字是*仅仅是*每个令牌的令牌号。所以你会有一个名为`0`的文件，然后是`1`、`2`、`3`，我想你明白了。无论有多少个令牌，每个令牌都需要一个 JSON 文件。你*不*需要`.json`文件扩展名的原因是，如果你尝试上传这些无扩展名文件中的一个，并导航到 IPFS URI，你会在响应的标题中看到 IPFS 实际上是自动声明内容类型，所以我们 gucci。

现在，每个令牌都有一个 JSON 文件，它们都在一个文件夹中。注意:这是一个不同于图像资源的文件夹。我想不一定是这样，但那样似乎更好。关注点的分离。从这里开始，您要将这个新文件夹上传到 Pinata，就像您上传 images 文件夹一样。简单的柠檬榨汁机，步骤完成。

这是入住的好时机。你怎么样，还好吗？如果你有任何问题，发推特给我@kyleholzinger，我总是会帮助有需要的开发人员。现在，您的 IPFS pin 管理器仪表板中应该有两个文件夹，一个包含您的所有图像资产，另一个包含每个资产的所有相应 JSON 文件。如果你有这个，你就有优势了。关于合同的事情。

# 将合同部署到 Rinkeby

将资产和 JSON 文件上传到 IPFS 后，确保在部署合同时将 baseURI 设置为`ipfs://<your JSON folder CID>/`。您不一定必须这么做，因为您可能在合同上写了一个`setBaseURI`方法(请这么做)，但是您知道他们说什么，测量两次，部署一次。吃了苦头才知道。

为了将您的合同部署到 rinkeby，请运行以下命令:

```
npx hardhat run scripts/run.js --network rinkeby
```

我通过别名`h`到`npx hardhat`让我的生活更轻松，但这是你的生活。此外，不要在运行此命令后清除您的终端历史记录。

# 验证 Rinkeby 上的合同

运行完`run.js`，应该已经吐槽出你新部署契约的契约地址了。要在 etherscan 上验证此合同，请运行以下命令:

```
npx hardhat verify --network rinkeby "<your contract address>" "ipfs://<your json CID>/"
```

这可能需要一秒钟的时间，但一两分钟后应该会显示一条成功消息。一旦通过验证，您就可以访问 [rinkeby.etherscan.io](http://rinkeby.etherscan.io) 并在该地址查看您验证过的合同及其所有漂亮的源代码。你喜欢看。

# 把你的基地设在 URI

你可能不需要这样做。只要确保你的`baseURI`被正确地设置为 IPFS 链接到你的 JSON 文件所在的文件夹。我再说一遍，JSON 文件，不是你的图像资产。每个 JSON 文件都应该链接到相应的图像资产 opensea 请求的顶级资产应该是每个令牌的 JSON 数据。

# 在 OpenSea 上列出你的项目

我假设你在这里使用 OpenSea，因为它是一种标准，但是做你想做的。这就是我正在做的。为了在 opensea 上列出部署到 rinkeby 的项目，您必须实际“导入”现有的令牌。它是相当隐蔽的，曾经在你点击“创建”时进入的页面中，但他们是贪婪的混蛋，想拿走你所有的钱，所以他们隐藏了所有的好东西。将自己定制的契约 ERC-721 令牌导入到 OpenSea 的页面在这里:[https://testnets.opensea.io/get-listed](https://testnets.opensea.io/get-listed)。你也可以使用这个页面列出 mainnet 上的一些东西，idk 为什么他们不知道你想发布到 rinkeby 实例，因为你在`testnets.opensea.io`上，但无论如何。

你所要做的就是给他们你的合同地址。

# 完成的

现在，您应该可以在您的收藏页面中看到您已经从合同中铸造的任何令牌(如果您这样做了的话)。他们可能还没有显示任何图像，我通常会通过点击右上角的“刷新”按钮来测试一下。如果你等了几分钟，它仍然没有显示任何东西，尝试用一个令牌 id 在你的合同上调用`tokenURI`，并导航到它给你的 URI(类似于`ipfs://lkasjdlkasjd/1`)。这个令牌应该是您的 JSON 文件，如果您导航到 JSON 中的`image`属性下指定的 URI，那么它应该是您希望在 opensea 上显示的图像。

差不多就是这样，如果有更简单的方法，请告诉我。恭喜你完成了你的合同，现在你必须做最难的部分，说服人们喜欢你的艺术。

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [加密套利](/coinmonks/crypto-arbitrage-guide-how-to-make-money-as-a-beginner-62bfe5c868f6)指南| [如何做空比特币](/coinmonks/how-to-short-bitcoin-568a2d0b4ae5)
*   [比特币基地 vs 瓦济克斯](https://coincodecap.com/coinbase-vs-wazirx) | [比特鲁点评](https://coincodecap.com/bitrue-review) | [波洛涅克斯 vs 比特克斯](https://coincodecap.com/poloniex-vs-bittrex)
*   [德国最佳加密交易所](https://coincodecap.com/crypto-exchanges-in-germany) | [Arbitrum:第二层解决方案](https://coincodecap.com/arbitrum)
*   [币安交易机器人](/coinmonks/binance-trading-bots-d0d57bb62c4c) | [OKEx 评论](/coinmonks/okex-review-6b369304110f) | [Atani 评论](https://coincodecap.com/atani-review)
*   [最佳加密交易信号电报](/coinmonks/best-crypto-signals-telegram-5785cdbc4b2b) | [MoonXBT 评论](/coinmonks/moonxbt-review-6e4ab26d037)
*   如何在 Bitbns 上购买柴犬(SHIB)币？ | [买弗洛基](https://coincodecap.com/buy-floki-inu-token)
*   [CoinFLEX 评论](https://coincodecap.com/coinflex-review) | [AEX 交易所评论](https://coincodecap.com/aex-exchange-review) | [UPbit 评论](https://coincodecap.com/upbit-review)
*   [十大最佳加密货币博客](https://coincodecap.com/best-cryptocurrency-blogs) | [YouHodler 评论](https://coincodecap.com/youhodler-review)
*   [AscendEx 保证金交易](https://coincodecap.com/ascendex-margin-trading) | [Bitfinex 赌注](https://coincodecap.com/bitfinex-staking)
*   [最好的卡达诺钱包](https://coincodecap.com/best-cardano-wallets) | [Bingbon 副本交易](https://coincodecap.com/bingbon-copy-trading)