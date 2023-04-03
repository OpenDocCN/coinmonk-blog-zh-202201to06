# 在安全帽中测试的技巧

> 原文：<https://medium.com/coinmonks/tips-for-testing-in-hardhat-c59e03837c92?source=collection_archive---------11----------------------->

## 我如何测试和调试我的智能合约。

![](img/ffc8ee0c788e2c8591ee3cdbeb88a0ee.png)

Image by @whoisdenilo on Unsplash.com

# 介绍

本文将是[官方安全帽文档](https://hardhat.org/getting-started/)的延伸。如果你还没有，我强烈建议你先去那里看看。话虽如此，我们还是直奔主题吧！

# 它

## 应该使用 console.log()

如果你做过任何类型的编程，你就会知道在代码执行过程中读取变量是多么的有用。我个人喜欢用这种方法，尤其是当我试图定位错误的时候。但是在你的智能合同中使用这个有点棘手。首先，您必须通过在您的 Solidity 代码中添加以下行来导入 hardhat 控制台:

```
import "hardhat/console.sol";
```

然后创建一个 Hardhat 节点来运行您的代码。您可以使用以下终端命令来完成此操作:

```
npx hardhat node
```

如果需要，你也可以[分叉](https://hardhat.org/hardhat-network/guides/mainnet-forking.html) mainnet 或 testnet。现在，当您运行您的测试/代码(在不同的终端窗口中)时，您将能够在节点终端中看到您 *console.logged* 的值！

另一种方法是使用一个名为*的服务，它将允许您查看来自已部署合同的 *console.logs* 。这种方法比较繁琐，但是允许您在生产中进行测试。*

## 应该使用。只是为了隔离测试

有时候你*。只有*想在你数百万的套件中运行某些测试。可以通过在**描述**或 **it** 命令后添加`.only`来实现，如下所示:

```
describe.only("Blah blah blah",...);
```

Hardhat 将只运行那个特定的测试，忽略所有其他的测试(和文件)。可以*。只有*多次测试，但有某些规则我还没来得及搞清楚。完成后，记得移除修饰符。

## 应该组织测试

如果你有很多测试(安全在加密中很重要，或者他们这么说)，那么*。只有*的方法可能还不够。幸运的是，Hardhat 有一个选项允许您指定测试的位置。您可以将您的测试分组到文件夹中，并在配置文件中更改指定的文件夹[路径，只运行该文件夹中的测试。](https://hardhat.org/config/)

# 结束语

您可能已经注意到，加密领域的文档从高度受限到根本不存在。因此，即使作为一个非作家，我也觉得有必要接过衣钵，为这个巨大的档案空白照亮一些光明。希望读者会发现我的文章很有帮助。我是这方面的新手，所以非常欢迎评论。编码快乐！

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

## 也阅读

[](https://coincodecap.com/blockfi-review) [## BlockFi 评论:2022 年的利弊和利率

### 今天，我们提出了一个全面的 BlockFi 评论，这是一个成立于 2017 年的加密贷款平台，拥有其…

coincodecap.com](https://coincodecap.com/blockfi-review) [](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) [## 如何在印度购买比特币？2021 年购买比特币的 7 款最佳应用[手机版]

### 如何使用移动应用程序购买比特币印度

medium.com](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) [](/coinmonks/best-crypto-tax-tool-for-my-money-72d4b430816b) [## 加密税务软件——五大最佳比特币税务计算器[2021]

### 不管你是刚接触加密还是已经在这个领域呆了一段时间，你都需要交税。

medium.com](/coinmonks/best-crypto-tax-tool-for-my-money-72d4b430816b)