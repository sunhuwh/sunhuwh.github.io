---
layout: post
title: web service
date: 2015-01-12 23:57
categories: [常识]
tags: []
---
Web service是一个平台独立的，低耦合的，自包含的、基于可编程的web的应用程序，可使用开放的XML（标准通用标记语言下的一个子集）标准来描述、发布、发现、协调和配置这些应用程序，用于开发分布式的互操作的应用程序。
Web Service技术， 能使得运行在不同机器上的不同应用无须借助附加的、专门的第三方软件或硬件， 就可相互交换数据或集成。依据Web Service规范实施的应用之间， 无论它们所使用的语言、 平台或内部协议是什么， 都可以相互交换数据。

Web service到底是什么；在什么情况下你应该使用Web service。研究一下当前的[应用程序开发](http://baike.baidu.com/view/1753085.htm)，你会发现一个绝对的倾向：人们开始偏爱基于[浏览器](http://baike.baidu.com/view/7718.htm)的客户端应用程序。这当然不是因为客户端能够提供更好的用户界面，而是因为它能够避免花在[桌面应用程序](http://baike.baidu.com/view/2251864.htm)发布上的高成本。发布[桌面应用程序](http://baike.baidu.com/view/2251864.htm)成本很高，一半是因为应用程序安装和配置的问题，另一半是因为客户端和服务器之间通信的问题。传统的Windows客户应用程序使用DCOM来与服务器进行通信和调用远程对象。配置好DCOM使其在一个大型的网络中正常工作将是一个极富挑战性的工作，同时也是许多IT工程师的噩梦。事实上，许多IT工程师宁愿忍受[浏览器](http://baike.baidu.com/view/7718.htm)所带来的功能限制，也不愿在局域网上去运行一个DCOM。在我看来，结果就是一个发布容易，但开发难度大而且用户界面极其受限的应用程序。极端的说，就是你花了更多的资金和时间，却开发出从用户看来功能更弱的应用程序。不信？问问你的会计师对新的基于浏览器的[会计软件](http://baike.baidu.com/view/3574156.htm)有什么想法：绝大多数商用程序用户希望使用更加友好的Windows用户界面。关于[客户端](http://baike.baidu.com/view/930.htm)与服务器的通信问题，一个完美的解决方法是使用HTTP协议来通信。这是因为任何运行[Web浏览器](http://baike.baidu.com/view/206703.htm)的机器都在使用HTTP协议。同时，当前许多[防火墙](http://baike.baidu.com/view/3067.htm)也配置为只允许HTTP连接。许多商用程序还面临另一个问题，那就是与其他程序的[互操作性](http://baike.baidu.com/view/1490165.htm)。如果所有的应用程序都是使用COM或.NET语言写的，并且都运行在Windows平台上，那就天下太平了。然而，事实上大多数商业数据仍然在大型主机上以非关系文件(VSAM)的形式存放，并由COBOL语言编写的大型机程序访问。而且，还有很多商用程序继续在使用C++、Java、Visual
 Basic和其他各种各样的语言编写。除了最简单的程序之外，所有的应用程序都需要与运行在其他异构平台上的应用程序集成并进行数据交换。这样的任务通常都是由特殊的方法，如[文件传输](http://baike.baidu.com/view/543341.htm)和分析，[消息队列](http://baike.baidu.com/view/262473.htm)，还有仅适用于某些情况的的API，如IBM的"高级程序到程序交流(APPC)"等来完成的。在以前，没有一个应用程序通信标准，是独立于平台、组建模型和[编程语言](http://baike.baidu.com/view/552871.htm)的。只有通过Web
 Service，[客户端](http://baike.baidu.com/view/930.htm)和服务器才能够自由的用HTTP进行通信，不论两个程序的平台和[编程语言](http://baike.baidu.com/view/552871.htm)是什么。**什么是Web Service**对这个问题，我们至少有两种答案。从表面上看，Web service 就是一个应用程序，它向外界暴露出一个能够通过Web进行调用的API。这就是说，你能够用编程的方法通过Web来调用这个应用程序。我们把调用这个Web service 的应用程序叫做客户。例如，你想创建一个Web service ，它的作用是返回当前的天气情况。那么你可以建立一个ASP页面，它接受邮政编码作为查询字符串，然后返回一个由逗号隔开的字符串，包含了当前的气温和天气。要调用这个ASP页面，[客户端](http://baike.baidu.com/view/930.htm)需要发送下面的这个HTTP
 GET返回的数据就应该是这样：这个ASP页面就应该可以算作是Web service 了。因为它基于HTTP GET请求，暴露出了一个可以通过Web调用的API。当然，Web service 还有更多的东西。下面是对Web service 更精确的解释： Web services是建立可互操作的[分布式应用程序](http://baike.baidu.com/view/553502.htm)的新平台。作为一个Windows程序员，你可能已经用COM或DCOM建立过基于组件的[分布式应用程序](http://baike.baidu.com/view/553502.htm)。COM是一个非常好的组件技术，但是我们也很容易举出COM并不能满足要求的情况。Web service平台是一套标准，它定义了应用程序如何在Web上实现[互操作性](http://baike.baidu.com/view/1490165.htm)。你可以用任何你喜欢的语言，在任何你喜欢的平台上写Web
 service ，只要我们可以通过Web service标准对这些服务进行查询和访问。



