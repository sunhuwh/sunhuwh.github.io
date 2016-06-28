---
layout: post
title: Include,html原样输出，调试
date: 2012-10-28 19:52
categories: [NEW Thinkphp]
tags: []
---
`竟然遗漏了这点，Include标签重新理解。没错，include标签是用来包含外部的模板文件的。它还有功能，进行参数的传递。例如<include file='Public:block' title='这是体育新闻' list='sportList' />这段很明显与通常情况下的不同，因为它多了后面的title....，它们就是为了传递参数而存在的。怎么使用它们所传的参数呢，就比如说这个[title]即可。包含多个模板文件就是用逗号将它们隔开就行了。

·原样输出，可以使用literal标签来防止模板标签被解析。
`输出某个变量是开发过程中经常会用到的调试方法，除了使用php内置的var_dump和print_r之外，ThinkPHP框架内置了一个对浏览器友好的var_dump方法，用于输出变量的信息到浏览器查看。
我们可以使用下面的方法输出错误信息：
halt($msg)  //输出错误信息，并中止执行
·模型调试：
在模型操作中 ，为了更好的查明错误，经常需要查看下最近使用的SQL语句，我们可以用getLastsql方法来输出上次执行的sql语句。
