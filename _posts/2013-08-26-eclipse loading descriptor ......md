---
layout: post
title: eclipse loading descriptor .....
date: 2013-08-26 09:04
categories: [eclipse]
tags: []
---
Eclipse启动完后打开某个项目出现：
Loading descriptor ....后无反应解决方案：
更改C:\Windows\System32\drivers\etc下的hosts文件，添加127.0.0.1   java.sun.com
如果没有看见hosts文件，那么很有可能使因为文件夹属性设置了隐藏功能。
解决方案：点下开始键，输入：文件夹选项，选择查看→将显示隐藏的文件、文件夹和驱动器和隐藏受保护的操作系统文件前面的钩钩给去掉就ok了。
现在可能碰到另一个问题，就是hosts文件不能修改。这个需要选择hosts→右键属性→在常规这一项下面有个只读，将只读的钩钩给去掉就可以修改了。


Loading descriptor...

修改hosts的原理是什么？

原因是，eclipse 在打开一个项目里会去java的服务器上去下载一个配置文件。（这个文件也不是必须的）。
然而在国内的网络很难连接java.sun.com这个服务器，所以就一直卡在那里，得不到服务器的响应。


而修改hosts的目的是手动指定一个域名对应的ip地址。
我们的修改就是将java.sun.com 指定到本机  127.0.0.1 ，这样就可以很快的连接上这个服务器，肯定，eclipse也下载不到对应的文件，但是会很快的结束这个过程。 所以 Loading descriptor 就不会长时间卡在那里。

拓展知识：
当我们将一个请求发送出去时，是将域名解析成ip地址，这个工作是由dns服务器来完成的。而hosts的作用就是能够帮助我们绕过dns，而是用里面的配置，指定域名的ip。
