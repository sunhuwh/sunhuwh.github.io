---
layout: post
title: <a> href和onclick
date: 2014-09-22 23:42
categories: [E-learning, java]
tags: []
---

1. 链接的`onclick` 事件被先执行，其次是`href`属性下的动作（[页面跳转](http://www.so.com/s?q=%E9%A1%B5%E9%9D%A2%E8%B7%B3%E8%BD%AC&ie=utf-8&src=se_lighten_f)，或
 javascript 伪链接）；
2. 假设链接中同时存在`href` 与`onclick`，如果想让`href` 属性下的动作不执行，`onclick` 必须得到一个`false`的返回值；
3. 如果页面过长有滚动条，且希望通过链接的 `onclick` 事件执行操作。应将它的 `href` 属性设为 `javascript:void(0);`，而不要是 `#`，这可以防止不必要的页面跳动；
4. 如果在链接的 `href`属性中调用一个有返回值的函数，当前页面的内容将被此[函数的返回值](http://www.so.com/s?q=%E5%87%BD%E6%95%B0%E7%9A%84%E8%BF%94%E5%9B%9E%E5%80%BC&ie=utf-8&src=se_lighten_f)代替；
5. 在按住[Shift键](http://www.so.com/s?q=Shift%E9%94%AE&ie=utf-8&src=se_lighten_f)的情况下会有所区别。
6. 今天我遇到的问题，在IE6.0里以href的形式访问不到parentNode。
7. 尽量不要用javascript:协议做为A的href属性，这样不仅会导致不必要的触发window.onbeforeunload事件，在IE里面更会使gif动画图片停止播放。

在Javascript中void是一个操作符，该操作符指定要计算一个表达式但是不返回值。
void 操作符用法格式如下： 1. javascript:void (expression) 2. javascript:void expression
expression 是一个要计算的 Javascript 标准的表达式。表达式外侧的[圆括号](http://www.so.com/s?q=%E5%9C%86%E6%8B%AC%E5%8F%B7&ie=utf-8&src=se_lighten_f)是选的，但是写上去是一个好习惯。
 (实现版本 Navigator 3.0)
你以使用 void 操作符指定超级链接。表达式会被计算但是不会在当前文档处装入任何内容。
下面的代码创建了一个超级链接，当用户点击以后不会发生任何事。当用户链接时，void(0) 计算为 0，但 Javascript 上没有任何效果。
<A HREF="javascript:void(0)">单此处什么也不会发生</A>
下面的代码创建了一个超级链接，用户单击时会提交表单。
<A HREF="javascript:void(document.form.submit())"> 
单此处提交表单</A>
下面代码则执行了subgo()函数，
<a href="javascript:void(0)" onclick="subgo()">点我</a>
在这里，javascript:void(0),没启实质上的作用，它仅仅是一个[死链接](http://www.so.com/s?q=%E6%AD%BB%E9%93%BE%E6%8E%A5&ie=utf-8&src=se_lighten_f)，执行的函数是subgo()。
<a href="#" onclick="subgo()">点我</a>与<a href="javascript:void(0)" onclick="subgo()">点我</a>区别。
实际上 #包含了一个位置信息默认的锚是#top 也就是网页的上端 ，而javascript:void(0) 仅仅表示一个死链接，没有任何信息。所以调用脚本的时候最好用void(0)
    href一般是指向一个URL地址，也可以调用javascript ,如href="javascript:xxx();",文档中推荐这样写：<a href=" javascript:void(0)" onclick="xxx();">xx</a>,但是这种方法在复杂环境有时会产生奇怪的问题，尽量不要用javascript:协议做为A的href属性，这样不仅会导致不必要的触发window.onbeforeunload事件，在IE里面更会使gif动画图片停止播放。
**    链接的 onclick 事件被先执行，其次是 href 属性下的动作（页面跳转，或 javascript 伪链接），如果不想让href 属性下的动作执行，onclick 需要要返回 false ，一般是这样写onclick="xxx();return
 false;".**



