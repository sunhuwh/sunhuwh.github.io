---
layout: post
title: 补充前面Java 加载Properties文件的六种方式
date: 2014-09-30 00:28
categories: [E-learning, java]
tags: []
---
有时会遇到jsp中加载properties的问题：
Properties property = new Properties();
property.load(getClass().getClassLoader().getResourceAsStream("config.properties"));
getClass().getClassLoader().getResourceAsStream("xxx.properties")
