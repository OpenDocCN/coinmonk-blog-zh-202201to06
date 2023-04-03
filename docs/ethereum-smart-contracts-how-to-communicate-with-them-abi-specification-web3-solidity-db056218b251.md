# 以太坊智能合约。怎么和他们沟通？(ABI 规范，web3，可靠性)

> 原文：<https://medium.com/coinmonks/ethereum-smart-contracts-how-to-communicate-with-them-abi-specification-web3-solidity-db056218b251?source=collection_archive---------1----------------------->

智能合约部署在区块链，它们是包含一些逻辑的代码片段，由 EVM 执行，将以太坊区块链变成一种世界分布式计算机。

智能合约可以由向区块链提交事务的链外用户/程序调用，或者它们也可以通过调用彼此的方法在它们之间通信(在链外调用之后，智能合约不能“触发”它们自己)。