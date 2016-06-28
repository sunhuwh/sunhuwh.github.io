---
layout: post
title: jstl变量作用域控制 scope
date: 2015-04-20 00:03
categories: [Jsp]
tags: []
---
<c:set var = "name" value = "csdn" scope = "request"/>
<c:set var = "name" value = "csdn" scope = "page"/>
...
暂且之说这两个，一个作用域是在本页面，一个作用域是在request中。
如果没有给定scope，默认情况是page。
所以有些情况可能需要作用域更大些，就需要设置scope。application、session、request、page
在设置变量的时候要注意，尽量设置一些易懂，并且与后台传过来的参数不同名称的。


