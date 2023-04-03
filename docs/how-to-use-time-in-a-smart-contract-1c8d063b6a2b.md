# 如何在智能合同中使用时间？

> 原文：<https://medium.com/coinmonks/how-to-use-time-in-a-smart-contract-1c8d063b6a2b?source=collection_archive---------9----------------------->

![](img/0b9c2bc01b1552f3dcc8887c2b583601.png)

在编写智能合同时，您可能会遇到基于时间的需求。在这种情况下，您应该能够在智能合约中存储时间。

## 那么，如何在智能合约中存储时间呢？

在 solidity 中，我们使用整数来存储 Unix 时间格式的时间。

看看下面的智能合同。

# 需要注意的要点:

*   我们使用类型单元(无符号整数)来存储 Unix 时间戳。
*   在 solidity 中，“block.timestamp”给出当前时间。我们可以通过调用“getCurrentTime()”来验证这一点。
*   我们还可以使用 Unix 时间格式执行不同的操作，例如' == '、'≤'、'≥'。

感谢你阅读这篇文章，❤

要了解更多关于区块链和智能合约的信息，请访问[ontheether.com](https://www.ontheether.com/)。

评论下你想学的区块链话题。

拍手声👏如果这篇文章对你有帮助。

在 [LinkedIn](https://www.linkedin.com/in/ajith-m-doodlebug/) 和 [GitHub](https://github.com/ajith-m-doodlebug/blockchain) 上和我联系。