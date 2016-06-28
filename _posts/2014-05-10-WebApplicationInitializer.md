---
layout: post
title: WebApplicationInitializer
date: 2014-05-10 02:47
categories: [servlet, E-learning]
tags: []
---
针对public class DefaultConfigration implements WebApplicationInitializer

来想一个问题：为什么实现了WebApplicationInitializer这个类后onStartup方法就会自动执行。
这个要看下它(WebApplicationInitializer)接口旁边(同包)有个SpringServletContainerInitializer
而这个类实现的是ServletContainerInitializer
这个接口，需要看它的API
首先，这个接口实现的必要条件是，必须在spring-web-3.X.X.RELEASE-sources.jar下的META_INF/services下有个javax.servlet.ServletContainerInitializer文件下有个跟ServletContainerIntializer实现类名字相同的一段代码。
然后还必须使用HandlesTypes声明ServletContainerInitializer可以使用的类型。
而如何发现ServletContainerInitializer的呢？
刚才说了ServletContainerIntializer该接口的实现必须声明一个JAR资源放到程序中的META-INF/services下，并且记有该接口那个实现类的全路径，才会被运行时(server)的查找机制或是其它特定机制找到。所以会发现。


所有三种类型的注释文档都可包含@see标记，它允许我们引用其他类里的文档。对于这个标记，javadoc会生成相应的HTML，将其直接链接到其他文档。格式如下：
@see 类名
@see 完整类名
@see 完整类名#方法名


参考：[Spring 3.1之无web.xml式 基于代码配置的servlet3.0应用](http://datum.iteye.com/blog/1537632)
[Servlet3.0新特性](http://blog.csdn.net/aking21alinjuju/article/details/5583820)

