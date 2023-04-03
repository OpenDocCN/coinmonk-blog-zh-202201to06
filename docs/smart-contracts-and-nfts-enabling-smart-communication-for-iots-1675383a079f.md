# 智能合同和 NFT:实现物联网设备的智能通信

> 原文：<https://medium.com/coinmonks/smart-contracts-and-nfts-enabling-smart-communication-for-iots-1675383a079f?source=collection_archive---------17----------------------->

什么是智能合约？

智能合约是安全的代码片段，在被触发时存储、验证和自我执行。由于没有人或中介的参与，智能合同的执行具有确定性，通常在几秒钟内完成，不依赖于银行假日。智能合约确保交易条件得到满足。它以与传统合同相同的方式定义了协议的规则和惩罚，并自动强制执行这些义务。

**什么是不可替代令牌(NFT)？**

“可替换”一词代表可以自由交换而不影响价值的属性，即一美元纸币或比特币。因此，不可替代性代表了资产的独特性和不可分割性。不可替代令牌虽然不是最响亮的词，但可以改变物联网设备的识别方式。虽然 NFT 一直出现在与数字艺术和收藏品相关的新闻中，但它们也可以用来唯一识别物联网设备。物联网设备的 NFTs 的这一属性非常有用，因为它解决了恶意或假冒设备欺骗真实物联网设备的问题。唯一识别物联网设备还有助于物联网设备的审计追踪、验证和定位。

**NFT 是如何产生的？**

物联网设备的 NFT 是使用 ERC-721 标准创建的，该标准为每个物理/数字资产仅生成一个令牌。NFT 是单独拥有的，所有者的变更需要固件重置。

使用唯一的 Id 和元数据(如制造商、用户、所有者和批准者)来管理 NFT 令牌的所有权。唯一 Id 和元数据的组合不能被克隆/复制。当物联网设备首次启动并连接到互联网时，会生成公钥和私钥对。公钥-私钥对以及一些其他信息被传递给一个智能契约，该契约铸造 NFT。这个智能合同还分配所有权并管理 NFTs 的可转让性。制造 NFT 的过程包括以下步骤:

创建新块

验证信息

将信息记录到区块链

NFT 有一些特殊的属性:

每个铸造的令牌都有一个唯一的标识符，直接与一个以太坊地址相关联。

它们不能与同类型的其他令牌直接互换。

每个令牌都有一个所有者，这个信息很容易验证。

私钥是原始内容的所有权证明，而内容创建者的公钥则充当该特定物联网设备的真实性证书。创建者的公钥本质上是令牌历史的永久部分。签名的消息可以用作所有权的证明，而不会泄露给任何人。没有人能以任何方式操纵它。当 NFT 所有权改变时，固件被重置，并且生成与新所有者相关联的新公钥。

【NFTs 和智能合约如何实现智能通信？

物联网设备以其区块链账户(BCA)参与区块链，BCA 是 NFT 的属性。物联网设备可以使用 BCA 账户对交易进行自助签名。这使得物联网设备可以跨网络共享数据。使用智能合同，可以在满足商定的交易条件后进行自动交易。因为不涉及任何中介，所以降低了识别和认证的成本。数据的分散性使其在没有中央系统作为目标的情况下也能抵御网络攻击。使用智能合约和 NFTs 有以下好处:

物联网设备可以记录位置、时间、温度等元数据。并使其作为元数据在区块链网络上可用。然后可以对元数据进行分析，以检查合规性和审计。

支付和谈判可以使用智能合同自动化，并在几秒钟内执行。

微支付可以在设备和服务之间轻松实现。

安全软件更新可以作为区块链上的 URL 发布，物联网设备可以使用加密哈希来验证更新。

**参考文献:**

[https://block geeks . com/guides/smart-contracts/# post-5615-_ A8 cy 6 rz 9 AAI 8](https://blockgeeks.com/guides/smart-contracts/#post-5615-_a8cy6rz9aai8)

[https://ethereum.org/en/nft/](https://ethereum.org/en/nft/)

[https://medium . com/asecuritysite-when-bob-met-Alice/trusted-IOT-linking-IOT-devices-to-NTFS-a 03 DBC 7 de 7 b 8](/asecuritysite-when-bob-met-alice/trusted-iot-linking-iot-devices-to-ntfs-a03dbc7de7b8)

[https://www . simpli learn . com/levelling-smart-contracts-for-IOT-applications-article](https://www.simplilearn.com/leveraging-smart-contracts-for-iot-applications-article)

[](https://iotbusinessnews.com/2021/03/31/03212-what-are-nfts-and-are-they-just-another-digital-fad/) [## 什么是 NFT，它们只是另一种数字时尚吗？

### 虽然您以前可能没有听说过“不可替换令牌”(NFT)这个术语，但这个数字概念在…

iotbusinessnews.com](https://iotbusinessnews.com/2021/03/31/03212-what-are-nfts-and-are-they-just-another-digital-fad/) 

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [Bookmap 点评](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)
*   [加拿大最佳加密交易机器人](https://coincodecap.com/5-best-crypto-trading-bots-in-canada) | [库币评论](https://coincodecap.com/kucoin-review)