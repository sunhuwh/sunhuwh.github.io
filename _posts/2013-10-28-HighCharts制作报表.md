---
layout: post
title: HighCharts制作报表
date: 2013-10-28 23:36
categories: [jQuery, javascript, 报表]
tags: []
---
项目需求有些复杂，对问卷调查结果进行统计，先从简单弄起：

首先需要了解几个概念：
HighCharts中series的data是用来放数据的，这里的数据为数组类型的（也不知道有没有其他的类型），而且是多维数组类型的，[ [ key1,value1 ],[ key2,value2 ], [ key3,value3 ],....[ keyn,valuen  ]]。
所以要想办法将我们的数据一一对应上去。
这么想，从controller向页面传数据，穿的是这样的，穿的是一个字符串：key1,value1,key2,value2,key3,value3....keyn,valuen
这里还有个东西要必须明白，怎么在js中运用这个字符串呢？
比如传的是json，<input type="hidden" id="hiddenJson" name="hiddenJson" value="${json}">
js中：var jsons = $("#hiddenJson").val();
得到后，做成data要的样子。需要注意的一点，value肯定是一个数字，那么就需要转换。不然肯定会出错的。这个一定要记住，很重要。
大致就是这个样了。

