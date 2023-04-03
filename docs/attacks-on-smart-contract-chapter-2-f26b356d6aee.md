# 对智能合同的攻击—第 2 章

> 原文：<https://medium.com/coinmonks/attacks-on-smart-contract-chapter-2-f26b356d6aee?source=collection_archive---------17----------------------->

![](img/7c5ca25b2f98be8b95293dc6e35ed3e7.png)

Photo By Stevanovicigor on [TechRepublic](https://www.techrepublic.com/article/distributed-denial-of-service-ddos-attacks-a-cheat-sheet/)

# 拒绝服务(DoS)攻击

那么什么是拒绝服务攻击呢？这是一种攻击，目的是阻止您的智能合约执行其指定用户可以访问的功能。

## 让我们以 KingOfEther 合同为例:

该示例有两个协定，一个是受害者协定“KingOfEther.sol ”,另一个是攻击者协定“Attacker.sol”。

KingOfEther 的目的是通过转移更多的以太来征服上一任国王。前任国王送的乙醚量会退还。

**KingOfEther.sol :**

**攻击者. sol :**

合同期望最高的乙醚量来维持国王的地位。如果用户发送的以太比之前的国王多，那么他/她将成为新国王，之前的国王将被退还。

这似乎在技术上是正确的。但是，当攻击者试图与协定进行交互并执行攻击时，攻击者将创建一个协定来与您的智能协定进行交互。攻击者的协定可以具有带 revert 语句的 fallback()函数，也可以没有 fallback()函数。当有人试图向攻击者的合同汇款而交易失败时，这将返回一个还原错误。

在上面的场景中，攻击者比之前的国王发送更多的以太，并成为国王。在这一点上，如果另一个用户来了并且支付比攻击者更多的钱来成为国王，那么该合同将向攻击者退款，因为它获得了新的最高价格，但是在这种情况下，该交易失败，因为攻击者的合同没有回退/接收功能来接收到该合同的钱，这将恢复该交易并且使攻击者永远成为国王。

## 解决办法

为了防止这种攻击，我们可以创建一个取款功能，让用户取款，而不是将合同发送给他们。在这种情况下，当受影响的用户试图退出时，他将成为攻击者。

**金戈菲瑟尔:**

> **代码示例:**[**https://solidity-by-example.org/hacks/denial-of-service/**](https://solidity-by-example.org/hacks/denial-of-service/)

🥳祝贺你，我们现在已经知道了关于可靠性的一个可能的攻击。让我们一起了解更多。

在[媒体](/@nufailismath15)、 [LinkedIn](https://www.linkedin.com/in/nufail-i-61377b10b/) 、 [Instagram](https://www.instagram.com/nufail_ismath/) 、 [Twitter](https://twitter.com/ismath_nufail) 上关注我