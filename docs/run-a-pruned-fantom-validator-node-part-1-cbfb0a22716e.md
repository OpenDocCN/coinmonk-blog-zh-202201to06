# 运行一个修剪过的 Fantom 验证器节点—第 1 部分

> 原文：<https://medium.com/coinmonks/run-a-pruned-fantom-validator-node-part-1-cbfb0a22716e?source=collection_archive---------11----------------------->

构建你的修剪过的验证器节点。

![](img/c1cf94a5fec729af43a5c154a83403e1.png)

**教程页面:**
[第一部分](https://blog.ethanharsh.com/run-a-pruned-fantom-validator-node-part-1-cbfb0a22716e) — *你在这里*
[第二部分](https://blog.ethanharsh.com/run-a-pruned-fantom-validator-node-part-2-89e1622eab27) — *下载&同步链数据* [第三部分](https://blog.ethanharsh.com/run-a-pruned-fantom-validator-node-part-3-fd6bc0ce9c7e) — *注册&运行* [完整教程](https://blog.ethanharsh.com/run-a-pruned-fantom-validator-node-e8297b38cbc)

**附加验证器帮助** 增加自我委托— *即将推出* 锁定自我赌注 *—即将推出* 增加&重新锁定自我赌注 *—即将推出* 更新验证器名称和标识 *—即将推出*

您想在 Fantom 网络上启动一个验证器节点吗？没问题。您想在链数据存储成本上节省大量资金吗？没问题。通过旋转修剪的验证器节点来保护网络并节省资金。

**什么是修剪？**

简而言之，修剪链数据会从区块链的本地副本中删除所有额外的、不必要的数据。修剪过的链数据对于验证器节点来说是完全可以接受的。

*一些最后的注释……*

首先，你需要最低的自我赌注金额(这是很多)。

*   最低赌注:50 万英尺

仅供参考，其他人可以向您的帐户下注的最大金额是:

*   最大验证者赌注:自我赌注金额的 15 倍

你的奖励…

*   回报:目前约 13%的 APY(自我持股的正常 APY+委托人 15%的回报)。APY 因赌注百分比而异。检查[https://fantom.foundation/ftm-staking/](https://fantom.foundation/ftm-staking/)获得最新的 APY。

## 验证程序参数

我在一个具有 700GB 磁盘空间 Google 云计算 N2D 系列 High Memory 4 实例上运行了一个 Fantom 验证程序。换句话说，一台拥有 4 个虚拟 CPU、32 GB 内存和 700GB 存储空间的电脑。这个大小似乎在大多数时间都保持了 40%到 50%的 CPU 利用率。

*TLDR；*

*   4vCPUs
*   32 GB 内存
*   700 GB 存储空间

相比之下，一个完整的验证器节点需要维护 4tb 的存储空间。那要贵得多。

## 概观

1.  启动云实例
2.  设置非超级用户
3.  安装所需的工具
4.  构建和测试
5.  下载修剪过的链接数据
6.  同步验证器节点
7.  注册验证器
8.  运行验证器节点

## 启动云实例

您可以在私有硬件或云服务上运行您的节点。Fantom 基金会建议在大型云提供商(亚马逊、谷歌云、数字海洋)上运行节点。我在谷歌云和数字海洋上都运行过节点。为了澄清，我将在本教程中使用 Ubuntu 20.04 LTS 版的命令。

## 设置非超级用户

这个有很多很多教程。下面是我个人最喜欢的在[数字海洋](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-20-04-quickstart)的团队写的。

## 安装所需的工具

安装准备验证器节点所需的工具。

```
sudo apt-get install -y build-essential wget ufw snapd
sudo snap install go --classic
```

## 设置防火墙

这让好的信息进来，把坏的信息挡在外面。谢谢 UFW。

```
sudo ufw allow OpenSSH
sudo ufw allow 5050/tcp
sudo ufw allow 5050/udp
yes | sudo ufw enable
```

## 安装验证器节点

从 Fantom foundation 发布的最新官方验证器节点中获取源代码。截至 2012 年 4 月 28 日，这是最新的版本。

```
wget -qO - https://github.com/Fantom-foundation/go-opera/archive/refs/tags/v1.1.0-rc.4.tar.gz | tar -xvz -C .
```

## 构建验证器节点

使用之前安装的工具从源代码构建可执行文件。

```
cd go-opera-1.1.0-rc.4
make
cp -r build/ ../.
cd ..
rm -r go-opera-1.1.0-rc.4
```

下一节将详细介绍如何下载 Fantom Opera Genesis 块，并使用修剪后的链数据同步您的节点。以这种方式构建节点将为您节省大量的时间和金钱。

***伊森哈什*** *Web3 开发者| Fantom 爱好者*
[个人网站](https://ethanharsh.com/)
[LinkedIn](https://www.linkedin.com/in/ethanharsh/)
[insta gram](http://instagram.com/eharsh4)

![](img/51a26626264e126c2dcfedfae315e486.png)

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [BigONE 交易所评论](/coinmonks/bigone-exchange-review-64705d85a1d4) | [电网交易 Bot](https://coincodecap.com/grid-trading)
*   [氹欞侊贸易评论](https://coincodecap.com/anny-trade-review) | [CoinSpot 评论](https://coincodecap.com/coinspot-review)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [投资印度的最佳加密软件](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021) | [WazirX P2P](https://coincodecap.com/wazirx-p2p)
*   [7 大最佳零费用密码交易平台](https://coincodecap.com/zero-fee-crypto-exchanges)