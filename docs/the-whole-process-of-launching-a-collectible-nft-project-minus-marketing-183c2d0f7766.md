# 推出一个有收藏价值的 NFT 项目的全过程(减去营销)

> 原文：<https://medium.com/coinmonks/the-whole-process-of-launching-a-collectible-nft-project-minus-marketing-183c2d0f7766?source=collection_archive---------5----------------------->

创建创成式艺术、部署智能合同、创建铸造 DApp 的概述，以及有关该流程的其他信息。

![](img/8ac44b659b2a3559aff195fc60876723.png)

Photo by [Arno Senoner](https://unsplash.com/@arnosenoner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

考虑到需要你全神贯注的各个领域，启动一个 NFT 项目在理想情况下是一个团队过程。但是如果你愿意探索其中的每一个，并且相信你会喜欢它，那么它可以是一个人的项目。在这篇文章中，我将概述所有的步骤，并分享我的实验如何在以太坊区块链上结束。请记住，这是一篇半技术性的文章，可以用作指南。

# 介绍

你好。我是 [Arda](https://linktr.ee/ardadurak) ，这是我的第一篇文章。我会在最后一段多谈谈我自己，这不是你来这里的原因。我将快速解释一下我的项目，以便在文章中引用。不是为了宣传。

> 在这里插入你对**持怀疑态度**的偏好 GIF，最好是来自一部有趣而聪明的电视剧。

我正在创建和发布我的项目的最后阶段，[突然独角兽](https://www.suddenlyunicorns.com)。是以太坊区块链上 11111 个独特像素艺术 NFT 的生成性艺术项目。

[](https://www.suddenlyunicorns.com/) [## 突然独角兽集合-以太坊区块链上 11111 个唯一的 NFT

### 探索以太坊区块链上的突然独角兽收集和薄荷独特的 NFT。您可以查看项目详情…

www.suddenlyunicorns.com](https://www.suddenlyunicorns.com/) 

和每个人一样，我已经听说了很多关于 NFTs 的事情，两个月前，我终于决定亲自探索一下，看看外面有什么。这让我对 Web3 进行了更多的探索，并了解了 NFT 是如何成为它的一部分的。所以我没有选择做这个项目，而是为了在我最喜欢的地方开始我的 Web3 冒险。

在这期间，我不得不做大量的阅读，实验，从零开始。我将在这篇文章中分享我的经验；主要是作为一个概述，并在将来单独和更技术性地重新审视每个步骤。

# 找到一个想法

我将保持这一部分的简短，因为它对每个人都有不同的作用。虽然它们都感觉是理论性的，但是有大量的文章是关于获得独特的想法的。基本上，你可以想出一个能激励你或让你开心的概念，可以选择任何可以定制的东西(比如颜色、配饰、任何类型的特征)，等等。在 OpenSea 上浏览一些收藏品可能会给你带来灵感。在一个昏昏欲睡的早晨，我和女儿一起玩耍时产生了这个想法。这不是非常独特的，但足以让我开始。

# 创造艺术和稀有桌子

根据您想要生成多少可收集的令牌，您必须创建足够的特征来提供唯一性。配件和身体(或一般，如果它是一个对象)的特点是显而易见的选择，结合颜色的变化。

考虑到我的艺术技巧，我决定用简单化的像素艺术。在尝试了各种桌面和在线工具后，我决定用 [**Pixilart**](http://pixilart.com/draw) 。和它一起工作绝对是一种享受。我只使用 Adobe Photoshop 来修复一些部分、图层和其他琐碎或细节的东西。

[](http://pixilart.com/draw) [## 在线制作像素艺术- Pixilart

### 这个绘图工具允许你制作像素艺术，游戏精灵和动画…

pixilart.com](http://pixilart.com/draw) 

我创造了基础独角兽形象。接下来，我为特征组建立了一个文件夹结构，并开始创建特征图像，大部分是附件。你必须小心地创造特征，这样每一个都可以完美地搭配和共存，并且有正确的分层顺序——例如，长睫毛不能遮住太阳镜。

你可以从其他系列中寻找灵感。我克制自己不去做，直到我完全被卡住，这样我就不会受到太大的影响。我不停地创造，删除，喜欢，讨厌他们中的许多人。但不知道何时停止，以及如何组织和管理这一切。我认为下面的文章在这方面对我帮助最大。

[](/web-design-web-developer-magazine/how-to-prepare-a-rarity-table-for-a-generative-nft-art-programmer-1c081db52f29) [## 如何为一个 NFT 艺术程序员准备一张罕见的桌子

### 因为你希望在你的生成集中有一些稀有的项目，对吗？

medium.com](/web-design-web-developer-magazine/how-to-prepare-a-rarity-table-for-a-generative-nft-art-programmer-1c081db52f29) 

一张**稀有度表**对于确保你收藏的代币的独特性至关重要。这就是你如何控制每一个特征的分布。这种规模的集合很少是平均分布的(我的意思是 11，111，但我想对于更小的规模也是如此)。本文中的示例表由 10 个不同的特征组组成，每个组平均有 10 个特征，用于创作 10，000 件艺术品。我认为除了自己创建一个类似的表之外，别无他法。我更喜欢使用 Excel 表作为可视化指南，并验证特征组百分比的总和总是百分之百，尽管从 Excel 中检索需要一些额外的逻辑，但保持它仍然比 JSON 文件更实用。

我的图片初稿和稀有度表已经准备好了，但它们一直在变，直到最后。因为这是澄清他们是否合作的下一个主题，需要无数次的迭代。

# 生成艺术品和元数据

基础图像、所有独立的特征图像、颜色决策和稀有度表；创作艺术品所需的所有基础工作都已准备就绪。现在你必须找到结合你的艺术和创建元数据的最佳方式。

考虑到我读过的所有东西，似乎 [HashLips 艺术引擎](https://github.com/HashLips/hashlips_art_engine)是最受欢迎的。特别是如果你不想一个人过多地研究图像合成、元数据创建。

但正如我所说，我去那里是为了好玩。所以我决定自己编码，完全控制它。我希望我可以共享一个 GitHub 库，但是它完全是为我的项目定制的。我计划创建一个通用版本，希望能和我的下一个 NFT 项目一起分享。

我开始寻找用于图像合成的潜在 NodeJS 库，我遇到了用于 node 的 [**GraphicsMagick。总的来说，除了不重要的痛苦时刻，我对它很满意。您可能会在**](https://github.com/aheckmann/gm) **[GraphicsMagick 编程接口列表](http://www.graphicsmagick.org/programming.html)中找到您喜欢的语言。否则，我祝你好运找到一个合适的，我相信你可以。**

每一个标记，也就是艺术品，都需要一个 JSON 对象作为它的元数据。它最基本地包含了令牌`name`、`description`、`image`(图片 URI)和一个`attributes`数组(稀有表正在运行)。对于元数据标准，我遵循了 OpenSea 上的文档以及现场项目的各种元数据。

到目前为止，我创建的逻辑，最简单的版本是:

*   从 Excel 文件的稀有度表中获取性状及其权重百分比。
*   创建 11，111 个具有随机选择特征的唯一 JSON 对象。
*   从这些 JSON 对象中生成 11，111 个唯一的图像。
*   从 JSON 对象创建相应的元数据，并编写一个文件。(在这里，我决定不使用**。json 扩展**。它简化了智能合约功能，我将在后面的*部署智能合约)*中详细介绍

所有的都在那里:11，111 张图片和 11，111 个元数据文件。但只要他们还在我的本地车道上，我就肯定不会罢休。

# 存储艺术品和元数据

如果你不熟悉，有两个选项来存储你的图像和元数据。链上，在智能合约本身中，或者链外，具有分散存储，是 [IPFS](https://ipfs.io) 。我决定使用使用这个协议的 Pinata 。

但首先，一些定义。

当你在 Pinata 上上传文件时，你会得到一个 CID，比如`QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1x24b8FILE`。

文件 URI 是`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xFILE`。

当你上传一个文件夹并从`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA`到达时，你会得到一个 CID。

如果这个文件夹中有一个名为 **1** 的元数据文件，那么这个文件的 URI 就是`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA/1`

这里，

*   **CID** 是`QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA`
*   **令牌 URI** 是`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA/1` (所以整个 URI)

我在上一个主题的逻辑中添加了另一个步骤:使用 [Pinata 的 API](https://docs.pinata.cloud) 逐个上传图像，获取相应的图像 CID(这是 IPFS 上该文件的唯一标识符)，使用该 CID 更新元数据，并再次将元数据上传到 Pinata。然而，这是一个错误，因为我没有考虑清楚。我得到了 22，222 个 cid。所以我完全放弃了它，把逻辑改成了这个。

*   将整个图像文件夹上传到 Pinata。现在，可以使用图像文件夹 CID 后跟/1.png 等来提供图像。
*   获取图像文件夹 CID，并运行另一个脚本来更新本地元数据文件中的**图像**属性。因此元数据指向相应的图像 IPFS·URI。
*   将整个元数据文件夹上传到 Pinata。以便可以通过元数据文件夹 CID 后跟/1 等来访问元数据。我必须再次指出，这里没有文件扩展名。

集中式存储违背了整个分散逻辑，因为它依赖于服务器。但我最终决定，在铸造过程中，将它们暂时存放在集中存放处。这是为了防止人们在制造令牌之前看到令牌的详细信息(当一个元数据 URI 是公共的时，所有其他的也可以被查看)。使用相应创建的智能合约，可以更改令牌 URI。也就是说，这些文件将从集中存储提供服务，并最终从 IPFS 提供服务。对于[突然独角兽](https://www.suddenlyunicorns.com)，文件也已经在 IPFS 了，只是还没有公开。但是稍后，在*下部署智能合同* **)** 。

资产被存储，是时候和区块链互动了。

# 部署智能合同

## 基础

这可能是最重要的部分。我的重点是以太坊从一开始，尽管天然气价格，我不打算在这里比较不同的区块链。

对于以太坊，你将需要接触到 [Solidity](https://docs.soliditylang.org/en/v0.8.12/) ，这是一种受 JavaScript、C++和 Python 启发的编程语言。作为一个之前有一些 C++知识的 JavaScript 开发人员，这是一个相当平稳的过渡。但这可能是因为有大量的资源和真实的例子可以让你检查和比较你的代码。所以我遇到的每个问题都有解决方法。

在我们继续之前，我强烈建议完成本教程。

[](https://docs.alchemy.com/alchemy/tutorials/how-to-create-an-nft) [## 如何创建 NFT 教程

### 本教程将引导您使用以太坊编写和部署一个不可替换的(ERC721)令牌智能合约…

docs.alchemy.com](https://docs.alchemy.com/alchemy/tutorials/how-to-create-an-nft) 

它会让你熟悉大量的工具和概念。我不想说得太详细，因为都在那里，所以我只能给你总结一下。在这些教程中，您将:

*   开立一个[炼金术](https://dashboard.alchemyapi.io/)账户，使用他们的 API 与以太坊区块链互动。
*   安装[元掩码](https://metamask.io)，一个加密钱包浏览器扩展，并为自己创建一个以太坊账户(即你的钱包)
*   使用 [Hardhat](https://hardhat.org/getting-started/#overview) 创建一个项目，这是一个编译、部署、测试和调试以太坊软件的开发环境。
*   编写一个契约，并将其部署到一个 [testnet](https://en.wikipedia.org/wiki/Testnet) (他们使用 Ropsten，但我建议使用 Rinkeby，这样您就可以在[OpenSea testnet](http://testnets.opensea.io)上看到您的测试令牌和其他细节)
*   使用 [ethers.js](https://docs.ethers.io/v5/) ，一个用于与以太坊区块链交互的库，与你部署的契约进行交互。
*   了解如何在 [Rinkeby Testnet](https://rinkeby.etherscan.io/) 或 [Ropsten Testnet](https://ropsten.etherscan.io/) 上查看您的合同和交易详情
*   铸造 NFT

这会让你对这个过程有一个总体的概念，并为接下来的步骤做好准备。

## 具有基本功能的智能合同

现在，是时候创建一个合适的智能合同了。在教程中只可能铸造一个令牌，它期望令牌 URI。但这对于我的收藏和我的体型来说是不可行的。我需要一个具有更多功能的智能合同。

它必须:

*   铸造多个代币
*   拥有最大数量的代币
*   设置代币价格、每笔交易的最大铸币限额和销售状态(启用或禁用)
*   包含铸造令牌的条件(对于上述值)
*   跟踪令牌计数
*   获取特定所有者的令牌
*   取出余额(你能想象忘记这一点吗)
*   为所有者保留代币

另外，由于我们是离线存储数据的，所以它必须处理`baseURI`。

那么什么是`baseURI`？

还记得之前的例子吗，令牌 URI 是`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA/1`？

**基础 URI** 在那个例子里是`https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA/`，所以基本上这里的文件夹是 URI。

因此，您需要在智能契约中使用**那个** baseURI，您可以为它提供一个`baseTokenURI`变量、一个用于设置它的`setBaseURI(...)`函数以及一个用于覆盖继承的`_baseURI()`函数的函数，以便它返回您的`baseTokenURI`。

```
string public baseTokenURI = “”;function setBaseURI(string memory _baseTokenURI) public onlyOwner {
    baseTokenURI = _baseTokenURI;
}function _baseURI() internal view virtual override returns (string memory) {
    return baseTokenURI;
}
```

部署完契约，就可以调用`setBaseURI(“https://gateway.pinata.cloud/ipfs/QmSfotcs6fRVQyf6hEKBhddQtetiFbrc49Eo1xMETADATA/"`。或者您可以在部署时直接在构造函数中调用它。当令牌被制造时，令牌 URI 基本上将是与新制造的令牌的`tokenId`连接的`baseTokenURI`。这就是我没有用 JSON 扩展名存储元数据文件的原因。契约更简洁，没有额外的字符串变量存储扩展，我们有一个更简单的连接。

但是有一个问题。当 baseURI 已知时，它是一个开放的自助餐。每个人都知道下一个代币会是什么，惊喜的元素被破坏了，这不再公平了。我将在下一个主题中讨论这个问题。基本的功能应该首先都在那里。

以下是智能合约示例和教程，您可以在创建自己的智能合约时进行检查，涵盖了上述要求。

[](https://dev.to/rounakbanik/writing-an-nft-collectible-smart-contract-2nh8) [## 撰写 NFT 可收集智能合同

### 在我以前的教程中，我们向你展示了如何使用我们的生成艺术库来创建一个头像集…

开发到](https://dev.to/rounakbanik/writing-an-nft-collectible-smart-contract-2nh8) [](https://github.com/HashLips/hashlips_nft_contract/tree/main/contract) [## hash lips _ NFT _ contract/主 HashLips/hashlips_nft_contract 处的合同

### 一个简单的 NFT 智能合同，与 HashLips 生态系统的其余部分一起工作。-hash lips _ NFT _ contract/contract at…

github.com](https://github.com/HashLips/hashlips_nft_contract/tree/main/contract) 

要考虑的最重要的事情是让你的代码尽可能紧凑。这有两个原因:

*   更少的代码意味着更少的错误。当您部署到处理金融资产的不可变数据库时，bug 是相当大的问题。作为一名使用 sprints 并偶尔进行修补的开发人员，这个事实让我很担心。
*   紧凑的代码，加上一些其他的最佳实践，将会节省你的[汽油](https://ethereum.org/en/developers/docs/gas/)。你和铸造代币的人都会从中受益。

现在来处理我之前提到的 baseURI 问题，以及令牌分发和公平性最佳实践

## 具有附加功能的智能合同

从用户的角度来看，铸造是随机的，只有你知道下一个会是什么。但是当你的 baseURI 是公共的，用户也知道，它是开放的。在智能契约的当前实现中，baseURI 在设置时确实是公共的。

这里有多条路可以走，这是一个很大的主题。我更喜欢写一篇涵盖其他内容的完整文章。但在这里，我将把重点放在我最终决定要做的事情上。

*   我创建了一个 AWS 桶。创建了一个**元数据**文件夹，用于存储 11，111 个没有属性的虚拟元数据。只有`tokenID`和`name`是动态的，它们都指向一个通用图像

```
{
  “tokenId”: 1,
  “name”: “Suddenly Unicorns #1”,
  “description”: “This Suddenly Unicorns token cannot wait to be unlocked”,
  “image”: “https://suddenlyunicornsnft.com/unrevealed/suddenlyunicorns.png",
  “external_url”: “https://suddenlyunicorns.com",
  “attributes”: []
}
```

*   我创建了一个空的**图片**文件夹。

当令牌生成后，我用包含 trait 属性的实际元数据替换元数据，并将相应的图像文件添加到 images 文件夹中。我承认这是体力活，但对我的第一个项目来说感觉更安全。这是一个“几乎即时”的令牌揭示(从显示一个普通的图像和空的特征属性，到显示实际的图像和实际的特征属性)

因此，即使 baseURI 是公共的，也没有未铸造令牌的细节。当所有的令牌都被铸造或经过一段时间后，您可以将 baseURI 设置为实际的 IPFS URI。

我尊重这个社区，尊重我的项目，尊重我自己。我没有看到一个所有代币都是铸造出来的世界，所以我确定我之前会这么做。我还不知道什么时候是最合适的时候，但我会更改 **baseURI。**也许这是社区将决定的事情。

并在顶部添加樱桃以确保铸造过程的公平性— **出处散列。**

我觉得这是一篇精彩的文章。但是你已经知道了，我给你总结一下。

[](/coinmonks/the-elegance-of-the-nft-provenance-hash-solution-823b39f99473) [## NFT 出处散列解决方案的优雅

### 它是如何工作的以及为什么重要

medium.com](/coinmonks/the-elegance-of-the-nft-provenance-hash-solution-823b39f99473) 

我从来没有想过，合同所有者必须证明，硬币分发没有什么好笑的。直到我熟悉了出处散列。想想看，你不能相信在铸造过程开始后，我不会随心所欲地改变代币的顺序。我必须证明在铸造开始前订单是预先确定的。但是怎么做呢？

> 输入出处散列

简单总结一下，您可以使用 SHA-256 散列法分别对图像进行散列，按照与相应令牌 id 相同的顺序连接这些散列字符串，然后再次进行散列。这为您提供了出处哈希，您可以在铸造开始之前在智能合同中设置它。我更喜欢在构造函数中完成。一个`PROVENANCE`变量和一个`setProvenanceHash(_provenanceHash)`函数就足够了。我还决定将图像的散列字符串作为令牌的一个单独的元数据属性。感觉很好。

现在，如果你仅仅改变一个图像的顺序，结果出处散列将会不同。这意味着在这个过程中顺序改变了。可耻。

关于分配公平还有一件事要提。所有合同都有每笔交易的最大代币数量限制。在阅读了一些关于一些所有者在一个项目中有太多硬币以及它如何造成一个不平衡的社区的批评后，我决定也为每个所有者设置一个限制。所以这既是对每笔交易的限制，也是对[突然变成独角兽](https://www.suddenlyunicorns.com)的每个所有者的限制。

我还用 Mocha 设置了测试，但是考虑到它是可选的，我将跳过这一部分。但我强烈建议。你必须反复测试你的合同，直到你可以放心地将它永久部署。

我能够从控制台与我的合同进行交互。但我不打算为每个想铸造我的代币的人设置相同的环境。因此，一个拥有全新功能的老网站是下一步的目标。

# 建设铸造的 DApp

当然，你可以决定在 [OpenSea](https://opensea.io) 、 [Rarible](https://rarible.com) 或其他市场上创建一个集合，并在那里出售代币。但是这并不像你预期的那样实际，因为上传这么大的收藏只有变通方法。其他的都是我自己做了以后才考虑的，但是你可以找到合适的方式。

> 在撰写本文时，OpenSea 上的黑客攻击正在发生。我没有足够的知识来评论这些的合法性，或者是否是 OpenSea 的错。但是必须包括这条信息。

对我来说，创建一个网站更有趣——一个任何人都可以铸造代币的铸造 DApp。唯一需要的额外库是 [ethers.js](https://docs.ethers.io/v5/) 和 [web3.js](https://web3js.readthedocs.io/en/v1.5.0/) ，以与您的智能合约交互。为了连接到用户的钱包，[元掩码](http://metamask.io)和 [WalletConnect](https://walletconnect.com) 是一些选项以及各种其他选项。我只选择了 MetaMask，因为它很简单，而且我知道它很常见。

我不是 React 开发人员，但它或多或少是 Web3 的标准。我过去已经试验过了，所以这是一个再次尝试的借口。有各种铸造网站教程和样本库。在尝试了其中一些之后，我发现[这个资源库](https://github.com/alchemyplatform/nft-minter-tutorial)，是 [create-react-app](https://create-react-app.dev) 的一个变种，由 Alchemy 创建最舒服。

[](https://docs.alchemy.com/alchemy/tutorials/nft-minter) [## NFT 明特教程:如何创建一个完整的堆栈 DApp

### 在本教程中，您将构建一个 NFT minter，并学习如何通过连接您的智能…

docs.alchemy.com](https://docs.alchemy.com/alchemy/tutorials/nft-minter) 

我按照上面的步骤操作，基本的功能就在那里了。该应用程序包括一个具有元掩码的钱包连接功能，以及一个具有三个字段的表单:图像的 IPFS URI，以及名称和描述字段。在提交时，用这三个创建一个元数据 JSON，它被上传到 Pinata，返回的令牌 URI 被用来铸造令牌。

![](img/28f4128d0c33bce6b27d0847041ed7b1.png)

Alchemy NFT Minter Form

这是一个伟大的开始，但我有很长的路要走，以调整它为我的项目。我删除了所有 Pinata 功能和所有表单字段。并做了适合多次造币的更改:即添加两个按钮来增加/减少总计数，根据总计数计算总成本，将其包含在交易参数的`value`字段中，最后将令牌计数作为唯一参数传递给智能合约造币函数。

![](img/83d22328cbca9a483935189cdb31c346.png)

Suddenly Unicorns Form with Initial Styling

然后是我最喜欢的部分，也是我最舒服的部分。样式、动画、增加的用户友好性逻辑、增加的移动功能等等。

即使当我正在完成网站的一半时，我也不会有那种平静的心情，除非我看到它在直播。

# 部署铸造 DApp

我用 [AWS Amplify](https://aws.amazon.com/amplify/) 为 app 服务。我更新了那里的环境变量。我以为我已经快完成这个应用了，但有些事情困扰着我。通过一些研究，我发现 create-react-app 上的环境变量(也包含我的 Alchemy API 密匙)被嵌入到构建中，并且它们是可公开访问的。

> 快速建立一个 [Heroku](http://heroku.com) 应用程序，并在那里移动铸造逻辑的一些部分(特别是创建交易参数)。AWS 在免费层上提供 NodeJS 应用时不如 Heroku 实用。

虽然我没有采纳他们的建议，但我仍然建议查看一下关于部署的[炼金术文档。](https://docs.alchemy.com/alchemy/tutorials/nft-minter/how-do-i-deploy-nfts-online)

开发完成了。我已经生成了图像并创建了元数据。我在 AWS 上为他们服务，也把所有东西上传到 IPFS。我完成了智能合同，并创建了一个网站来铸造它们。

现在怎么办？

# 营销

但是你说不会有营销。

嗯，没有，因为我现在正处于这一步。

我目前所做的是:我写了这篇文章，我创建了一个 [Discord 服务器](https://discord.gg/PSXp9MeBtn)，两个 Twitter 账户(一个用于[突然独角兽](https://twitter.com/SuddUnicornsNFT)和一个[个人账户](https://twitter.com/ardaduraketh)，以及一个 [Instagram 账户](https://www.instagram.com/suddenlyunicorns/)。我正在想办法解决这个问题，并且可能会得到支持。

但我就快成功了，这很有趣。

# 额外资源

我想分享一些对我帮助很大但不随波逐流的资源。

这篇我看了好几遍，后悔看晚了。这很有启发性，也帮助我构建了这篇文章。当我参与到[多边形](https://polygon.technology)中时，我创造的第一个符号将来自这个项目。

[](/technest/how-to-launch-an-nft-project-by-yourself-252a7fefa748) [## 如何自己启动一个 NFT 项目

### 创建 10，000 个自动生成的艺术品，将智能合同部署到以太坊/多边形区块链，设置…

medium.com](/technest/how-to-launch-an-nft-project-by-yourself-252a7fefa748) 

这是第一篇文章，后面还有许多文章。它们只是提供了整个过程的清晰概述和详细内容。

[](/scrappy-squirrels/tutorial-create-generative-nft-art-with-rarities-8ee6ce843133) [## 教程:用稀有物品创造 NFT 艺术

### 介绍

medium.com](/scrappy-squirrels/tutorial-create-generative-nft-art-with-rarities-8ee6ce843133) 

# 关于我

再说一遍，我是 [Arda](https://linktr.ee/ardadurak) 。

我是一名十多年的软件开发人员。其中四家公司的电子商务前端开发商。我对软件开发并不陌生，但我擅长创建在线形象。我个人或专业上从未享受过，但这个项目需要我更加积极，我可能会喜欢它。如果你正在读这篇文章，我很想知道你读了，并感谢你的鼓励。所以我乐于接受问题、建议和反馈。

我只是希望你在这次冒险中一切顺利，并希望你能享受和忍受。

如果你厌倦了[突然出现独角兽](https://www.suddenlyunicorns.com)，你可以跳过这最后一部分。

# 突然独角兽，又一次，但带有普通的语气

[](https://www.suddenlyunicorns.com/) [## 突然独角兽集合-以太坊区块链上 11111 个唯一的 NFT

### 探索以太坊区块链上的突然独角兽收集和薄荷独特的 NFT。您可以查看项目详情…

www.suddenlyunicorns.com](https://www.suddenlyunicorns.com/) 

突然之间，Unicorns 变成了一个社区驱动的实验项目。我女儿是我选择独角兽的最大灵感。这是一个很大的乐趣，创造这一点，我希望与人们分享谁发现它同样有趣。

每个独角兽都有独特的特点和配件。铸造它们，它们就会变成现实。他们中的一些人带着一个**小**惊喜而来。最稀有的是，这里有五种类型的**稀有独角兽**，它们迫不及待地想要解锁。