---
layout: post
title: spring MVC
date: 2013-07-16 01:59
categories: [Spring]
tags: [MVC]
---
Spring MVC 分离了控制器、模型对象、分派器以及处理程序对象的角色，这种分离让它们更容易进行定制。
Spring 的 Web MVC 框架是围绕 DispatcherServlet 设计的，它把请求分派给处理程序，同时带有可配置的处理程序映射、视图解析、本地语言、主题解析以及上载文件支持。默认的处理程序是非常简单的 Controller 接口，只有一个方法 ModelAndView handleRequest(request, response)。Spring 提供了一个控制器层次结构，可以派生子类。如果应用程序需要处理用户输入表单，那么可以继承 AbstractFormController。如果需要把多页输入处理到一个表单，那么可以继承 AbstractWizardFormController。
工作过程：
1.将web页面中的输入元素封装为一个（请求）数据对象。
2.根据请求的不同，调度相应的逻辑处理单元，并将(请求)数据对象作为参数传入。
3.逻辑处理单元完成运算后，返回一个结果数据对象。
4.将结果数据对象中的数据与预先设计的表现层相融合并展现给用户。
