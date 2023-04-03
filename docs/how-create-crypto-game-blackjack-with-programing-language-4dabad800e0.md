# 如何用编程语言创建加密游戏 21 点

> 原文：<https://medium.com/coinmonks/how-create-crypto-game-blackjack-with-programing-language-4dabad800e0?source=collection_archive---------26----------------------->

![](img/52dd66af893b656906ea9689ff7116da.png)

你在找什么？

本教程将向您展示如何使用 Python、JavaScript 和 Canvas 制作自己的加密游戏。我们将创建一个具有以下特征的 21 点游戏:洗牌、抽一张初始牌、旋转一张新牌、指示何时赢了。如果你对制作你自己的加密游戏感兴趣，但是不知道从哪里开始，这篇博文就是为你准备的！它将向您展示如何从零开始制作自己的 21 点游戏，而不需要任何编程经验。

**下面是最终结果的预告:**

**如何洗牌。**

让我们先讨论一下游戏机制。在 21 点中，我们需要一副牌，作为我们的随机数发生器(RNG)。我们将有 52 张牌。

我们需要能够添加和删除我们的卡组。让我们为这个功能实现一个接口:

game = { shuffle:function(){ for(var I = 0；我< 52; i++) { this._addCards(Math.ceil(Math.random() * 52)); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } } };

This new implementation has a deck of cards which is accessible via the game object. We have a shuffle method, which will randomly select cards and add them to our deck container object. We also have an addCards method, which will generate a specific number of cards and push them onto the end of our deck object.

**游戏的关键**

在大多数加密游戏中，你会有一副牌。在 21 点中，我们需要洗牌。我们有一个创建、移除和洗牌的基本界面:

game = { shuffle:function(){ for(var I = 0；i < 52i++) {这个。_ empty cards()；} }，add cards:function(num){ for(var I = 0；i < numi++){ cards . push(cards . length)；} } };

让我们稍微调整一下我们的代码。我们需要能够从我们的牌组中取出牌:

game = { shuffle:function(){ for(var I = 0；i < 52i++) {这个。_ empty cards()；} }，add cards:function(num){ for(var I = 0；i < numi++){ cards . push(cards . length)；} }，empty cards:function(){ for(var a = 0；a < cards . length—1；a++){ cards . pop()；} } };

这副牌是用洗牌法创建的。洗完牌后，我们清空这副牌，以便再次洗牌。这是我们的游戏对象的样子:

