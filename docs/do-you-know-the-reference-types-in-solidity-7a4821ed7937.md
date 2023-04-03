# 你知道 SOLIDITY 中的引用类型吗？

> 原文：<https://medium.com/coinmonks/do-you-know-the-reference-types-in-solidity-7a4821ed7937?source=collection_archive---------9----------------------->

![](img/ea41c8d0ab60189b1dd7e2aa5ba97aa8.png)

正如我们在我的第二篇文章中了解到的，Solidity 有不同的数据类型，分为两类，即:引用类型和值类型。在这篇文章中，我们将集中讨论 solidity 中的引用类型部分。

# **参考类型**

参考类型顾名思义即*所指。R* 引用类型不直接将数据存储到变量中，而是存储数据的位置(从该位置引用数据)。如果使用引用类型，则必须始终显式提供存储该类型的数据区域:

*   内存——其生存期仅限于外部函数调用，
*   存储——存储状态变量的位置，其生命期限于合同的生命期，
*   包含函数参数的特殊数据位置。

在这种情况下，使用引用类型，两个不同的变量可以引用同一个位置；一个变量的任何变化都会影响到另一个变量；因此，值类型需要非常小心地处理。值类型和引用类型之间的显著区别是数据位置。

## 数据位置和分配行为

数据位置不仅与数据的持久性相关，还与赋值的语义相关:

*   在`storage`和`memory`(或来自`calldata`)之间的分配总是创建一个独立的副本。
*   从`memory`到`memory`的分配仅创建参考。这意味着对一个内存变量的更改在引用相同数据的所有其他内存变量中也是可见的。
*   从`storage`到本地存储变量的赋值也只分配一个引用。
*   所有其他分配给`storage`的任务总是复制。这种情况的例子是对状态变量或存储结构类型的局部变量成员的赋值，即使局部变量本身只是一个引用。

引用类型由以下内容组成:

*   排列
*   结构
*   绘图

> 数组和结构有额外的数据位置，指定数据(变量值)应该存储在哪里。

## **数组**

数组是一组相同数据类型的元素，其中每个元素都有一个称为 index 的特定位置。Solidity 中的数组可以是动态的(即它可以被修改或改变)或固定大小的(即它是固定的/不能被改变)。

**固定大小数组**

固定大小数组在声明时具有预定义的大小。例如，一个固定大小为 5 且元素类型为 uint 的数组被写成，

```
uint[5] arrayName;
```

当我们声明一个数组时，它不会初始化；我们必须用一个新的关键字来初始化它。然而，在 Solidity 中，你不能对固定大小的数组使用 new 关键字；相反，它们可以内联初始化。

```
uint[5] marks  = [uint(50), 60,70,80,90];
```

**动态数组**

动态数组在声明时没有预定义的大小；大小将在运行时确定。

```
uint[] arrayName;
```

可以用“new”关键字或 inline 初始化动态数组。

```
uint[5] mathMarks = [uint(50), 60,70,80,90];**int**[] scienceMarks = **new** **int**[](5);
```

## 结构

结构允许您将数据分组在一起。Solidity 提供了一种以结构形式定义新类型的方法，如下例所示:

该协定不提供结构协定的全部功能，但它包含理解结构所必需的基本概念。结构类型可以在映射和数组中使用，它们本身可以包含映射和数组。

尽管结构本身可以是映射成员的值类型，或者可以包含其类型的动态大小数组，但结构不可能包含其自身类型的成员。这个限制是必要的，因为结构的大小必须是有限的。

## 绘图

映射就像 python 中的字典，它允许高效的查找。比如:我们来看看 Rachael 是否包含在下面的数组中；

```
[Serah, Esther, Eve];
[Serah=true, Esther=true, Eve=true]; //which means that rachael is not included.
```

在数组中，我们必须经过 3 次查找，但是在映射中，我们只需要一次查找就可以得到想要的结果。

映射类型使用语法`mapping(KeyType => ValueType)`，映射类型的变量使用语法`mapping(KeyType => ValueType) VariableName`声明。`KeyType`可以是任何内置值类型、`bytes`、`string`，或者任何契约或枚举类型。

在下面的例子中，`Mapping`契约定义了一个公共`balances`映射，键类型为`address`，值类型为`uint`，将以太坊地址映射到一个无符号整数值。

**感谢阅读！**

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [最佳免费加密信号](https://coincodecap.com/free-crypto-signals) | [YoBit 评论](/coinmonks/yobit-review-175464162c62) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [OKEx 回顾](/coinmonks/okex-review-6b369304110f) | [Kucoin 交易机器人](/coinmonks/kucoin-trading-bot-automate-your-trades-8cf0ca2138e0) | [期货交易机器人](/coinmonks/futures-trading-bots-5a282ccee3f5)
*   [AscendEx Staking](https://coincodecap.com/ascendex-staking)|[Bot Ocean Review](https://coincodecap.com/bot-ocean-review)|[最佳比特币钱包](https://coincodecap.com/bitcoin-wallets-india)
*   [霍比审核](https://coincodecap.com/huobi-review) | [OKEx 保证金交易](https://coincodecap.com/okex-margin-trading) | [期货交易](https://coincodecap.com/futures-trading)
*   [比特币基地跑马圈地](https://coincodecap.com/coinbase-staking) | [Hotbit 评论](/coinmonks/hotbit-review-cd5bec41dafb) | [KuCoin 评论](https://coincodecap.com/kucoin-review)