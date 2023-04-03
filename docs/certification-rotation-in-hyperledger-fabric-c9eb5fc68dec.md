# Hyperledger 结构中的证书轮换/续订:恢复过期的证书结构网络

> 原文：<https://medium.com/coinmonks/certification-rotation-in-hyperledger-fabric-c9eb5fc68dec?source=collection_archive---------4----------------------->

证书轮换是 Hyperledger 结构中最重要和最关键的部分之一。

![](img/b4e90b5a3a15810d3a76cc2f7166a70e.png)

[**Photo by Shubham Dhage on Unsplash**](https://unsplash.com/photos/_rZnChsIFuQ)

签名下有三个部分 1) CA
2)注册
3) TLS

请检查任何 fabric-ca-server-config.yaml 中的签名部分

**签名部分:**
“默认”部分用于注册证书的签名；默认到期(“到期”字段)为“8760h”，即 1 年(小时)。

**Profile:ca**
“CA”Profile 子部分用于签署中间 CA 证书；默认到期(“到期”字段)是“ **43800h** ”，即 5 年(小时)。请注意，“isca”是真的，这意味着它颁发 ca 证书。maxpathlen 为 0 意味着中间 CA 不能颁发其他中间 CA 证书，尽管它仍然可以颁发终端实体证书。

**Profile:tls**
“TLS”Profile 子部分用于签署 TLS 证书请求；默认到期(“到期”字段)为“ **8760h** ”，即以小时为单位的 **1** 年。

tls 和注册证书的默认有效期为 1 年( **8760h** )。如果您的网络建成 1 年，您可能会面临认证过期的问题，事实上，您将无法与网络互动，实际上您的网络将关闭。

解决方案:
1)到期前轮换证书。(我们应该遵循这个)
2)到期后轮换证书。(如果您忘记了续订证书，不推荐使用这种方法，您可以使用这种方法来恢复证书)

让我们把这篇文章分成两部分

1.  使用过期的证书创建网络
2.  恢复过期证书的网络(您可以将此活动视为证书轮换)

我建议浏览我的 youtube 视频，里面有所有的信息。在这篇文章中，我只是提到了步骤，而不是所有的编码部分。我用自己的回购创造了一个网络。在我以前的视频有关于如何从头开始创建一个网络的所有信息。

## **第一部分**

注意:**如果您已经使用过期的证书联网，您可以从第 2 部分开始。**

1.  将您的机器时间设置为过去的日期(32 天前)
2.  为所有组织创建 CA 服务
3.  更改 fabric-ca-server-config.yaml 文件，如下所示

4.重新启动 CA 服务。
5。创建所有参与者证书。6。创建通道工件
7。运行所有其他服务(Peer、order、CouchDB)
8。部署链码。
9。在 API 中创建一个连接配置文件。
10。调用一些事务并验证是否一切正常。

注意:在这个阶段，我们有一个工作网络。注册和 TLS 的默认证书过期时间都是 720 小时(30 天)。

## **第二部分**

1.  将日期更改为当前。现在，我们有一个在 32 天之前创建的网络，默认到期时间是 30 天(720 小时)。在这个阶段，我们有一个证书过期的网络。为了验证，您可以检查任何服务的日志(peer，orderer)，可能会有错误。
2.  我们必须为网络中的所有参与者创建新的证书(注册、TLS)。在 repo 中有一个 renew-cert.sh 脚本可用，只需运行它，它将创建新的证书。
3.  现在，我们需要在所有订购者服务中使用 env 变量。添加这些变量并重新启动订购程序。

```
- ORDERER_GENERAL_TLS_TLSHANDSHAKETIMESHIFT=200h- ORDERER_GENERAL_CLUSTER_TLSHANDSHAKETIMESHIFT=200h- ORDERER_GENERAL_AUTHENTICATION_NOEXPIRATIONCHECKS=true
```

4.用新创建的 MSP 文件夹更改所有订购者、所有对等者的所有 MSP 文件夹，并重新启动服务。

5.我们必须进行配置更新，以更改订购者 tls 证书。在当前网络中，我们有一个应用程序通道，一个系统通道。

6.我们可以一次更新一个订购者的配置。我们有两个通道，这意味着我们必须进行 3x2=6，6 配置更新。

7.在上述视频中，我已经涵盖了所有步骤，请通过它，并在回购所有可用的代码

8.首先对系统通道和应用程序通道进行配置更新。成功完成后，替换新创建的 tls 证书并重新启动订购者。

9.对所有订购者执行相同的上述程序。

10.用新创建的 tls 文件夹替换所有对等方的 tls 文件夹，并重新启动所有对等方

11.在 API 中重新创建连接配置文件并重启服务器。

12.从钱包中删除过期的管理员身份，注册新用户，尝试调用新交易。验证它是否成功执行。

13.一件重要的事情是，当在 API 注册一个新用户时，我们必须存储从 CA 返回的秘密(在注册中)，否则我们将无法重新注册同一个用户。

14.您可以对证书轮换或续订使用相同的脚本。这里我们在过期的网络上做一些活动。您可以在证书到期前续订证书，这样我们的网络就可以正常运行，不会因为证书到期而停机。

15.下面提到的配置更新脚本示例。

本文到此为止，我知道它非常简短，但在视频中，我已经涵盖了轮换/续订证书所需的大部分内容。

如果你面临任何问题，请让我知道，我很乐意帮助你。你可以通过 linked in 或 Instagram 与我联系。
[](https://www.instagram.com/pavanadhavofficial/)**[**https://www.linkedin.com/in/pavan-adhav/**](https://www.linkedin.com/in/pavan-adhav/) **邮箱:adhavpavan@gmail.com****

# **参考**

*   **[https://github.com/adhavpavan/FabricNetwork-2.x.git](https://github.com/adhavpavan/FabricNetwork-2.x.git)**

> **加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资**

# **另外，阅读**

*   **[SmithBot 评论](https://coincodecap.com/smithbot-review) | [4 款最佳免费开源交易机器人](https://coincodecap.com/free-open-source-trading-bots)**
*   **[比特币基地僵尸工具](/coinmonks/coinbase-bots-ac6359e897f3) | [AscendEX 审查](/coinmonks/ascendex-review-53e829cf75fa) | [OKEx 交易僵尸工具](/coinmonks/okex-trading-bots-234920f61e60)**
*   **[如何在印度购买比特币？](/coinmonks/buy-bitcoin-in-india-feb50ddfef94) | [瓦济克斯审查](/coinmonks/wazirx-review-5c811b074f5b)**
*   **[隐翅虫替代品](/coinmonks/cryptohopper-alternatives-d67287b16d27) | [HitBTC 审查](/coinmonks/hitbtc-review-c5143c5d53c2)**
*   **[CBET 评论](https://coincodecap.com/cbet-casino-review) | [库科恩 vs 比特币基地](https://coincodecap.com/kucoin-vs-coinbase)**
*   **[折叠 App 审核](https://coincodecap.com/fold-app-review) | [Kucoin 交易机器人](/coinmonks/kucoin-trading-bot-automate-your-trades-8cf0ca2138e0) | [Probit 审核](https://coincodecap.com/probit-review)**