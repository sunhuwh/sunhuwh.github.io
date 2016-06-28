---
layout: post
title: TypeError:无法获取属性“nodeName”的值：对象null或未定义
date: 2013-03-09 04:53
categories: [Struts 2]
tags: []
---
TypeError:无法获取属性“nodeName”的值：对象null或未定义
原本以为这样就可以了：result必须为jsp类型的才能显示错误信息。如果不用什么-validation.xml的话，那就必须得将错误信息写在action中了。但是同时又带来了一个问题，那就是email类型，password类型。在些Form表单时必须添上一句话validate="true"。我也不知道我在写登录界面时并没有带上这句话，但是我没有填任何东西就submit后，会显示错误信息如：email必填，password必填。但是当我也没有带上validate="true"，再验证一个action时，却不起作用了，不再显示任何错误信息。

不能显示出验证错误后的信息的原因总结：
theme不能为simple，为simple了struts标签就不能用了。
form设置添上validate="true"。

