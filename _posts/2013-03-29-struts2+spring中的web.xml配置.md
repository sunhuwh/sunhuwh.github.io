---
layout: post
title: struts2+spring中的web.xml配置
date: 2013-03-29 12:45
categories: [Spring, Struts 2]
tags: []
---
调试方法：由于我们写web.xml时经常会加载struts2的核心，常常导致错误信息量增加的非常的多，所以在调试的时候会将其注释起来，然后再去调试。调试的时候注意先后顺序，一般出现错误，会有黑体字显示出来（反正我这次是的），注意与所加载的jar文件相比较，实在不行就百度下。

在网上查了一下，多是说把ContextLoaderListener改为SpringContextServlet，但我这样改了没用。后来在一个英文网站上看到一个遇到同样问题的帖子，他是这样改的：
<context-param> 
   <param-name>log4jConfigLocation</param-name> 
   <param-value>/WEB-INF/config/log4j.properties</param-value> 
</context-param> 

······ 

<!-- 定义LOG4J监听器 --> 
<listener> 
   <listener-class> 
org.springframework.web.util.Log4jConfigListener 
   </listener-class> 
</listener> 

这样改了问题就解决了，不用再修改ContextLoaderListener。
   