# 坚固性—存储与内存对比呼叫数据

> 原文：<https://medium.com/coinmonks/solidity-storage-vs-memory-vs-calldata-8c7e8c38bce?source=collection_archive---------0----------------------->

![](img/e1da9cc1e185108bcb1a3b48f81bbdec.png)

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/storage?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

无论何时，当您在 Solidity 中编写智能合同时，您必须了解 EVM 是如何处理您的变量和数据的。您所做的选择将影响天然气成本(调用您的功能或部署您的合同)以及存储布局。

考虑到 Ethereum 中的每一个块空间都被高度重视(因此 Eth 的成本，尽管最近在下降)，这严重影响了您的代码和最终契约的效率，这有望被频繁调用。每个函数调用都使用气体；当总结整个函数调用的潜在寿命时，每一点节省都有帮助。

# 储存；储备

`Storage`最容易理解——所有状态变量都存储在**中**。因为状态可以在契约中改变(例如，在函数中)，所以`storage`变量必须是可变的。但是它们的*位置*是持久的，它们保存在区块链。

`storage`中的状态变量以紧凑的方式排列——如果可能的话，多个值将占据相同的`storage`位置。除了动态大小的数组和结构的特殊情况之外，其他变量都被打包成 32 字节的块。

如果这些变量少于 32 字节，它们将被合并以占据同一个槽。否则，他们将被推到下一个`storage`位置。数据按其在合同中的声明顺序，从`0`槽(至槽`1`、`2`、`3`等)开始连续存储(即一个接一个)。

动态数组和结构总是占据一个新的槽，并且跟随它们的任何变量也将被初始化以开始一个新的`storage`槽。

因为动态数组和结构的大小都是先验未知的(例如，直到您在契约中为它们赋值)，所以它们不能与它们的数据一起存储在其他状态变量之间。取而代之的是，假设它们占用 32 个字节，并且其中的元素从一个单独的`storage`槽开始存储，该槽是使用 Keccak-256 哈希计算的。

但是，常量状态变量是*而不是*保存到`storage`槽中。相反，它们被直接注入到契约字节码中——每当这些变量被读取时，契约会自动将它们切换为它们所分配的常量值。

# 记忆

`**Memory**` **是为函数范围内定义的变量保留的。它们只在一个函数被调用时存在，因此是临时变量，不能在这个作用域之外被访问(也就是在你的契约中除了这个函数之外的任何地方)。然而，它们在函数中是可变的。**

Solidity 为`memory`预留了 4 个 32 字节的槽位，具体字节范围由:1) 64 字节的暂存空间，用于哈希方法；2) 32 字节用于当前分配的`memory`大小，这是空闲的`memory`指针，Solidity 总是在这里放置新的对象；以及 3)32 字节零槽——用作动态`memory`数组的初始值，并且永远不应该被写入。

由于这些布局差异，数组和结构会根据是在`storage`还是`memory`中而占据不同的空间。

## 示例:

```
uint8[4] arr;struct Str {
    uint v1;
    uint v2;
    uint8 v3;
    uint8 v4;
}
```

在这两种情况下，数组`arr`和结构`Str`在`memory`中占据 128 个字节(即 4 项，每项 32 字节)。然而，作为`storage`，`arr`仅占用 32 字节(1 个槽)，而`Str`占用 96 字节(3 个槽，每个槽 32 字节)。

# 呼叫数据

`**Calldata**` **是一个不可变的临时位置，用于存储函数参数，其行为很像** `**memory**` **。**

建议尽量使用`calldata`，因为这样可以避免不必要的复制，确保数据不被更改。带有`calldata`数据位置的数组和结构也可以从函数中返回。

这种类型的数据被认为是 ABI 规范定义的格式，即填充到 32 字节的倍数(不同于内部函数调用)。构造函数的参数略有不同，因为它们直接附加在契约代码的末尾(也是 ABI 编码)。

# 比较

每当你定义一个引用类型变量(数组或结构)时，你还需要定义它的数据位置——除非它是一个状态变量，在这种情况下，它被自动解释为`storage`。自从 Solidity v0.6.9 以来，`memory`和`calldata`在所有函数中都是允许的，而不管它们的可见性类型(即外部、公共等)。

赋值将导致创建副本，或者仅仅是对同一数据块的引用—类似于 Javascript 中的对象或数组:

*   在`storage`和`memory`(或从`calldata`)之间的分配总是创建一个单独的副本。
*   从`memory`到`memory`的赋值仅创建引用。因此，改变一个内存变量会改变引用相同数据的所有其他内存变量。
*   从`storage`到局部存储变量的赋值也只分配一个引用。
*   所有其他分配给`storage`的任务总是复制。

对于函数中的数组参数，建议使用`calldata`而不是`memory`，因为这样可以节省大量气体。例如，通过使用`calldata`，在输入数组上循环的求和函数可以节省大约 1829 gas (~3.5%)。

```
// Gas used: 50992
function func1 (uint[] memory nums) external {
  for (uint i = 0; i < nums.length; ++i) {
     ...
  }
}// Gas used: 49163
function func2 (uint[] calldata nums) external {
  for (uint i = 0; i < nums.length; ++i) {
     ...
  }
}
```

就这些——一些关于 Solidity 中数据位置的信息。感谢阅读！

## 参考资料:

*   [https://docs . soliditylang . org/en/v 0 . 8 . 13/types . html # data-location-and-assignment-behavior](https://docs.soliditylang.org/en/v0.8.13/types.html#data-location-and-assignment-behaviour)
*   [https://docs . solidy lang . org/en/v 0 . 8 . 13/types . html # reference-types](https://docs.soliditylang.org/en/v0.8.13/types.html#reference-types)
*   [https://docs . solidy lang . org/en/v 0 . 8 . 13/internals/layout _ in _ storage . html](https://docs.soliditylang.org/en/v0.8.13/internals/layout_in_storage.html)
*   [https://twitter.com/Web3Oscar/status/1514509414501343234](https://twitter.com/Web3Oscar/status/1514509414501343234)
*   [https://Twitter . com/Patrick alpha c/status/1514257121302429696](https://twitter.com/PatrickAlphaC/status/1514257121302429696)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Bookmap 点评](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)