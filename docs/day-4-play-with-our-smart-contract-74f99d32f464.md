# 区块链:第 4 天——玩转我们的智能合约

> 原文：<https://medium.com/coinmonks/day-4-play-with-our-smart-contract-74f99d32f464?source=collection_archive---------24----------------------->

# 先决条件

在进入这篇文章之前，请阅读我之前的关于使用 EtherJS 和 VueJS 来设置项目的文章。

[](/coinmonks/blockchain-day-2-etherjs-vuejs-4a2896a50ef2) [## 区块链:第二天— EtherJS + VueJS

### #概述

medium.com](/coinmonks/blockchain-day-2-etherjs-vuejs-4a2896a50ef2) 

# 操场

## 部署您的合同

是时候将您新创建的合同`Library`部署到 Ganache 或 Hardhat 网络上了。

如果 hardhat 网络作为本地以太坊测试网络:

```
// In one terminal
npx hardhat node//on the other terminal
npx hardhat run scripts/deploy.ts --network hardhat
```

或者，如果您已经将 Ganache 定义为本地测试工作，那么这几乎是相同的

```
npx hardhat run scripts/deploy.ts --network ganache
```

记得启动 ganache，并在您的`hardhat.config.ts`中定义 ganache 网络

```
networks: {     
    ganache: { 
        url: "http://127.0.0.1:7545", 
        accounts: process.env.GANACHE_PRIVATE_KEY !== undefined ?                 
          [process.env.GANACHE_PRIVATE_KEY] : [], 
    }, 
},
```

如果合同部署成功，由于`deploy.ts`中的以下代码，合同的地址将在终端上打印出来

```
async function main() { const Library = await ethers.getContractFactory("Library"); const library = await Library.deploy("Miichisoft Library"); await library.deployed(); console.log("Library deployed to:", library.address);}
```

## 玩弄你的契约

由于我们已经在[的前一篇文章](/coinmonks/blockchain-day-2-etherjs-vuejs-4a2896a50ef2)中实现了 EtherJS 插件，现在我们可以很容易地与我们部署的契约进行交互。比方说，如果我们想给图书馆增加一本新书。

UI 准备会有人这样想:

```
<div> <label for="isbn">ISBN:</label> <input id='isbn' type="text" v-model="new_book.isbn"> <label for="author" >Author:</label> <input id='author' type="text" v-model="new_book.author"> <label for="title">Title:</label> <input id='title' type="text" v-model="new_book.title"> <button class="primaryButton" @click="addBook()">Add</button></div>
```

我们的 Vue 数据模型:

```
data() { return { currentAccount: null, currentContract : null, contractAddress: "<deployed_address", new_book: { isbn:'', title:'', author:'' } };},
```

每当我们点击`Add`按钮时，我们从输入中获取所有信息，组成一个图书结构并调用智能合同功能

```
methods:{
    addBook: async function(){ await this.currentContract.addBook(this.new_book.isbn, this.new_book.title, this.new_book.author);},}
```

现在，您可以输入图书的 isbn、书名和作者，然后单击 add 按钮，MetaMask 会询问您是否允许触发新事务来添加新书。在您的批准下，将创建一个新的交易，签名并通过网络发送，以向我们的书店添加一本新书。

练习:当我们添加完一本新书时，通过使用 EtherJS 与您的网络进行交互，实现您自己的逻辑来显示书店中的所有书籍将是一个很好的练习。

# 最后的

我们完成了前端，展示了使用我们的 EtherJS 插件与区块链交互的能力。在下一篇文章中，我们将看到如何从我们的智能契约中发出一个事件，以及如何捕捉发出的事件并在 VueJS 前端使用它们。