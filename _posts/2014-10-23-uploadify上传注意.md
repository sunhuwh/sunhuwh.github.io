---
layout: post
title: uploadify上传注意
date: 2014-10-23 23:08
categories: [E-learning, java]
tags: []
---
上传的时候，session是不能跟着上传一起传的。
如果上传的方法，被权限拦截器给拦截了，而拦截器是不能读取到session的。这个时候在上传的时候会报302错误。
所以这时，不要将上传方法写到这种被拦截的地方。
'uploader'       : ROOT_PATH+'courseware/update/upload', 

