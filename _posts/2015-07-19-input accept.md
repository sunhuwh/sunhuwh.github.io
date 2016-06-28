---
layout: post
title: input accept
date: 2015-07-19 23:59
categories: [HTML]
tags: [chrome]
---
input accept是为了上传文件时，浏览器选择什么类型文件而存在的。
比如:
`html 

 <input type="file" name="pic" accept="image/gif,image.jpg" /> 
`
将寻找gif,jpg格式的文件。
功能很强大，但是chrome不兼容。
只能用js来获取文件的后缀，继而判断是否符合文件类型了。
