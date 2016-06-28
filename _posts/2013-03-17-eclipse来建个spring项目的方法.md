---
layout: post
title: eclipse来建个spring项目的方法
date: 2013-03-17 03:51
categories: [Spring]
tags: []
---
在网上搜了个专门讲Spring的课件，结果课件里面的图显示不出来，原以为是课件自身问题，结果看见评论里很多人都说图显示不出来，就一人说显示得出来，后来我换成了火狐，竟然成了。Spring课件URL：[http://sishuok.com/forum/blogCategory/showByCategory/40/49.html?user_id=2](http://sishuok.com/forum/blogCategory/showByCategory/40/49.html?user_id=2)
建一个简单的项目的方法：
安装插件方法：install New Software
首先安装SpringSource Tool Suite插件依赖：
Name为：SpringSource Tool Suite
Location为：[http://dist.springsource.com/release/TOOLS/update/e3.6](http://dist.springsource.com/release/TOOLS/update/e3.6)
将url贴在work with上，等待反应，后来只选择aspectJ Development Tools（required）
aspect Development Tools Source（Optional）
Other AJDI tools（Optional）
等待反应，后eclipse会提示删除哪些，就删除哪些就行了。
第二步：
Name为：SpringSource Tool Suite
Location为：[http://dist.springsource.com/release/TOOLS/update/e3.6](http://dist.springsource.com/release/TOOLS/update/e3.6)
Core/Spring IDE
Extensions (Incubation)/Spring IDE
Extensions/Spring IDE
Integrations/Spring IDE
第三步导入jar包就行了，
核心jar包：从下载的spring-framework-3.0.5.RELEASE-with-docs.zip中dist目录查找如下jar包
org.springframework.asm-3.0.5.RELEASE.jar
org.springframework.core-3.0.5.RELEASE.jar
org.springframework.beans-3.0.5.RELEASE.jar
org.springframework.context-3.0.5.RELEASE.jar
org.springframework.expression-3.0.5.RELEASE.jar
  依赖的jar包：从下载的spring-framework-3.0.5.RELEASE-dependencies.zip中查找如下依赖jar包
com.springsource.org.apache.log4j-1.2.15.jar
com.springsource.org.apache.commons.logging-1.1.1.jar
com.springsource.org.apache.commons.collections-3.2.1.jar
第二个我的资源里已经上传了
再接着创建java工程就行了，
名字就为chapter2就行了，再properties，Java Build Path，选Libraries，接着Add JARs（lib包中的），Add Library（Junit->Junit4），这样整个项目需要的东西都准备好了。
建个resources的source folder类型的文件夹，再在下面建个文件为chapter，这个文件夹下面放配置文件的。
文件结构就是：
src---java文件（系统自带）
resources-----配置文件
JRE System Library（系统自带）
Junit 4
Referenced Libraries（导入包后自动生成）
lib------jar包
然后根据这来建项目就行了
 
