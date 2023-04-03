# 理解 SOLIDITY 中的值类型

> 原文：<https://medium.com/coinmonks/understanding-value-types-in-solidity-5caa1af846ef?source=collection_archive---------26----------------------->

![](img/5f909edeb4af46f9c10c78072dd8ac21.png)

在我进一步讨论可靠性中的各种价值类型之前，让我们回顾一下什么是可靠性，以便更好地理解。

**什么是扎实？**

Solidity 是一种面向对象的编程语言，有助于在各种区块链平台上实现智能合约，尤其是以太坊。Solidity 是一种静态类型的语言，这意味着你必须在编译时指定每个变量(状态和局部变量)。

**什么是智能合约？**

智能合约是在以太坊区块链上运行的程序。它们是储存在区块链上的计算机程序，可以让我们将传统合同转换成数字合同。智能合约非常符合逻辑，遵循 if this then that 结构。

智能合约是以太坊账户的一种。这意味着他们有一个平衡，他们可以通过网络发送交易。然而，它们不受用户控制，相反，它们被部署到网络上并按程序运行。然后，用户帐户可以通过提交执行智能合约上定义的功能的交易来与智能合约进行交互。智能合同可以像常规合同一样定义规则，并通过代码自动执行这些规则。默认情况下，不能删除智能合同，并且与智能合同的交互是不可逆的。

坚固性提供了几种基本类型，当它们组合在一起时，就形成了复杂类型。Solidity 有不同的数据类型。这些数据类型分为两类，即引用类型和值类型。在本文中，我们将关注值类型。那么，让我们看看什么是值类型。

# **值类型**

以下类型被称为值类型，因为这些类型的变量总是通过值传递，也就是说，当它们用作函数参数或用于赋值时，总是被复制。

## **布尔型**

布尔值 **s** 由 **boo** l 表示，该数据类型只接受两个值**真**或**假**。

适用于 bool 类型的运算符有:

*   *！(逻辑否定)*
*   *l&(逻辑连词即 and)*
*   *l ||(逻辑析取即或)*
*   *l ==(等式)*
*   *l！=(不等式)*

布尔运算符占用 1 个字节的存储空间。逻辑“**和“**以及逻辑**或“**运算符遵循与其他编程语言相同的短路规则。例如，在表达式 var(x) || var(y)中，如果 var(x)的计算结果为 true，则不会计算 var(y)。

## **整数**

不同大小的整数有两种主要的实性类型:

*   int—有符号整数。
*   uint —无符号整数。

**uint8** 到 **uint256 (** 从 8 位到 256 位的无符号整数)

**int8** 到**int 256(**8 位到 256 位有符号整数)，默认都是 32 字节。

uint8、uint256 等关键字可以分别用来分配 8 位到 256 位的存储大小。默认情况下，分配是 256 位。也就是说，uint 和 int 可以用来代替 uint256 和 int256。uint 和 int 分别是 **uint256** 和 **int256** 的别名(一个假的或假定的身份)。对这些类型执行算术运算有两种模式。

***未勾选和勾选模式***

*默认情况下，算法总是被检查，这意味着如果操作的结果落在类型的值范围之外，调用通过失败的断言被恢复。使用“未检查{…}”切换到未检查模式*

我们可以对整数执行的操作有:

**比较运算符**(计算结果为布尔值)

*< =(小于或等于)*

*<(小于)*

*==(等于)*

*！=(不等于)*

*> =(大于或等于)*

*>(大于)*

**位操作符**

&(按位与)

|(按位包含或)

^(按位异或)

~(按位非)

**算术运算符**

+(加法)

—(减法)

一元—(对单个操作数进行减法运算)

一元+(添加单个操作数)

*(乘以单个操作数)

/(除法)

%(除法的余数)

**(取幂运算)

<< (left shift)

· >>(右移)

## **固定点数**

这些用于存储带有十进制值的浮点数。有两种类型的定点数，即:

*   fixed —带符号的定点数。
*   ufixed —无符号定点数。

关键词: **ufixedMxN** 、 **fixedMxN** ，其中；

**M 代表类型**所取的位数；

**N 代表可用的小数位数**。

m 必须能被 8 整除，并且从 8 位到 256 位。n 必须介于 0 和 80 之间，包括 0 和 80。ufixed 和 fixed 分别是 ufixed128x18 和 fixed128x18 的别名。

注意:定点数可以在 Solidity 中声明，但是这种语言并不完全支持。

## 地址

每个帐户和智能合同都有一个存储为 20 字节的地址。该地址用于跨帐户发送和接收以太网。这可以认为是区块链上的公共身份或者账号。地址类型有两种类型，即:

address-保存一个 20 字节的值(以太坊地址的大小)。

地址支付-是相同的地址，但有转移和发送成员。

注意:智能合同地址之间的区别背后的思想是，应付地址可以接收以太网，而简单地址不能。

## 固定大小的字节数组

值类型 bytes1、bytes2、bytes3、…、bytes32 包含一个字节序列(从 1 到 32)。

可应用于此实值类型的运算符:

**对比:** < =，<，==，！=，> =，>(评估为布尔值)

**位运算符:** &，|，^(按位异或)，~(按位求反)

**移位操作符:** < <(左移)、> >(右移)

**索引访问:**如果 x 的类型是 bytesI，那么 x[k] for 0 < = k < I 返回第 k 个字节(只读)。

## **枚举**

solidity 中的枚举是创建用户定义类型的一种方式。它们可以显式地与所有整数类型相互转换，但可以隐式地转换。枚举值按照定义的顺序编号，从 0 开始。

```
Example:// SPDX-License-Identifier: MITpragma solidity ^0.8.7;contract EnumType {enum Months { Jan, Feb, Mar, April, May, June, July, Aug, Sept, Oct, Nov, Dec }function getFirstEnum() public pure returns(Months) {return Months.Jan;}}//result 0: uint8: 0 ( Enums are numbered in the way they are defined i.e Jan-0, Feb-1, Mar-2 and so on )
```

从整数的显式转换在运行时检查值是否在枚举的范围内，否则会导致死机错误。枚举需要至少一个成员，声明时其默认值是第一个成员。枚举的成员不能超过 256 个。

我希望这篇文章能让你更好地理解 solidity 中的值类型。请关注我的下一篇关于引用类型的文章。

**谢谢你看完！**

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [最佳免费加密信号](https://coincodecap.com/free-crypto-signals) | [YoBit 评论](/coinmonks/yobit-review-175464162c62) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [OKEx 回顾](/coinmonks/okex-review-6b369304110f) | [Kucoin 交易机器人](/coinmonks/kucoin-trading-bot-automate-your-trades-8cf0ca2138e0) | [期货交易机器人](/coinmonks/futures-trading-bots-5a282ccee3f5)
*   [AscendEx Staking](https://coincodecap.com/ascendex-staking)|[Bot Ocean Review](https://coincodecap.com/bot-ocean-review)|[最佳比特币钱包](https://coincodecap.com/bitcoin-wallets-india)
*   [霍比评论](https://coincodecap.com/huobi-review) | [OKEx 保证金交易](https://coincodecap.com/okex-margin-trading) | [期货交易](https://coincodecap.com/futures-trading)
*   [比特币基地赌注](https://coincodecap.com/coinbase-staking) | [热点评论](/coinmonks/hotbit-review-cd5bec41dafb) | [库币评论](https://coincodecap.com/kucoin-review)