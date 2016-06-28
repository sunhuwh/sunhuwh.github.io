---
layout: post
title: spring/IoC的配置
date: 2013-03-19 03:13
categories: [Spring]
tags: []
---
java @override 报错处理
有时候在自己电脑上编译通过的java代码，在别人那里却编译不通过，总是@override报错，把@override去掉就好了，但不能从根本上解决问题。
据说这是jdk的问题，@Override是JDK5就已经有了，但有个小小的Bug，就是不支持对接口的实现，认为这不是Override 而JDK6修正了这个Bug，无论是对父类的方法覆盖还是对接口的实现都可以加上@Override。
首先要确保安装了jdk 1.6，

然后，在eclipse中修改配置，在 Windows->Preferences-->java->Compiler-->compiler compliance level 中选择 1.6，刷新工程，重新编译下；
如果还是不行，就在报错的工程上，鼠标右键选择 Properties-->Java Compiler-->compiler compliance level 中选择 1.6,刷新工程，重新编译下。

通过构造器注入配置Bean，要用<constructor-arg>。而通过setter注入的需要用到<property>。
Spring是如何知道setter方法的呢？如何注入值到里面去呢？这就跟方法的名称关系很大。比如说setMessage()，那么
<property>的name就必须为message。

javaBean的限制：
getter方法，一般属性以“get”开头，对于boolean类型的，一般以”is“开头，后跟首字母大写。如getMessage,isOk。
属性的访问级别还必须得为private。

Spring类型转换系统对于boolean类型进行了容错处理，除了可以使用“true/false”标准的Java值进行注入，还能使用“yes/no”、“on/off”、“1/0”来代表“真/假”

注入Bean ID，这里的ID是一个常量不是引用，类似于注入常量，但其可以起到错误验证功能。
俩方式：
1.<property name = "id"><idref bean = "bean1"</property>
2.<property name = "id"><idref local = "bean2"></property>
不同的地方就是第一种可以在容器初始化时验证Bean是否存在，如果不存在将抛出异常，而第二种则是Bean实际使用时才能发现传入的Bean的ID是否正确。第一种比较好点。
   