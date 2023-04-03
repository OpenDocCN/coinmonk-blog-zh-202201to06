# Kubernetes 工作流程简而言之

> 原文：<https://medium.com/coinmonks/kubernetes-workflow-in-short-161fe80f2f89?source=collection_archive---------16----------------------->

# **简介**

祝大家平安，这个博客主要关注 Kubernetes 及其工作流程。

# **入门**

Kubernetes 是一个容器编排工具，有很多特性，需要一个单独的系列文章。在这里，我将重点讨论如何在 Kubernetes 上托管一些简单的东西。

# 容器

在开始学习 Kubernetes 之前，了解一些关于容器的知识是很重要的。

可以把容器想象成一个完整应用程序的运行实例，具有所有必需的依赖关系。容器不必是整个应用程序，它们可以是不同的微服务、服务等。

所以简单地部署一个容器就足够了，而不是安装整个应用程序及其依赖项。

# 集群与节点和单元

顾名思义，群集指的是节点群集。一个集群可以运行多个节点。

准确地说，节点是一个虚拟机。它将有中央处理器，内存，只读存储器等。一个节点可以运行多个 pod。

pod 通常是运行的容器，但不一定是单个容器。它是 Kubernetes 中基本的可部署对象。

> 交易新手？试试[密码交易机器人](/coinmonks/crypto-trading-bot-c2ffce8acb2a)或[复制交易](/coinmonks/top-10-crypto-copy-trading-platforms-for-beginners-d0c37c7d698c)

# **服务和入口**

部署在 pod 中的容器可以通过使用服务公开来访问。服务有助于内部路由(集群内部和集群之间的通信)以及使用 IP 对外公开某些内容。

例如，只有通过服务公开 pod，才能访问运行前端的 pod。

Ingress 是一种负载平衡器，主要用于基于域的路由(Ingress 还有许多其他功能)。

例如，您拥有一个名为[xyz.com](http://xyz.com)的域名，您需要基于“xyz.com/about”、“abc.xyz.com”等路径创建子域或域名。这些都可以在 Ingress 的帮助下处理。

将需要入口控制器来处理入口。Nginx 是最常见的 Ingress 和 Ingress 控制器，但还有其他几种 [Ingress 控制器](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/#additional-controllers)。

# 机密和配置

配置文件有可以公开的值，秘密文件有可以公开的值。这些是应用程序运行时所需的值。它们主要在 AppSettings 中使用，在应用程序的容器化过程中会被忽略，因此，如果 AppSettings 中有值，则这些文件作为 config 和 secret 是必不可少的，以便应用程序工作。

# 基本工作流程

您已经准备好部署一个应用程序。

第一步是容器化[应用程序](https://shajith.hashnode.dev/containerizing-an-angular-app)并获得[映像](https://shajith.hashnode.dev/creating-our-own-image-using-dockerfile)。该图像可以用于使用任何管道的构建(我们将在接下来的博客中重点介绍)，或者直接托管在 K8s 中。

用 YAML 编写的部署文件可以用来创建 pod。如果需要，秘密，配置文件和服务也写在 YAML。

如果需要的话，服务文件公开应用程序以使用任何 IP 进行外部访问。

这是一个 K8s 应用程序的基本工作流程。

# 摘要

这篇博客解释了如何在 Kubernetes 中托管一个最小文件，而不涉及云或管道概念。下面的博客将关注 K8s 附带的云和管道概念。

# 回头见…

好吧。所以，请继续关注我，我们会更加了解 Kubernetes 和 DevOps。

愿你平安！