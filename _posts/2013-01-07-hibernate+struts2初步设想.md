---
layout: post
title: hibernate+struts2初步设想
date: 2013-01-07 00:13
categories: [Hibernate]
tags: []
---
当我们从action类通过execute函数传数据到jsp页面时，需要将某个字符串使用get和set函数来。

我是这样做的，专门做了一个java文件来进行增删改查，然后再在execute中使用这个类的方法来进行增删改查的。这里的配置文件，比如说hibernate.cfg.xml，主要是用来配置数据库的，其中如果要修改数据库名则改变<property name="connection.url">即可，还有一个<mapping resource="XXXX.hbm.xml"/>需要修改下。另一个配置文件XXX.hbm.xml主要是数据库字段与类中的属性的映射。
