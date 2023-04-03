# 使用 Synpress 测试 e2e 登录到具有元掩码的 dApp

> 原文：<https://medium.com/coinmonks/test-e2e-login-to-dapp-with-metamask-with-synpress-5248dd1f17c1?source=collection_archive---------3----------------------->

## 包括使用 Synpress 和 Cypress 使用 Metamask 对 Web3 dApp 登录进行端到端测试的工作示例

![](img/a80e486284ef244dc3d1cc89dbe6ded0.png)

Photo by [Shubham Dhage](https://unsplash.com/@theshubhamdhage?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 今日话题

端到端测试(e2e)用于前端开发，允许应用程序的可伸缩性。编写 e2e 测试的一个非常流行的工具是 [Cypress](https://www.cypress.io/) 。然而，如果你想为 web3 dApps 做一些 e2e 测试，Cypress 本身不能帮助你。Cypress 单独不能测试 metamask 相互作用。因此，我们需要别的东西。我们要用 [Synpress](https://github.com/Synthetixio/synpress) 。

# 什么是 Synpress？

Synpress 是 Cypress 的一个包装器，并在[木偶师](https://github.com/puppeteer/puppeteer)的帮助下对其进行了扩展。产生允许您与元掩码交互的自定义命令。它是如何工作的？它运行一个全局 cypress `before`例程，安装一个元掩码插件，并对其进行配置。

*   通行证 metmask 欢迎页面
*   进口钱包
*   更改网络(默认为`kovan`)或创建自定义网络并对其进行更改(取决于您的设置)
*   切换回 Cypress window 并开始测试

(您可以稍后在您的机器上观察测试运行程序，在稍后运行 cypress 测试时创建一个元掩码概要文件)。

所以请记住:Synpress 允许我们测试 metamask 登录、认证以及与智能合约的交互。但是在本文中，我们只关注登录部分。我们将通过 6 个步骤来实现这一目标。

# 这篇文章是给谁看的？

这篇文章主要针对初学者，因为它删除了第一次使用 Synpress 和 Cypress 时极其复杂的细节。对于初学者来说，用 Cypress 设置 Synpress 是相当具有挑战性的(我自己也经历过)。没有适合初学者的资源，仅仅查阅 Synpress 库对你没有任何帮助，因为你可能无法快速解决复杂的问题。因此，我将介绍如何用最简单的材料为自己的 web3 dApp 实现端到端测试。

如果你是 e2e 测试界的新手，我建议你在继续之前先完成 cypress 的[入门](https://docs.cypress.io/guides/getting-started/installing-cypress)部分。不会花你太长时间的。在从 cypress 入门和本教程之后，我认为你可以很快开始使用 web3 dApp e2e 测试，因为你已经有了一个很好的基础，可以从这个基础上提高。

# 步骤 1 —创建项目并添加依赖项

```
cd /your/project/pathnpm install cypress --save-devnpm i @synthetixio/synpressnpm install env-cmd
```

## 将脚本添加到 package.json

```
"scripts": {
    "test": "env-cmd -f .env npx synpress run -cf synpress.json --config supportFile='cypress/support/index.js'",
```

# 步骤 2 —创建文件夹和文件

在根目录下添加一个名为`tests`的文件夹

在这个`tests`文件夹中创建两个文件夹，一个叫做`integration`(或者你喜欢的`e2e`)，另一个叫做`support`

# 支持文件夹:

将以下两个文件添加到`support`文件夹中。

**command.js**

对于本教程，您可以将其留空，但是它允许您编写自定义测试函数。我只是想提到这一点，以便您了解可能的架构(可能是为了未来的项目)。

```
import "@testing-library/cypress/add-commands";// your custom code here
```

然后将 **index.js** 添加到`support`文件夹，内容如下:

```
import './commands'
import "@synthetixio/synpress/support";
```

注意:如果你不把这些行添加到`index.js`中，你会得到一个错误，比如说

`TypeError: cy.acceptMetamaskAccess is not a function`

这个`index.js`允许 Cypress 使用 Synpress 实现的功能。

# 集成(或 e2e)文件夹:

在`integration`中添加另一个名为`specs`的文件夹。在`specs`内添加一个`login.spec.js`文件。我们将在步骤 4 中添加测试。

# 步骤 3——编写一个简单的测试

我们在`login.spec.js`中编写测试

如果你想知道 synpress 提供了哪些功能，请查看:[https://github . com/synthetixio/synpress/blob/master/support/index . d . ts](https://github.com/synthetixio/synpress/blob/master/support/index.d.ts)

查看下面的代码。我想象它只有一个“连接钱包”按钮，只有 metamask 弹出。

# 步骤 Synpress 的配置

现在，我们几乎涵盖了所有步骤，我们正在接近终点线。还剩两步。让我们继续 synpress 的配置。配置在`synpress.json`文件中指定。我们这样做:

1.  在根目录下创建一个`synpress.json`文件
2.  添加到文件中

我想指出几件事。请确保将“baseUrl”设置为您的项目。如果您正在测试您的本地开发服务器，您可能需要

`"baseUrl": "http://localhost:3000"`

此外，确保键`"integrationFolder"`的值指向您实际的`integrations`或`e2e`文件夹，否则您将收到类似如下的错误:

```
Can't run because no spec files were found.We searched for specs inside of this folder:
<some path>
```

还要注意键-值对:`"supportFile": "tests/support/index.js"`确保它指向`index.js`文件，否则会收到

`Your supportFile is missing or invalid`

# 第 5 步——创建。环境文件

运行测试前的最后一步。我们需要配置`.env`文件。它将用于在 synpress/cypress `before`例程中配置元掩码。

通过`NETWORK_NAME`变量选择网络。我们可以在`mainnet`、`ropsten`、`kovan`、`rinkeby`、`goerli`和`localhost`中选择。然后加一个例句。

```
NETWORK_NAME=kovan
SECRET_WORDS="test, test, test, test, test, test, test, test, test, test, test, junk"
```

还有其他属性你可以配置，再看一下 [synpress](https://github.com/Synthetixio/synpress) repo。

# 步骤 6 —运行测试

由于我们向我们的`package.json`添加了脚本，我们现在可以很容易地用

`npm run test`代表`env-cmd -f .env npx synpress run -cf synpress.json`(见步骤 1)

# 结论

本教程指导你完成了第一次 synpress 测试，并有望引导你更频繁地测试你的 web3 dApps。尝试与区块链进行更复杂的交互，巩固您在本教程中获得的知识。例如，尝试创建一个智能合约，您可以将钱包中的一些 eth 存入智能合约，然后编写您的 synpress 测试。让我在推特上知道你做了什么。

回购:[https://github.com/yvesbou/synpress_metamask_login](https://github.com/yvesbou/synpress_metamask_login)

https://github.com/Synthetixio/synpress

# 关于 Dappify

《Web3 的平方空间》。我们让数百万人能够以分散的方式建立品牌，分享他们的故事，并通过美丽的在线展示与他们的客户进行交易。构建者可以从专注于 web3 用例的模板中设计和启动项目，而无需编写一行代码。Dappify 降低了构建者进入 web3 的门槛，通过预构建的模板将区块链和 UX 的复杂性抽象化，他们可以根据自己的需求进行调整，为用户提供超友好的最终体验。

作者:[https://twitter.com/boutellier_yves](https://twitter.com/boutellier_yves)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Bookmap 评论](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [库币评论](https://coincodecap.com/kucoin-review)