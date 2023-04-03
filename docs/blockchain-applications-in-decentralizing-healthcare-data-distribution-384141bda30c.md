# 区块链在去中心化医疗数据分发中的应用

> 原文：<https://medium.com/coinmonks/blockchain-applications-in-decentralizing-healthcare-data-distribution-384141bda30c?source=collection_archive---------42----------------------->

为什么医疗保健数据的控制很重要

![](img/d6c98f8bf377c6e274c67fb97a2dbafa.png)

Photo by [Clint Adair](https://unsplash.com/@clintadair?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

目录

1.  [区块链和 NFTs 简介](#da37)
    [1。问题陈述](#8b13)
2.  [医疗保健领域的传统模式
    1。医疗保健数据使用示例](#29b9) [2。非基于区块链的系统](#b843) [3。国家医疗保健系统。商业视角](#126d)
3.  [区块链模型](http://"d76b) [1。利用 NFTs](#9379) [的项目 2。医疗保健供应链管理项目](#931a)
4.  [理论方案设计](#451e)
    [1。对医疗保健 NFTs](#3838) [2 的改进。现金流](#3fbb)
5.  [讨论](#a831) [1。集中控制](#8a78) [2。身份整合](#6d7d) [3。安全问题](#05ab)
6.  [结论&未来工作](#4bd2)
7.  [参考文献](#6b1b)

# **1。区块链和 NFTs 简介**

Blockchain can be defined as having the unique properties of immutability, transparency and anonymity [7]. Blockchain is used for a wide variety of projects such as cryptocurrencies, Internet of Things as well as tokenizing art and intellectual property ownership [9].
The main components of a Blockchain includes a peer-to-peer network, which is a set of nodes that can read and write transactions on the blockchain; and a consensus protocol, which is a set of rules that determine how new transactions are added to the Blockchain. The security of the Blockchain is also paramount to its success and therefore the features of it being tamper proof are very important so that it is very easy to verify whether transactions have been manipulated after their recording or not. It should also be able to ward off any attempts to tamper with it adequately [7]. Blockchains can be either public or private [9]. In this case “Public” means that the record of transactions as well as the consensus protocol are open to anyone. To counter the lack of control on users public Blockchains must have conditions that prevents the participants form any malicious activity. As an example, in proof of work (PoW) based Blockchains (such as Bitcoin and Ethereum) this is achieved by requiring the users to use their computational power to solve a cryptographic puzzle to be allowed to append the new block (i.e., new set of transactions) to the Blockchain. Both Bitcoin and Ethereum, which are the most well known Blockchains today, use proof of work but this results in a low transaction speed and consumes lots of energy. Another consensus method that is commonly used by Blockchains today is called proof of stake (PoS). It is an alternative that does not use as much energy and instead uses economic rationality. A random process selects an entity to append the next block to the Blockchain from among the entities that stake the crypto currency [7]. Private Blockchains use classic authentication mechanisms and are used by corporations and banks. However, such implementations come at the cost of violating the for the most part, Blockchain trustlessness and decentralization compared to public Blockchains. Private Blockchains therefore result in greater speed of transactions as their consensus protocol does not have to be based on hard mathematical cryptography [7].
The non-fungible token (NFT) has been used for a variety of use cases as of 2021\. NFTs represent ownership rights to a unique digital or real-world asset and are issued on the Blockchain. They can be used to make it more difficult for digital creations to be copied and shared by proving ownership through the Blockchain transactions. They have also been used to issue a limited number of digital assets which has primarily included artworks that have retained skyrocketed in value through scarcity [9].
There are both fungible as well as NFT creation standards that have been implemented. Fungible tokens are not unique and thus divisible and an example is money. NFTs are unique and technically not divisible and an example of such is an original art painting that retains its value despite duplications. Hundreds of thousands if not millions of dollars have been used to purchase NFTs. By may 2021 about 34 million United States dollars had been spent on NFT sales [9]. However by the end of 2021 about 25 billion United States dollars had been spent on [NFT sales](https://tinyurl.com/yw6578fe). That is an incredible amount of growth and but there are signs that it is slowing down to a certain extent. The technologies of the NFTs are still immature however the ecosystem and use cases have been growing at a great speed. The NFT was initially created from the ERC721 token standard of Ethereum which designates each token as unique and distinct [9]. This makes the token ideal secure digital property rights and for users to trade those digital properties. This could perhaps also extend to the trading of electronic health records by the owners of the records. There are legal pitfalls regarding the use of NFTs when it comes to the limitations of the governments enforcing an individuals ownership of their digital property [9]. This is because the governments do not currently use Blockchain as evidence of proof of ownership.
A Blockchain solution instead of a traditional database is not always the right choice for the storage and validation of data because is an energy inefficient way to store data [3]. When data must be kept confidential and all the participants are registered and authenticated users then a Blockchain is not needed [7]. Blockchain solutions are best used when a decentralized solution is required to mediate between trustless entities.
There are many different ways with which Blockchain based startups decide to raise funds for development. Initial coin offerings (ICOs) have declined and been replaced by Initial exchange offerings ([IEOs](https://coinmarketcap.com/alexandria/article/what-is-an-ieo)) which are more scrutinized forms of fund raising where an exchange oversees the process of selling the tokens and projects have to submit white papers that are held to a certain standard. Initial decentralized-exchange offerings ([IDOs](https://coinmarketcap.com/alexandria/glossary/initial-dex-offering)) are a cheaper and less stringent alternative to IEOs which utilize decentralized exchanges that do not demand sums of payments and exclusive availability of the token on only that exchange.

**1.1 问题陈述**
在过去几年中，可公开获得的医疗保健数据量呈指数级增长，这为生物信息学和商业研究带来了前所未有的可能性。区块链技术同样在应用方面取得了很大进展，也吸引了大量的金融关注。分布式账本技术、令牌化和分散融资的机制也为患者提供了重新控制其医疗数据以及将其访问货币化的机会。区块链有可能彻底改变医疗保健数据管理。
在这个项目中，我们将分析医疗保健数据和区块链技术交汇处的创业努力，以及这些项目如何利用不可伪造的令牌和分散金融机制等技术来跟踪和/或货币化数据。将剖析项目的可行性及其面临的挑战，并提出改进建议。未来的机会也将被理论化和探索。
总而言之，本研究的主要研究问题是:

> 区块链系统能在多大程度上有助于医疗数据去中心化共享？
> 基因组数据能否通过区块链金融方面进一步货币化？

为此，在第 2 节中，我们调查了医疗保健数据交换的状况，即它在发达国家使用传统数据库而不使用区块链技术的工作方式。在第 3 节中，我们描述了不同类型的前沿区块链解决方案，这些解决方案通过供应链管理以及 NFT 及其市场，在医疗数据共享及其货币化的交叉点上运行。在第 4 节中，我们提出了一个改进的系统，它建立在第 3 节中提到的项目的基础上，并对其进行了改进。在第 5 节中，讨论了关于缺陷和可能的解决方案以及未来可能发生的改进的不同关注点。

# 2.医疗保健中的传统模式

**2.1 医疗保健数据使用示例** 为了举例说明医疗保健数据的使用，有必要说明医疗保健数据通常是在患者就诊、描述其症状和社会经济状况以及对其内部和外部状况进行体检时，通过诊所和医院生成的。由此收集的数据存储在患者日志中的电子健康记录系统中，可能包括医生就诊记录、血液测试结果、疫苗接种结果、药物和处方药物等。在一些医疗保健系统中，患者的基因组也可以存储在患者日志中，在患者患有遗传疾病的情况下，这对于患者的治疗是必不可少的。
可以通过替换或审查姓名和地址等数据的某些部分来匿名化这些数据，这使得跟踪或识别患者变得更加困难。一旦数据被匿名化，它可以被转移到与诊所或医院有协议的某些方或公司。数据传输可能需要符合 GDPR(通用数据保护法规)的要求，具体取决于数据传输所在的国家/地区，以及数据即使被匿名化，是否仍被视为属于患者，因此可能需要相应患者的同意。如果卫生保健提供者打算分发数据，并且从一开始(在治疗之前)就计划好了，那么有可能所有患者都要签署一份声明，声明如果他们要接受治疗，他们同意任何未来的匿名卫生保健数据传输。由于医疗服务提供者能够拒绝治疗，在治疗前获得同意在心理上具有更高的成功概率。当医疗服务提供者重新分发数据时，购买数据的利益相关者可以向他们支付费用。当涉及基因组数据、医院效率和疾病跟踪以及医疗保健数据等用途时，利益相关方可以使用这些数据进行药物研发研究。保险公司甚至可以使用它来确定哪些类型的患者可以住院，并更多地要求他们的保险，这可能导致公司对他们为这些患者提供的服务收取额外费用。从医疗保健数据中获得的见解在决策中具有各种类型的用途，从保险单确定和贷款偿还概率，到确定针对易受某些流行病影响的人群采取哪些公共安全措施。

**2.2 基于非区块链的系统** 医疗保健领域的诊断和实际临床决策需要高标准的数据共享。它可以用 SSS(安全、可靠以及可扩展)的缩写来概括[6]。共享数据的方式对于确保将与患者相关的数据快速传输到需要的地方(可能是患者当前即将接受治疗的地方)至关重要。卫生保健工作者和医生必须能够以保密和有效的方式发送临床患者数据，以便患者总是基于他们最新的健康状况接受治疗。远程医疗和电子医疗属于医疗保健领域，在这些领域中，数据被发送给相应的相关专家以获得专家意见，而患者的当前医生将无法接收这些数据。在这些在线临床状况的领域中，可以通过不同的方法发送患者的数据，例如存储转发技术，或者基于在线实时临床监测的技术，其中可以包括远程监测。患者可以远程诊断，同时由专家进行治疗。敏感性、安全性以及隐私非常重要，因为数据非常敏感。除了前面提到的问题，还有互操作性的挑战。这是因为在实践中共享数据时，利益相关者和相关方之间需要大量的合作。数据共享协议、患者匹配和分层算法、伦理和管理规则只是所有各方在临床数据共享能够顺利进行之前需要同意的一些重要问题，以便电子健康在实践中发挥作用[6]。实施应用新的和即将到来的技术，如人工智能/机器学习，IT 和认知以及物联网在临床环境中的应用，以帮助医生[6]。
电子健康记录(EHR)系统是医疗保健系统的关键组成部分，医疗保健系统由大量不同的健康相关系统组成，包括处方系统、健康信息交换系统和临床决策支持系统[4]。在未来，这些系统还可以部署实时临床人工智能模型。EHR 系统如何工作的一个例子是，医生如何将访问过 EHR 系统的患者的症状记录下来，然后使用该系统给患者开出患者能够在当地药店购买的药物。该记录以及开处方的原因将存在于 EHR 系统中。
临床信息学和生物信息学是有区别的。临床信息学包括支持医疗保健服务的技术，而生物信息学是优化和分析生物医学数据以改善医疗保健的方法的开发[1]。
随着针对个体患者进行特定治疗的个性化精准医疗变得越来越普遍，临床信息学也在不断扩展。需要有关电子医疗和健康记录的培训和专业知识，以使整个过程更加有效，并确保资源和规模经济可以促使技术成熟[1]。
生物信息学仍然主要基于研究，但由于世界范围内产生的生物数据越来越多，它已经呈指数级增长。生物信息学的重点过去是收集数据，但现在已经转移到管理和分析已经可用的数据，这些数据随着生物实验和电子医疗记录呈指数级增长[1]。基因组分析的成本也已经下降，到 2022 年成本将低于 300 美元，这导致了大量基因组数据的产生，这些数据可用于研究遗传疾病，并帮助制药公司开发针对董事会成员基因的药物，以提高药物有效性。生物信息学和临床信息学可以集成到电子医疗记录中，以提高精准医疗，并允许两个领域的见解相互启发，缩短新实验室发现的临床应用时间。[1].

**2.3 国家医疗保健系统** 世界各地有许多不同的电子医疗保健系统在使用，对于电子健康记录以及此类记录应包含的内容，没有统一或广泛接受的定义[4]。已经部署了许多国家 EHR (NEHR)系统。NEHRs 需要能够与其他医疗保健提供商开发的其他 EHR 系统互操作[4]。在欧洲国家中，到 2017 年实施 NEHR 的领先国家是丹麦、瑞典、荷兰和瑞士，而其余国家面临挑战，仍处于规划阶段。当时面临挑战的国家有挪威、德国和奥地利[4]。在欧洲之外，澳大利亚、新西兰和以色列被认为是世界上 NEHR 实施情况最好的国家之一，而韩国和加拿大正在其公立医院迅速实施更多的 EHR[4]。
丹麦在其医疗保健系统的各个部门使用信息技术[2],是世界上医疗保健服务领先的国家之一。每个病人都有独特的电子个人识别码，以及与该国所有医疗保健数据库集成的健康卡。市政当局和地区有健康协议，所以他们可以协调医疗保健在一起[2] [4]。可以说，丹麦的医疗保健是在国家一级管理的，而且相当集中。总的来说，许多国家都有 EHR 系统，但它们之间的互操作性很低，尤其是在医疗保健提供商具有政治导向关系的情况下。与这些国家的保险提供商的互操作性也很低。许多国家使用公民号码作为患者的唯一标识符，即使如此，许多国家也没有通用的患者标识符[4]。

**2.4 商业前景** 医疗保健行业规模庞大，价值约 8.3 万亿美元，大型科技公司也对此感兴趣，并在 2020 年初投资了约 68 亿美元。由于能够从对社交媒体的控制中解析出大量数据，大型科技公司已经拥有大量可用数据。包括 facebook、谷歌、亚马逊和微软在内的大型科技公司可以访问高级分析，这使他们能够理解他们拥有的数据。也有非正统的解决方案，如虚拟现实和 oculus rift，正在帮助培训医护人员[8]。
据估计，人均医疗保健数据的价格约为 1000 美元。如果每个患者的医疗保健数据通过区块链技术转换成 NFT，然后许可或出售给希望利用和分析它的实体，这可能会产生巨大的影响[8]。
许多初创公司正在进军医疗保健行业，并一直在创建医疗保健市场。这是由于医疗保健，即使匿名化可以获得一个巨大的价格。像辉瑞这样的制药公司每年花费一千多万美元从不同来源获取医疗保健数据。Segmed 等医疗保健数据市场已经获得了数百万美元的种子资金。另一家名为 Burstchain 的公司目前已经在 600 多家医院中使用大数据，但它是一种基于区块链的解决方案，因此将在相应的章节中详细阐述。

# 3.区块链模型

区块链技术可以通过几种不同的方式降低全球医疗保健系统的成本。方法之一是减少官僚主义的繁文缛节，因为由于低效的保险结构、官僚主义以及基于债务和通货膨胀的财政政策，医疗保健成本的很大一部分膨胀了[5]。通过利用区块链的功能，使医疗记录可供许多医疗保健提供商和电子医疗保健系统使用，可以降低医疗保健的价格。这将通过利用区块链技术的去中心化和金融性质来实现，区块链技术是不可信的和通货紧缩的。医疗保健的成本将更多地与绩效而不是分配不当联系在一起[5]。EHR 可以通过加密的 IPFS 存储在 NFT 上，这将导致不可变的记录，这些记录由于与正确的患者相关联而被确认为真实的，并且是不可伪造的，因此对于患者是唯一的，这也解决了许多 EHR 系统没有通用患者标识符的问题。
许多参与[个人基因组学的私营公司将他们的数据货币化](https://tinyurl.com/2mxw3x48)，而患者和用户无法从中受益，因此没有得到补偿。然后，数据的所有者可以设置数据共享规则和权限。像 Oasis network 这样的网络正在开发一些功能，允许用户有选择地向愿意付费获取数据的第三方授予许可。可能会有人担心医疗数据的货币化会导致数据价格上涨，从而使研究人员难以用有限的资金支付数据费用。然而，货币化的方式仍然可以工作，这与通过大学等组织支付研究论文的方式是一样的，大学已经为通过某些网站和期刊提供的所有研究论文预付了费用。这将使大量资金能够支付医疗数据。

**3.1 利用 NFTs 的项目** 许多基于区块链的医疗保健平台已经出现，允许人们利用他们的医疗保健数据赚钱。在这些市场中，EncrypGen 发布了一种名为 DNA 的令牌，该令牌也旨在允许个人将其基因组数据用于研究，同时从中获利。另一家这样的公司是 Longenesis，这是一家基于人工智能医疗保健的公司，也是一个开放的健康网络，消费者可以将他们的医疗保健数据货币化，并利用人工智能和大数据分析增强的产品[8]。
aime dis 是一家总部位于 NFT 的医疗保健货币化解决方案公司，最近推出了 IEO()并实施了一个医疗保健平台，该平台将作为 NFT 市场。他们建立了第一个医学和科学 NFT 市场，名为 DataXChange，每个 NFT 的价格可以高达每个 NFT 几千美元。他们的 NFT 还包含所有类型的数据，包括与患者相关的药物、研究以及社会经济数据。他们的解决方案是基于这样一个事实，即感兴趣的各方将能够直接从平台上出售和购买数据，然后使用这些数据。他们允许同一 NFTs 的多个所有者，这样利益相关者将能够协同使用数据。数据提供者也将受到激励，通过从 NFT 的销售和使用中获取费用来继续托管和/或铸造 NFT。NFTs 的安全性是通过私有访问密钥来维护的，该密钥在数据被转售时重新生成，并且该私有密钥只允许当前的购买者访问数据。NFT 被加密并存储在 Aimedis 的私有[区块链上。Aimedis 实现的令牌也应该通过使用 NFTs 来获得，并且该令牌将能够被下注，从而允许获得 NFT 奖。](https://aimedis.io/aimx-nft-blockchain)

**3.2 医疗保健行业的供应链管理项目** 还有一些公司负责管理与数据及其所有权相关的控制链。BurstIQ 就是这样一家公司。Burstchain 是由 BurstIQ 公司构建的另一个基于区块链的系统，该系统目前在美国与 600 多家医院合作，并提供医疗保健数据监管链的权限管理，其中还包括可撤销的同意以及数据的粒度所有权。他们创建的平台可以使数据共享，而不管其大小如何，从一个数据点到 Pb 级的非常大的数据集，并且共享的数据可以以有条件和基于触发的方式撤销其权限。多维区块链可以通过这些方法创建，这些方法可以在系统效率和健康之间形成相互依赖[8]。

# 4.理论项目设计

在上述区块链平台上扩展的项目的一个可能提案是 NFT 的可能细分和清算。目前，非金融资产是以固定价格出售的，它们必须作为整体出售，在某些情况下价值数千美元，因此它们缺乏流动性，财富被截留在其中，不能很容易地用于其他目的。当包含医疗保健和社会经济数据的医疗 NFT 在未来具有确定的价值，并且可以作为资产发挥作用时，允许释放资产中的非流动性财富是很重要的。实现这一点的方法之一是将 NFT 的不同部分进行细分，然后将这些部分分别出售或出租给想要它们的不同利益相关者。在图像 NFT 的情况下，细分是将 JPEG 或 PNG 文件的部分分割成小块，而在医疗保健 NFT 的情况下，细分是将数据列表分割成更小的相关列表(社会经济数据、疾病数据、医疗处方数据)。
该提案的一个例子是将 NFT 的社会经济部分出租给社交媒体或保险公司，将基因组学和医疗保健部分出租给生物信息学研究小组。与租用整个 NFT 相比，NFT 各部分的总租金可更准确地估算 NFT 的真实价值，因为它提供了某些利益相关方所需的 NFT 部分。
一旦 NFT 的价值被确定，就有可能开发一个区块链平台 smartcontract，允许数据提供商以各自的 NFT 为抵押获得贷款，从而将 NFT 的所有权作为平台的抵押品。只要 NFT 归平台所有，通过转售和使用 NFTs 积累的任何租金、订阅费和费用都由平台而不是作为数据提供者的个人获得。数据提供商将能够通过还清贷款来重新获得对 NFT 的权利，此后，平台积累的订阅和费用将再次被直接发送给数据提供商。

**4.1 改善医疗保健非功能性医疗服务** 以激励数据购买者继续将非功能性医疗服务视为有价值的服务，而不仅仅是停止支付订阅费，并防止数据泄露；基于不断变化的医疗保健数据和数据提供者或患者的状态，对现有的 NFTs 实施不断的更新将是有用的。随着患者不断地访问医生和患者，他们的状态发生变化，一些人获得新的疾病，而另一些人从他们的健康问题中恢复，因此医疗保健 NFTs 的真正价值将是持续访问不断变化和不断改进的数据存储。未来世界将出现大量物联网应用，这些应用可以通过安装在智能手机等各种设备中的外部传感器来测量患者的不同身体参数，从而进一步提高这些数据的质量。公司和研究团体以及其他医疗保健数据利益相关者希望数据半定期更新，以确保他们所有的人工智能和大数据模型都是最新的，并且他们很可能会为连续访问支付订阅费。

**4.2 现金流** 这样一个项目的现金流最好通过一个图表来显示，该图表描述了 NFT 是如何被订阅的，从而导致资金流向 NFT 被分配到的钱包。一旦 NFT 在另一个系统中被提供作为抵押品，那么钱被重新路由到平台，并且作为交换，数据提供者被给予与根据其估计价格的 NFT 的价值的一定百分比相对应的金额。数据提供者可以随意处置贷款。当他们决定重新获得提供给 NFT 所有者的订阅付款时，他们可以重新存入借出的金额，然后订阅付款再次被路由到数据提供者。这提供了一个封闭的现金流系统，只要 NFT 保持价值，数据提供商就有可能重新获得 NFT 订阅费和 NFT 所有权。然而，只要 NFT 的价格远远低于获得贷款时的价值，就无法收回 NFT，这时可以实施“清算”方法。另一种清算方法是，如果在一定时间内没有支付贷款，就让数据提供者失去 NFT。贷款必须是 NFT 价值的一定百分比，以确保双方都有承担风险的动机，同时满足商定的贷款条件。
要让这个 NFT 抵押品和细分平台发挥作用，需要与数据提供商用来生成或铸造医疗保健 NFT 的市场和系统集成，以确保 NFT 的新部分可以通过解析原始 NFT 实际创建。NFTs 的细分片段也应该是一种便于利益相关者购买和使用数据的格式。需要与整个原始 NFT 进程的利益相关者进行大量的密切合作。费用和订阅付款的路由也必须以与原始 NFT 销售类似的方式实现。为了创造一个最小可行的产品，智能合同将被编码成固态，并部署在以太坊虚拟机上。
还有一个风险是，这种类型的项目是由已经进入 NFT 医疗保健领域并已经创造了市场的利益相关者实施的。他们可以很容易地实现这些改进和考虑。已经有为 NFTs 创建的具有高价值的平台，其中之一就是 Nftfi。Nftfi 是一个平台，它为人们提供了一种以固定期限出借他们的 NFT 以换取 Dai 或 Wrapped Eth 的方式。NFT 被用作贷款的抵押品，如果贷款没有偿还，借款人将失去他们的 NFT，但可以保留打包的 Eth。与此同时，贷方获得了 NFT。市场支持各种各样的 NFT，但不支持每一个 NFT。商定的贷款有固定的 apy(年收益率)和固定的时间期限。

# 5.讨论

**5.1 集中控制** 为了使 NFT 的医疗保健市场存在，以便对非功能性医疗服务进行审查，从而提供正确的数据而不是伪造的数据，并使非功能性医疗服务达到一定的标准，这些市场必须是集中的，或者受政府和医院等集中管理机构的管辖。政府和医院可以制定标准，非功能性测试和它们的有效性必须符合这些标准才能发挥作用。这导致了集中化问题，最终在某种程度上破坏了区块链技术的去中心化性质。NFTs 是否可能有许多不同的格式和标准，但是这会抑制采用，因为医疗保健提供者会反对采用许多不同形式的数据共享和输入系统。

**5.2 身份整合** 了解你的客户也称为 KYC 是一个识别身份以防止欺诈的过程。从一家医院到另一家医院进行 KYC 是非常复杂和耗时的，区块链是这个问题的解决方案，因为它可以通过不可变的账本更容易地验证，并且还可以分散数据库的安全性。KYC 对于医疗服务提供者协调具有患者医疗保健史的患者的治疗也很重要。
这方面的一个例子是，当一名患者因急诊被送往医院时，医护人员可能会询问患者的详细情况。这些细节包括任何损伤、疾病和患者的身体状况，以及患者是否对某些状况(如高血压)有某种倾向，或者是否有自身免疫问题(如过敏)。这些细节也包括药物。患者可能认为某些情况和药物与他们当前的困境无关，这种考虑可能造成的伤害取决于患者对药物的判断和教育。卫生保健专业人员很少有时间与所有不同的机构协调，例如私人诊所和病人以前去过的其他医院，以确认病人自己声称的病史图像。患者日志中也可能有大量信息，诊所的医生通常会在其中记录就诊情况，即使这些信息以 EHR 的形式出现，也需要大量阅读或数据挖掘才能提取出来。
为了克服上述例子中解释的障碍，将区块链技术集成到一个集成解决方案中可能是有用的，例如从 EHRs 的解析数据中生成的 NFT。此类解决方案已在第 3 节中提到，许多基于区块链的公司正在与医院合作。为了让他们基于 NFT 的解决方案取得成功，就医疗保健数据 NFT 中应包含的数据格式达成一致非常重要。这种格式可以通过挑选最受欢迎和最容易获得的格式来非正式地决定，这种格式在竞争市场中最有用处。然而，如果区块链公司之间更密切地合作，这一过程将会加快。决定一种类型的医疗保健模式也是一个全球性的问题，因为不同国家的 EHR 系统千差万别，不愿意采用彼此的系统。

**5.3 安全问题** NFT 数据因泄露而落入他人之手的可能性是一个无法在数字领域解决的问题，需要各国政府和司法系统等监管机构的帮助才能实施。或许核查和监管的结合能够提供一个解决方案，让各方在买卖非森林交易之前签署具有法律约束力的文件；然而，这种解决方案对于大量转售是不可行的。
针对试图破坏创新医疗数据系统的非理性行为，可以采取的安全措施数量有限。然而，我们最多能做的是假设大多数与系统互动的个人和团体都是理性的行为者，因此不会为了很少或没有收益而破坏系统。在许多情况下，泄露患者的医疗保健数据不会使已经付费订阅或购买有限数据访问权的一方受益。由于区块链技术的性质，很容易确定是谁泄露了数据，这将导致该方失去可信度。
医疗保健数据 NFT 有价值的原因之一是，由于数据提供商的健康状况不断变化，它们也在不断变化，因此价值会随着时间的推移而增加。另一个原因是，NFT 的真实性可以通过区块链来验证。如果泄露数据的一方试图删除或掩盖他们访问的任何痕迹，泄露的数据将不会具有相同的安全级别。移除区块链访问的痕迹也会导致真实性的移除，因为这并不是通过区块链验证数据完整性的一种方法，因此泄漏是不可信的。为了让数据发挥最大的价值，需要通过付费的方式以正确的方式访问数据。
当涉及到侵犯医疗保健数据的数字产权时，可以认为未经授权复制非功能性数据将受到 GDPR 的保护。这可能会使复制或拷贝的 NFT 被政府视为被盗的数字财产，从而允许人们利用现有的执法和法律系统起诉和/或追回他们的数字财产。截至[还没有](https://tinyurl.com/2p937ssk)NFT 被版权法和专利法认可。然而，随着加密货币的日益主流化和区块链技术日益成为主流，NFTs 作为数字财产的认可可能会在未来发生。

# 6.结论和未来工作

医疗保健数据分发的未来在很大程度上取决于将许多不同的医疗保健提供商互连在一起，以便他们的数据可以无缝共享。NFTs 是通过经济激励将医疗服务提供者聚集在一起的一种方式，也是吸引患者参与的一种可行方式。基于数据和技术的医疗保健是非常动态和个性化的，然而它需要几年的时间才能被采用，但区块链可以通过吸引和在经济上激励患者来加速现有的整合基于数据的技术的努力，如人工智能和机器学习模型。当患者利用他们对数据的新控制权时，医疗保健的未来可能会发生彻底的变革，这也可能加快研究和治疗的发展。有许多基于区块链的平台已经产生了各种各样的工具，并与医院建立了合作伙伴关系，因此可以说，变革世界医疗保健的所有工具都已经存在。他们只是需要被收养。

# 7.参考

[1]
克里斯蒂安·卡斯塔涅达等《提高诊断准确性实现精准医疗的临床决策支持系统》。载于:《临床生物信息学杂志》5.1 (2015)，第 1 页“16。

[2]
Elias Mossialos 等 2015 国际卫生保健系统概况。加拿大卫生药物与技术署，2016 年。

彼得·费尔利。区块链世界——喂养区块链野兽如果比特币真的成为主流，维持它所需的电力将是巨大的。载于:IEEE Spectrum 54.10 (2017)，第 36 页“59。

[4]
小刺列昂尼德和小刺列昂尼德。实施全国范围的电子健康记录(EHR):13 个国家的国际经验。载于:《国际卫生保健质量保证杂志》(2018)。

[5]
斯坦尼斯劳·P·斯塔维基，迈克尔·S·弗森伯格，托马斯·J·帕帕迪莫斯，等,《学术医学的新进展？医疗保健领域的区块链技术:更大、更好、更公平、更快、更精简。载于:国际学术医学杂志 4.1 (2018)，第 1 页。

[6]
Asad Ali Siyal 等,《区块链技术在医疗保健领域的应用:挑战与未来展望》。载于:密码学 3.1 (2019)，第 3 页。

[7]
Lorenzo Ghiro 等什么是区块链？明确区块链在物联网中的作用的定义。载于:arXiv 预印本 arXiv:2102.03750 (2021)。

简·托马森。大技术、大数据和数字健康新世界。载于:《全球健康杂志》(2021 年)。

[9]
秦王等.不可替代令牌(NFT):概述、评价、机遇与挑战。载于:arXiv 预印本 arXiv:2105.07447 (2021)。

> 加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

# 另外，阅读

*   [加密保证金交易交易所](/coinmonks/crypto-margin-trading-exchanges-428b1f7ad108) | [赚取比特币](/coinmonks/earn-bitcoin-6e8bd3c592d9) | [Mudrex 投资](https://coincodecap.com/mudrex-invest-review-the-best-way-to-invest-in-crypto)
*   [WazirX vs coin dcx vs bit bns](/coinmonks/wazirx-vs-coindcx-vs-bitbns-149f4f19a2f1)|[block fi vs coin loan vs Nexo](/coinmonks/blockfi-vs-coinloan-vs-nexo-cb624635230d)
*   [比斯勒评论](https://coincodecap.com/bitsler-review)|[WazirX vs coin switch vs coin dcx](https://coincodecap.com/wazirx-vs-coinswitch-vs-coindcx)
*   [7 大副本交易平台](https://coincodecap.com/copy-trading-platforms) | [BuyCoins 点评](https://coincodecap.com/buycoins-review)