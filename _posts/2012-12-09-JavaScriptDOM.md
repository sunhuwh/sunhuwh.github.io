---
layout: post
title: JavaScript/DOM
date: 2012-12-09 23:51
categories: [javascript]
tags: []
---
document.cookie设置查询与当前文档相关的所有cookie。


unescape()解码对应的escape字符串


indexOf()检索参数在对应的字符串中出现的位置，如果未出现则返回-1。


substring（）参数可有2个，必须1个。都是数字类型的。表示首个位置。返回两个位置之间的字符串。


javascript的with表示什么？当有一个对象的多个属性或者方法需要操作的时候用with。


对邮箱进行验证：@位置大于1，并且第一个和@之间必须得有个.符号。根据以上两个来验证。


onMouseOver事件的作用就是告诉浏览器如果鼠标悬浮于图像之上，浏览器将执行某个函数，切换到另一个，反之onMouseOut。不过要记住设置name。


<area>是定义图像映射中的区域，总是嵌套在<map>中的。它的属性shape表示形状（鼠标区域范围的形状），coords表示坐标，如得看shape是什么形状来规定值，如果是圆形就规定圆心坐标和半径大小，如果未矩形则规定四个顶点的坐标，等等等等。target表示以何种方式打开链接，有时可以在新窗口打开(_blank)，有时本窗口打开（_top）。nohref规定区域中没有相关的链接。


如果把onMouseOver和上面的<area>联合起来就会使鼠标移动到某个区域显示某个东西。


通过javascript可进行计时操作。setTimeout() 未来的某时执行代码 ，clearTimeout() 取消setTimeout() 。第一个参数时调用的javascript的字符串，第二个指示从当前起多少毫秒后执行第一个参数。


节点，由上至下，文档节点，元素节点，文本节点，属性节点，注释节点。


同级节点：为共享用一个父节点的节点。


查找并访问节点：通过getElementById()和getElementsByTagName()方法，用
过使用一个元素节点的parentNode、firstChild以及lastChild属性。
   