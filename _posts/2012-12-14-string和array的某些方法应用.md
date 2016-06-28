---
layout: post
title: string和array的某些方法应用
date: 2012-12-14 17:28
categories: [ThinkPHP]
tags: [总结]
---
substr()字符串的剪切

array_shift()数组的第一个元素删除并返回的是这个元素

arrray_pop()将最后个元素删除
字符串，split(以什么分割，规定返回数组的最大长度)，如果将第一个参数设置为了“”那么就会将其完全每个变成数组的元素。这个函数与数组的Array.join（）操作正好相反。

总结：当要添加什么功能的时候先想好该从哪个地方下手，留个印象在便签中可以写下一些东西提示自己。因为thinkphp支持mvc分层处理的。所以一般而言我们先写html，里面如果差些数据我们可以用提示来代替。最后需要的东西再从控制器中下手就可以了。现在就涉及到html和php了，除此之外就是javascript，javascript一般都是根据你想要得到什么时间而做的。而html和php，html就是根据其标签来设置，不清楚的时候就在html教程中找到相应的标签就可以解决了。php也是差不多的。

下一阶段就是用java来完成这些功能了
