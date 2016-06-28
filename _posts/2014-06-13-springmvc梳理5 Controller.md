---
layout: post
title: springmvc梳理5 Controller
date: 2014-06-13 01:26
categories: [E-learning, spring mvc]
tags: []
---
原来以前对MVC里面的C都理解错误。
Controller控制器，是MVC中的部分C，为什么是部分呢？因为此处的控制器主要负责功能处理部分：
1.收集并验证（验证还不是很懂，随着后面的学习问题应该可以解答）参数，绑定到命令对象
2.将命令对象传给业务对象，业务对象处理完后返回模型数据。
3.返回ModelAndView（Model部分是业务对象返回的模型数据，视图部分为逻辑视图名）

然后接着上次说的DispatcherServlet，它主要是负责流程控制。

所以它们俩一起，即DispatcherServlet + Controller才能被称为完整的C。
参考：http://jinnianshilongnian.iteye.com/blog/1608234
