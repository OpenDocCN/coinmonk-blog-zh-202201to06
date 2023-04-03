# 如何运行 StarkNet 节点(非常简单)

> 原文：<https://medium.com/coinmonks/how-to-run-a-starknet-node-very-easy-7937e3a7d942?source=collection_archive---------3----------------------->

![](img/bbe5a4dbb49f29cd2fde4c00f67fdaa0.png)

Photo by [Nathan Duck](https://unsplash.com/@nvte?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## StarkNet 是 StarkWare 在以太坊上的通用 zk rollup。

# 🏁表演

ZK 汇总可以像其他汇总技术一样压缩交易，方法是创建包含所有交易的小证明并将它们上传到区块链以太坊。这有点像上传一个文件夹的数据和上传一个. zip 文件。通过这一点，他们可以以非常低的成本实现类似签证的吞吐量。

# 🔒安全性

ZK 汇总没有安全假设。可能发生的最坏情况是交易被卡住。

# ✨权力下放

虽然当前的 zk 汇总处于早期开发阶段，还不是非常分散，但有些，如 StarkNet，现在已经有了功能节点客户端。🎉

# ⚖️可达性

多亏了 zk 的惊人和非常有前途的研究，交易成本已经非常低，并将继续大幅下降。

# 🛠如何运行 StarkNet 节点并成为 ZK 革命的一部分🚀

*我创建了一个小小的 shell 脚本，让你的生活更轻松。*

首先，您将希望设置一个至少有 2 个内核、2 GiBs RAM、50 GiBs 和您首选的 Linux 发行版(我们使用 Ubuntu 20.04)的实例，然后在您的主机上:

**更新:有了 Pathfinder 0.2.6-alpha，你不再需要任何额外的插件来构建 docker 镜像，JSON-RPC 现在也可以转发了！我只能推荐使用 docker，而不是从源代码构建节点！查看本教程使用 docker:**[https://medium . com/@ niklasbenjaminmuegge/running-starknet-nodes-very-easy-v2-92987909 cebc](/@niklasbenjaminmuegge/running-starknet-nodes-very-easy-v2-92987909cebc)设置 Pathfinder

1.克隆包含我的安装脚本的存储库。

```
git clone [https://github.com/nmuegge/starknet-pathfinder-install-script.git](https://github.com/nmuegge/starknet-pathfinder-install-script.git)
```

2.输入存储库。

```
cd starknet-pathfinder-install-script
```

3.将脚本复制到实例中，并使其可执行。

```
scp install_starknet_pathfinder_node.sh root@IP_ADDRESS:/root/
```

4.输入您的实例。

```
ssh root@IP_ADDRESS
```

5.使脚本可执行。

```
chmod -x install_starknet_pathfinder_node.sh
```

6.观看魔术表演，🧙‍🪄

```
./install_starknet_pathfinder_node.sh
```

***等瞧！✨欢迎来到 ZK 革命🚀***

**给自己一个大大的惊喜吧！你真棒！为自己支持#去中心化和#可及性而自豪！**

👇在 StarkNet discord 频道#full-node-success 与我们分享您的成功👇

[](https://discord.gg/Fx6zFE7n) [## 加入 StarkNet Discord 服务器！

### StarkNet 服务器是 StarkNet 所有参与者讨论和分享的地方。开发者，用户，基础设施，所有的事情都在谈论…

不和谐. gg](https://discord.gg/Fx6zFE7n) 

请随意查看我的 [crypto coda 页面](https://coda.io/@niklas-benjamin-muegge/crypto)获取更多指南和 alpha。