game = { shuffle: function () { this。_ empty cards()；}，add cards:function(num){ for(var I = 0；i < numi++){ cards . push(cards . length)；}，empty cards:function(){ for(var a = 0；a < cards . length—1；a++){ cards . pop()；} } };

让我们实现这个洗牌方法:

game = { shuffle:function(){ for(var I = 0；i < 52i++) {这个。_ empty cards()；} }，add cards:function(num){ for(var I = 0；i < numi++){ cards . push(cards . length)；} }，empty cards:function(){ for(var a = 0；a < cards . length—1；a++){ card . pop()；} };

现在我们可以开始玩我们的 21 点游戏了！

让我们看看 shuffle 方法的源代码:

game = { shuffle:function(){ for(var I = 0；我< 52; i++) { this._emptyCards(); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } }, emptyCards: function() { for (var a = 0; a < Cards.length — 1; a++) { Card.pop(); } };

It will randomly remove cards from the deck. We need to add some coding for drawing a winning hand:

game = { shuffle: function () { for (var i = 0; i < 52; i++) { this._emptyCards(); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } }, emptyCards: function() { for (var a = 0; a < Cards.length — 1; a++) { Card.pop(); } };

So now we can make our own games. Here are two more examples:

**第一步:确定你需要从游戏中得到什么**

在开始编写代码之前，你必须在头脑中有一个游戏。加密游戏和其他游戏的主要区别在于，你需要能够动态地改变一些事情(随机挑选卡片，从最初的一副牌中分发新卡，添加新功能)。例如，如果你正在制作一个加密问答应用程序，你的游戏每次启动时都会完全不同。

上面的 21 点游戏只不过是一个随机数生成器。这只有在我们开始玩游戏的时候才会发生。在发了一张牌并添加了一张新牌后，这副牌将被洗牌，所有的牌都将消失。这副牌中的第一张牌成为当前可用来回答问题的牌。

在重新开始之前，我们需要有一些从我们的牌组中生成和移除牌的模式:

game = { shuffle:function(){ for(var I = 0；第二步:设计你的游戏

现在有趣的部分来了！在开始编码之前，想想你需要实现什么。大多数时候，你会有一副不同的牌，可以根据需要发牌。如果你的游戏需要一次发多张牌，你应该实现一个类似这样的接口:

game = { shuffle:function(){ for(var I = 0；i < 52; i++) { this.currentCard = Cards.length; this._addCards(Cards.length); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } }, emptyCards: function() { for (var a = 0; a < Cards.length — 1; a++) { Card.pop(); } };

**第三步:实现游戏**

在你决定了你要做什么样的游戏后，你就准备好实施它了！让我们再次开始我们的 21 点游戏。我们将有洗牌法和出牌法，因为我们一次只发一张牌:

game = { shuffle:function(){ for(var I = 0；我< 52; i++) { this.currentCard = Cards.length — 1; this._addCards(Cards.length); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } }, emptyCards: function() { for (var a = 0; a < Cards.length — 1; a++) { Card.pop(); } };

Here is how the code to deal the first card looks like:

game = { dealCard: function () { var card = Cards.length — 1; for (var i = 0; i < card; i++) { if (Cards.length > 0) {这个。_ deal cards()；} } }，_ deal cards:function(){ for(var a = 0；第四步:测试你的游戏

你可以在脑子里有一个游戏，但不代表你知道怎么把它写对。即使你不打算用它做什么，你也应该测试你的代码。下面是处理整副牌并检查我们是否应该被允许处理另一副牌的代码:

game = { shuffle:function(){ for(var I = 0；I< 52; i++) { this.currentCard = Cards.length — 1; this._addCards(Cards.length); } }, addCards: function (num) { for (var i = 0; i < num; i++) { Cards.push(Cards.length); } }, emptyCards: function() { for (var a = 0; a < Cards.length — 1; a++) { Card.pop(); } };

test = { testDealerTests: function () { if (Cards.length >cards . maxcount){ console . log('庄家可以发另一张牌。');} else { console.log('庄家不能再发一张牌。从头开始。);} }，testDealCards:function(){ if(cards . length > 1){ console . log('庄家不能发牌。');} else { for(var I = 0；I< Cards.length; i++) { if (i >1){ console . log(‘你不能再发一张牌了。’);} else { console.log('你可以洗牌，发另一张牌。

');} } console.log('经销商交易\ '？');test . testdealertests()；} };

**第五步:给你的游戏添加一个图形用户界面**

你以为我会就此结束本教程吗，哈哈？你可以在游戏中加入各种有趣的元素。假设您正在制作一个这样的纸牌游戏:

为了使它更有趣，你可能想增加一些功能，比如改变你的卡片的背景颜色:

仅此而已！如果你愿意，你可以为自己的游戏想出一些点子，并加以实现。如果您想了解有关该主题的更多信息，请参考以下资源:

PSN Web API 是处理用户交互的好方法。它也非常简单，因为它使用 JSON 作为返回值。

每当您从用户那里获得输入时，您的游戏可能会以编程方式改变—在这个游戏中，我添加了所有在玩扑克时扔掉的牌。这样，我可以确保当我们重新开始时，桌子上总会有两张牌。

如果你已经通读了这个教程，你仍然有一些问题或者某些事情不适合你，请在下面留下评论，我会尽快帮助你。

更多教程请关注我的 Twitter 或 Github！请随意留下一些反馈——也欢迎对教程的请求！感谢阅读。

我做了一个叫做 ScreenCastsToGif 的小工具，它可以帮助你从你录制的视频中创建动画 Gif。它完全免费使用，只需尝试一下并留下一些反馈，这样我就知道我是否应该继续工作:)。

请启用 JavaScript 来查看 Disqus 支持的评论。

迪斯克斯

你也可以考虑这些相关的帖子:在[ASP.NET](http://asp.net/)Web API 2 中学习身份验证，在。NET Core 与 WebAPI 2 和 OWIN 中间件在 ASP.NET[创建一个基本游戏](http://asp.net/) WebAPI 2 与 HttpClient 在本教程中，我将向您展示如何使用 Web API 2 向 Azure cloud 上托管的[ASP.NET](http://asp.net/)MVC 6 应用程序发送请求。在我职业生涯的这个阶段，我已经开始使用 jQuery，然后是 AngularJs，现在是[ASP.NET](http://asp.net/)MVC 6 当需要编写新的 web 应用程序时，我仍然更喜欢使用 pure。NET 框架解决方案。NET Core，它给了我许多优势，如能够利用实体框架开箱即用，或轻松地将其与其他 NoSQL 数据库集成，因为实体框架不需要那种数据访问代码。它只是开箱即用。当你有很多微服务相互通信，REST 是其中一种方式时，[ASP.NET](http://asp.net/)Web API 2 似乎是微软开发人员最常见的选择，尽管它已经被弃用多年，但我仍然更喜欢使用它，因为我真的很喜欢它，而且当你使用它工作时，它仍然是编写微服务 API 的好方法。净核心项目。还有[ASP.NET](http://asp.net/)核心 MVC，已经从头开始重新编写，现在公开了一组新的 API，以便能够使用以前在[ASP.NET](http://asp.net/)MVC 中不可用的功能，但将从[ASP.NET](http://asp.net/)核心 1.0 开始可用。新的[ASP.NET](http://asp.net/)核心 MVC 将使用与实体框架 7 不兼容的实体框架 6，因此本教程将使用实体框架 7，它是一个非常好的 web 应用程序数据库，因为它是一个 NoSQL 数据库，具有处理微服务所需的所有特性。在本教程中，我将使用 Web API 2 提供一个例子，说明如何在很短的时间内处理 HTTP 请求，以及如何在需要时提供基本的身份验证。首先，你必须创建一个[ASP.NET](http://asp.net/)核心 MVC 6 应用程序。登录被禁用，因为我们不需要它，所以我们首先向项目添加所需的引用:

引用 Entity Framework 7 Nuget 包之后，您可以在 Startup.cs 文件中更改一些设置，比如将您的基本 URL 更改为自定义 URL，还可以设置一些路由。我现在不会谈论这个，因为有很多教程解释如何做到这一点，而且很容易，但假设您想确保用户只能通过 [https://mydomain/api](https://mydomain/api) 访问您的 API，那么您可以在 Configure 方法中添加它:

配置您的 ASP.NET[核心 MVC 6 应用程序现在让我们创建一个名为 APIController 的控制器，它有一个接受 GET 请求的动作:](http://asp.net/)

创建 API 控制器，然后我们只需像这样为我们的操作添加代码:

现在创建 API 操作如果我们运行我们的应用程序，您会看到它出错，因为我们还没有设置我们的身份验证。在本教程的最后，我们将看到如何做到这一点。我使用 Entity Framework 7 作为数据库，所以我们在需要时添加一个 using 语句:

现在让我们在控制器中创建数据库，我们可以为我们的操作添加一些代码，以获得代表当前登录用户的用户 ID:

现在添加了 Authenticate 函数，您可以像这样将一些 HttpClient 实例注入到您的控制器中:

使用 HttpClient 添加身份验证要开始发送请求，我们必须创建一个启用了基本身份验证的 HttpClient 实例:

创建 HttpClient 的一个实例，我们可以像这样把它注入到我们的控制器中:

使用 ASP.NET[核心 MVC 6 和实体框架 7 创建一个 HttpClient 实例，然后我们可以使用 HttpClient 实例的 Authenticate 方法来调用我们的动作，如果用户登录，它将为我们提供一个用户 ID，在这种情况下它不会这样做，因为我们还没有为基本认证提供任何散列。所以让我们为此添加一些代码:](http://asp.net/)

现在添加基本身份验证如果您尝试运行您的应用程序，您会看到它总是返回一个空列表。这是因为我只是检查它是否返回用户 ID，但是当然我们还可以用我们的 API 做其他事情。如果您想创建一个简单的 API，它只返回一个项目列表，您可以使用下面的代码:

现在，当您在 Nuget 包资源管理器中运行您的应用程序时，您将看到这将如何返回数据库中的所有项目。GitHub 上有这个小项目。我将很快发布更多文章，所以如果你有兴趣了解更多关于 space 核心 MVC 6 和实体框架 7 的内容，请关注这个空间。我希望这篇文章对你有用。你可以在下面的评论区留下你的反馈。如果你是编程新手，想了解更多，可以看看我的书《用 ASP.NET 和 AngularJS 为智能设备编程》，这本书教你如何用 AngularJS 2 和 ASP.NET 的 MVC 6 用 HTML 5 和 JavaScript 构建现代网络界面。通过包管理器控制台安装 nuget 包，打开命令提示符，转到你的项目所在的目录(Ctrl+Shift+P)>CD C:\ Users \ Username \ Documents \ Visual Studio 2017 \ Projects。运行“安装-打包微软。AspNetCore.Mvc -Pre”命令将其安装到您的 Visual Studio 2017 中。在 GitHub 上投稿:[https://github.com/felixthecat/Blog](https://github.com/felixthecat/Blog)

本文是你可能也想看的[ASP.NET](http://asp.net/)Core 和[ASP.NET](http://asp.net/)Core MVC 系列文章的一部分:用实体框架 7 (C#)在[ASP.NET](http://asp.net/)Core 1.0(c#)中构建一个简单的 Web API 用[ASP.NET](http://asp.net/)Core MVC 6(c#)和 Angular 2 (ES6)构建一个在线报价系统用[ASP.NET](http://asp.net/)Core 1.0(VB。NET)与实体框架 7 (VB。NET)用[ASP.NET](http://asp.net/)Core 1.0 和 Angular 2 (AngularJS)构建一个在线报价系统用[ASP.NET](http://asp.net/)Core 1.0(c#)用实体框架 7 (C#)构建一个简单的 Web API 用[ASP.NET](http://asp.net/)Core 1.0、Angular 2 和 Bootstrap 4 构建一个在线报价系统

您收到这封电子邮件是因为您订阅了[ASP.NET](http://asp.net/)开发者社区简讯或 Feedly。您可以随时在设置页面取消订阅或更改您的设置

新来的 ASP.NET[？先查这个:ASP.NET](http://asp.net/)的[是什么？](http://asp.net/)

你可能还想检查一下[ASP.NET](http://asp.net/)内核:什么是[ASP.NET](http://asp.net/)内核？。

喜欢你读的吗？如果是这样的话，注册我们的时事通讯，并通过现在订阅获得更多关于如何掌握[ASP.NET](http://asp.net/)的技巧和诀窍！有任何问题或反馈吗？下面留言评论！此外，如果你认为这篇文章对你的朋友有用，请不要犹豫与他们分享。只需使用页面顶部的社交媒体按钮。感谢阅读！^_^:你可以在自己的网站上留下回复或引用通告。留下回复

发布于。。。。。。。

In [ASP.NET](http://asp.net/) MVC 5, you don’t need to use the new attribute @section on action. It’s the view engine that does that for you: <div asp-view> … </div> <% @section … %> In [ASP.NET](http://asp.net/) Core MVC 6 and [ASP.NET](http://asp.net/) Core 2.0, you can use this: <% @section … %> You can also do this in [ASP.NET](http://asp.net/) MVC 6: <% @section … %> You can also use a ViewBag to contain any toys you want and it’s even possible to declare multiple sections if you want to. This is what I do in my Controllers these days: public class HomeController : Controller { [HttpGet] public ActionResult Index() { var data = ViewBag.Message; return View(data); } } The ViewBag allows you to pass variables between the different parts of your code and the view. As a matter of fact, the ViewBag is nothing more than a dictionary and is made available to your views by including the Microsoft.AspNetCore.Mvc.ViewFeatures NuGet package in your project: <script src=”~/lib/Microsoft/AspNetCore.Mvc.ViewFeatures/view-source-first@2.0.2.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc.ViewFeatures/jquery@3.1.0/jquery.min.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc.ViewFeatures/jquery@3.1.0/jquery.validate@3.1.0/dist/jquery.validate-vsdoc-amd-2.0.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc.ViewFeatures/jquery@3.1.0/jquery.validate@3.1.0/dist/jquery.validate-amd-2.0.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc.ViewFeatures/jquery@3.1.0/extensions/validate-on-input@4.0.0.js”></script> <%= Html.ValidationSummary() %> I was searching all over MVC 1, 2 and 5 and here’s what I found: <div class=”text-right”> <h2>Here are some useful links to help you get started with {{Name}}</h2> @section HelpLinks { @Html.ActionLink(“Get Started Now”, “Index”, “Home”) @Html.ActionLink(“Create A New Store”, “Create”, “Home”) @Html.ActionLink(“See all Stores”, “Index”, “Stores”) } </div> It seems as though the section tag was first introduced in MVC 2 and then deprecated in MVC 5 so that it can be removed in something newer like [ASP.NET](http://asp.net/) Core MVC 6 or [ASP.NET](http://asp.net/) Core 2.0\. And this is what Google suggests, too: @section or <div asp-view></div> Apparently, section tags are now considered obsolete and you’re supposed to use <div asp-view></div> instead. The tag views are rendered only for Razor-based views (and for parts of Razor itself). But @section … can be used on any view and are rendered before anything else in the view. <% @section … %> <div> { render partial } </div> So it seems that you can use sections in any view, and that’s what I do with my Razor views these days. I use ViewBags for everything else: public ActionResult Index(ActionResult data) { ViewBag.Message = data; return View(); } public ActionResult About() { var data = ViewBag.Message; return View(data); } Then I include “ViewBag” as a dictionary in the HTML: <%= Html.ActionLink(“About”, “About”) %> ViewBag can contain any variables, too. The downside is that it’s quite slow to display multiple + objects. Here’s where I usually end up: <% @Html.ActionLink(“Create a new store”, “Create”) %> public ActionResult Create(string store) { ViewBag[“Store name”] = store; return View(); } <div class=”grid-column”> <div class=”row” asp-view> … </div> <%= Html.Partial(“Store Name”, string.Empty)</%> </div> The default behavior of the [ASP.NET](http://asp.net/) MVC 6 services is async query execution. In [ASP.NET](http://asp.net/) MVC 5, if you used the new action attribute: @section … (new) In [ASP.NET](http://asp.net/) Core MVC 6 and [ASP.NET](http://asp.net/) Core 2.0, you can use this: @section … (new) I have to say that I’m not too familiar with it since I usually use ViewBags to pass variables between the different parts of my code and the view. The ViewBag allows you to pass variables between the different parts of your code and the view. As a matter of fact, the ViewBag is nothing more than a dictionary <script src=”~/lib/Microsoft/AspNetCore.Mvc/view-source-first@2.0.2.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3.1.0/jquery.min.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3.1.0/jquery.validate@3.1.0/dist/jquery.validate-vsdoc-amd-2.0.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3\..\..\..\dist\jquery\.validate-amd-2\.0\.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3\..\..\..\extensions\validate-on-input@4\.0\.js”></script> <%= Html.ValidationSummary() %> The beauty of [ASP.NET](http://asp.net/) MVC 6 is the fact that the default behavior of the services is async query execution. In [ASP.NET](http://asp.net/) MVC 5, if you used the new action attribute: @section … (new) In [ASP.NET](http://asp.net/) Core MVC 6 and [ASP.NET](http://asp.net/) Core 2.0, you can use this: @section … (new) By the way, MVC 1~5 only know how to render HTML and not the new [ASP.NET](http://asp.net/) Core MVC 6 view engine. It’s the view engine implements Razor markup, which is quite different from HTML markup. The ViewBag allows you to pass variables between the different parts of your code and the view. As a matter of fact, the ViewBag is nothing more than a dictionary and is made available to your views by including the Microsoft.AspNetCore.Mvc.ViewFeatures NuGet package in your project: <script src=”~/lib/Microsoft/AspNetCore.Mvc/view-source-first@2.0.2.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3.1.0/jquery.min.js”></script> <script src=”~/lib/Microsoft/AspNetCore.Mvc/jquery@3.1.0/jquery.validate@3.1.0/dist\jquery\._validate-vsdoc-amd-2\.0\.js”></script> <script

加入 Coinmonks [电报频道](https://t.me/coincodecap)和 [Youtube 频道](https://www.youtube.com/c/coinmonks/videos)了解加密交易和投资

另外，阅读

[如何开始用加密贷款赚取被动收入](https://coincodecap.com/passive-income-crypto-lending)

[BigONE 交易所评论](/coinmonks/bigone-exchange-review-64705d85a1d4) | [电网交易机器人](https://coincodecap.com/grid-trading)

> [氹欞侊贸易评论](https://coincodecap.com/anny-trade-review) | [CoinSpot 评论](https://coincodecap.com/coinspot-review)

# [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)

*   [投资印度的最佳加密软件](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021) | [WazirX P2P](https://coincodecap.com/wazirx-p2p)
*   [7 个最佳零费用加密交易平台](https://coincodecap.com/zero-fee-crypto-exchanges)
*   [最佳网上赌场](https://coincodecap.com/best-online-casinos) | [期货交易机器人](/coinmonks/futures-trading-bots-5a282ccee3f5)
*   [10 Best Crypto Exchange in Singapore](https://coincodecap.com/crypto-exchange-in-singapore) | [Buy AXS](https://coincodecap.com/buy-axs-token)
*   [Best Crypto to Invest in India](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021) | [WazirX P2P](https://coincodecap.com/wazirx-p2p)
*   [7 Best Zero Fee Crypto Exchange Platforms](https://coincodecap.com/zero-fee-crypto-exchanges)
*   [Best Online Casinos](https://coincodecap.com/best-online-casinos) | [Futures Trading Bots](/coinmonks/futures-trading-bots-5a282ccee3f5)