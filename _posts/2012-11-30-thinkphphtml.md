---
layout: post
title: tp/html
date: 2012-11-30 17:16
categories: [thinkphp, HTML]
tags: []
---
·tr属性bgcolor，行的背景颜色。但是HTML 4.01中不赞成使用这种属性，要用CSS进行代替。<tr style = "background-color:red">


·td属性，跨列：colspan。以后这么，关于什么的标签直接找寻，看里面的属性有哪些符合。


·无意中发现了csdn的bug，发表评论中如果发送多了字就会显示不出来，哎，我是说自己弄的blog按照csdn一样的弄怎么会出问题，搞了半天csdn就是个错的。


·当title过长后，另外三个就会缩短。。。终于搜到了，可以用自动换行解决，这是td是使用的， style="WORD-BREAK: break-all; WORD-WRAP: break-word"。就这样就够了。

·去掉表格中间的线，td属性添加style="border:0px"

