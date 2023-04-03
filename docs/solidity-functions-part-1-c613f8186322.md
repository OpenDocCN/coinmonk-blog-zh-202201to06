# 实度函数第一部分

> 原文：<https://medium.com/coinmonks/solidity-functions-part-1-c613f8186322?source=collection_archive---------26----------------------->

# vi̇ew

函数可以被声明为`**view**`，在这种情况下它们承诺不修改状态。

例如:

```
function random() public view returns (uint8) { return uint8(uint256(keccak256(block.timestamp, block.difficulty))%20);}// it generates a number that is between 1 and 20 //
```

## 注意

以下语句被视为修改状态:

1.  写入状态变量。
2.  [发射事件](https://docs.soliditylang.org/en/v0.8.11/contracts.html?highlight=view#events)。
3.  [创建其他合同](https://docs.soliditylang.org/en/v0.8.11/control-structures.html#creating-contracts)。
4.  使用`selfdestruct`。
5.  通过电话发送以太网。
6.  调用任何未标记为`**view**`或`pure`的函数。
7.  使用低级调用。
8.  使用包含某些操作码的内联程序集。

# 纯的

函数可以被声明为`pure`，在这种情况下，它们保证不读取或修改状态。

```
pragma solidity ^0.5.0;

contract Test {
   function getResult() public pure returns(uint product, uint sum){
      uint a = 1; 
      uint b = 2;
      product = a * b;
      sum = a + b; 
   }
}
```

# 输出

```
0: uint256: product 2
1: uint256: sum 3
```

## 注意

以下语句如果出现在函数中，将被视为读取状态，在这种情况下编译器将抛出警告。

1-读取状态变量。

2-访问地址(this)。平衡还是

.balance。

3-访问 block、tx、msg 的任何特殊变量(可以读取 msg.sig 和 msg.data)。

4-调用任何未标记为纯函数的函数。

5-使用包含某些操作码的内联程序集。