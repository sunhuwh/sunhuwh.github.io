---
layout: post
title: tomcat构建web站点
date: 2013-03-02 15:23
categories: [Java Web]
tags: []
---
启动tomcat除了用计算机管理中的服务还可以用tomcat中的启动项，位于tomcat/bin下.exe文件中。
tomcat5.exe启动的Tomcat程序不一定是tomcat5.exe自身所在的目录。因为tomcat5.exe只是启动一个org,apache.catalina.startup.Bootstrap类的Windows外壳包装程序。
在按照书上说的设置web站点的虚拟子目录时出现问题，在server.xml中没有找到
<!--
<Context path = "" docBase = "ROOT" debug="0"/>
-->
类似的这个东西也没找到，找到的只有<Host>....
用那可以构建根目录，但无法构建虚拟子目录。
由于<Context>元素只能放在<Host>元素中，我就在<Host>元素中增加设置虚拟子目录的代码，但是还是不行。
