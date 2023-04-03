# 与 Hardhat 建立智能合同(您需要知道的一切)

> 原文：<https://medium.com/coinmonks/hardhat-development-everything-you-need-to-know-4cc93e309377?source=collection_archive---------21----------------------->

## 安全帽开发环境介绍

#康普西#区块链#以太坊#坚固

![](img/09f8fd321a33e59285cb4b2efdb4fb0f.png)

Photo by [Michael Dziedzic](https://unsplash.com/@lazycreekimages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

Hardhat 是一个开发环境来**编译**、**部署**、**测试**、&、**调试**你的**以太坊程序**。这是通过 **Hardhat Runner** 完成的，它是一个 **CLI 命令工具**，作为所有 Hardhat 特性和功能的可扩展**任务运行器**。

Hardhat 通过项目中的**本地安装**使用。

要安装它，您需要创建一个 npm 项目，方法是在 CLI 中键入`npm init`，然后键入`npm install --save-dev hardhat`。

```
npm install --save-dev hardhat
```

一旦完成，运行`npx hardhat`创建一个**准系统安全帽环境**。所有与 hardhat 进行的交互都必须使用该命令，后跟所需的可执行任务&选项。

```
npx hardhat compile
```

最后，从控制台中选择“创建一个示例项目”选项。这将建立一个项目并安装`[@nomiclabs/hardhat-ethers](http://twitter.com/nomiclabs/hardhat-ethers)`、`[@nomiclabs/hardhat-waffle](http://twitter.com/nomiclabs/hardhat-waffle)`和其他必要的软件包。

# 收集

任务`compile`将编译一个安全帽项目。

```
npx hardhat compile
```

在初始编译之后，如果没有对项目进行可观察到的改变，hardhat 将不会编译。如果需要，可以通过添加`--force`选项来强制编译。或者，可以使用`clean`任务来清除缓存并删除所有工件。

# 配置

在`module.export`包内的`hardhat.config.js`中进行配置更改。该模块中可用的字段有`defaultNetwork`、`network`、`solidity`、`paths`和`mocha`。

*以下是使用外部节点的通用安全帽配置:*

# 网络

Hardhat 提供了内置的本地**以太坊网络**。

默认情况下，启动时实例会自动启动。

`node`任务为 Hardhat 网络公开了一个`JSON-RPC`接口，使其可以被外部客户端访问。

```
npx hardhat node
```

**也可以使用外部 JSON-RPC** (远程过程调用)网络，将 hardhat 开发环境扩展到**test net**和**main net**。然而，这些外部网络必须在`hardhat.config.js`文件中的`network`字段下进行配置。

这里是一个基本的网络配置:

一旦配置完成，如果选项可用，任务可以显式声明一个带`--network`的网络。如果所需网络是本地托管的，则应使用`--network localhost`选项。

# 剧本

Hardhat 支持 **Javascript** 或**类型脚本**中的脚本。

脚本可用于编写**部署**、**测试**或**维护**的代码。

`run <script.js>`任务用于运行依赖于 hardhat 的脚本，而独立脚本则通过`node <script.js>`运行。根据前一种方法运行的脚本可以访问 Hardhat 的全局范围，而不能访问的脚本必须显式声明依赖关系。

```
npx hardhat run script.js
```

*下面是一个基本的部署脚本:*

# 测试

Hardhat 支持用**Waffle**&**ethers . js**进行测试。

任务将执行文件路径中的所有测试。

```
npx hardhat test
```

下面是一个基本的文本脚本:

# 任务

**任务**是安全帽内的基本工作单元；所有的 hardhat 进程都是通过任务来执行的，这使得默认的和定制的例程可以很容易地执行。

`task(…)`功能创建任务。它既可以在其参数内定义整个任务，也可以链接函数来逐步构建其各个部分。

>✏️ **注意:**任务应该在`hardhat.config.js`内声明

构建器模式方法从`task(name, description)`函数开始，由`addParam(name, description)` & `setAction(async (taskArgs) => {…})`链接。

complete params 方法使用任务函数的扩展版本:`task(name, description, async function (taskArguments, hre, runSuper) {…})`。与前一种方法不同，在任务被命令调用之前，参数是未知的。这允许更多的灵活性，但是更容易出错。

*下面是一个用构建器方法做的任务:*

`subtask(…)`功能的工作方式几乎和`task(…)`完全一样。唯一的区别是它不记录它的帮助消息。这使得子任务成为构建复合任务的良好解决方案，而不会造成控制台输出拥挤。

`run()`函数用于运行任务和子任务。

```
hre.run("balance", { account: "0x89Df..."});
```

# 安慰

Hardhat 支持**日志**内置、交互式 **Javascript 控制台**。

所有 hardhat 全局范围的成员都可以在控制台中使用。

`console`任务将创建一个控制台实例。

```
npx hardhat console
```

日志记录是通过`console.log()`函数完成的，可以从 Hardhat 环境中的任何地方发出:合同、脚本、测试、配置等等…

# 就是这样！

正如我在我的页面上所说的，这些是我个人笔记本上的笔记。如果有任何明显的错误，请随时留下评论，以便我可以修复它们。还有，如果有你想从我这里看到的内容，请告诉我！

## 资源

安全帽的文档:[https://hardhat.org/getting-started/](https://hardhat.org/getting-started/)

> 交易新手？尝试[加密交易机器人](/coinmonks/crypto-trading-bot-c2ffce8acb2a)或[复制交易](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c)