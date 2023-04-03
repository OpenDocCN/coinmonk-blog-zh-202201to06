# 区块链:第 3 天——撰写你的第一份智能合同

> 原文：<https://medium.com/coinmonks/blockchain-day3-writing-your-first-smart-contract-4a2ac655c8c0?source=collection_archive---------12----------------------->

# **一、概述**

距离我的上一篇帖子已经过去几周了，因为我现在的项目太忙了。今天，我将继续我关于区块链的系列文章，学习如何使用 solidity 写一个简单的智能合同。

让我们考虑一个关于一个令人敬畏的图书馆的简单场景。作为库，必须满足以下要求

*   图书馆有藏书
*   我们将用一些信息来表示每本书，比如 isbn、作者、书名。
*   只有图书馆的所有者可以添加图书
*   如果有书的话，其他人可以来借
*   书籍必须在阅读后归还给图书馆，以便其他人可以借阅

# 二。履行

*   第一步是定义我们的库

```
// SPDX-License-Identifier: GPL-3.0pragma solidity ^0.8.4;contract Library{
    string internal _name = "An Awesome Library"
    /** * Return library name */ function name() public view returns (string memory) { return _name; }}
```

没有什么需要解释的，因为我们刚刚定义了一个具有初始名称的库。函数`name()`除了返回当前库的名称之外什么也不做。

*   图书馆需要书，所以让我们简单地用`struct`来定义一本书的样子:

```
// Sample structure of a Bookstruct Book { string isbn; string title; string author;}
```

*   区块链在最大程度上是一个账本，可以用作数据库，让我们定义我们简单的数据库的表称为`bookstore`，账本记录谁借了哪本书

```
// BookstoreBook[] internal bookstore;//Book id -> borrower mapping(uint256 => address) internal ledger;
```

*   现在一个构造函数来初始化我们刚刚创建的东西

```
constructor(string memory name_) { _name = name_; bookstore.push( Book({ isbn: "9781853260315", title: "20,000 Leagues Under the Sea (Wordsworth Classics)", author: "Jules Verne" }) );}
```

这里我们给所有者一个机会，在部署时定义他/她自己的图书馆名称，并把一本书推送到我们的书店，这只是一个例子。

*   所有者可以添加图书。我们可以做一个限制来满足这个要求。`function modifier`这是我想到的第一件事，但由于我是一个懒惰的开发人员，我决定使用 OpenZeppelin 的 [Ownable](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable.sol) 合同来代替:

```
// SPDX-License-Identifier: GPL-3.0pragma solidity ^0.8.4;import "@openzeppelin/contracts/access/**Ownable.sol**";contract Library is **Ownable** {string internal _name = "A Wonderful Library";// Sample structure of a Bookstruct Book { string isbn; string title; string author;}// BookstoreBook[] internal bookstore;mapping(uint256 => address) internal ledger;constructor(string memory name_) { _name = name_; bookstore.push( Book({ isbn: "9781853260315", title: "20,000 Leagues Under the Sea (Wordsworth Classics)", author: "Jules Verne" }) );}/*** Return library name*/function name() public view returns (string memory) { return _name;}/*** Add new Book*/function addBook(string memory _isbn, string memory _title, string memory _author) public **onlyOwner** { bookstore.push( Book({ isbn: _isbn, title: _title, author: _author }) );
 }}
```

*   现在是`borrow`和`return`出书的时候了:

```
function getBookById(uint256 _bookId) external view onlyValidBookId(_bookId) returns (uint256 bookId,string memory isbn, 
string memory title, 
string memory author, 
address borrower) { Book storage book = bookstore[_bookId]; bookId = _bookId; isbn = book.isbn; title = book.title; author = book.author; borrower = ledger[_bookId];}/**Function: borrowingBookInput : bookIdReturn : boolean*/function isBorrowingBook(uint256 _bookId) public view onlyValidBookId(_bookId) returns (bool) { return msg.sender == _getBorrowerByBookId(_bookId);}function isAvailable(uint256 _bookId) public view onlyValidBookId(_bookId) returns(bool) { return ledger[_bookId] == address(0);}modifier onlyBorrowable(uint256 _bookId) { require( !isBorrowingBook(_bookId) && isAvailable(_bookId), "Not available or already borrowed by you." ); _;}/**Function : borrowInput : _bookId*/function borrow(uint256 _bookId) public onlyBorrowable(_bookId) { ledger[_bookId] = msg.sender; emit Borrow(msg.sender, _bookId);}/**Function : borrowInput : _bookId*/function takeBack(uint256 _bookId) public { require( isBorrowingBook(_bookId), "Can only return borrowing book." ); ledger[_bookId] = address(0); emit TakeBack(msg.sender, _bookId);}
```

这里我们做一些验证

*   我们想借的书的 id 是一个有效的 id，不超过书店数组的最大 id。
*   如果分类账不包含借书历史或包含借书历史，但借书人是地址(0)，则认为该账簿可用。
*   一个人只能在有书的时候借书
*   一个人只有在他/她是借书人的情况下才能把书还给图书馆

我们还为对借书或还书事件感兴趣的客户发出事件。

# 三。最后的话

今天，我们使用以下知识创建了一个简单的图书馆智能合同:

*   合同
*   功能
*   访问修饰符:内部，公共…
*   数据类型:基本类型，结构类型，数组，集合…
*   功能修饰符
*   外部库(openzeppelin)

在下一章，我们将看到如何使用 etherjs 与我们的智能合约进行交互。