---
layout: post
title: The method decodeBuffer(String) from the type characterDecoder is not accessible due to ...
date: 2015-01-12 00:26
categories: [java, eclipse]
tags: []
---
![](http://img.blog.csdn.net/20150109110521281?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)![](http://img.blog.csdn.net/20150109110536484?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
因包加载顺序问题导致的。
解决方法：删除jar包，重新再导入。
删除：
![](http://img.blog.csdn.net/20150109110827556?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
导入：
![](http://img.blog.csdn.net/20150109110852064?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
![](http://img.blog.csdn.net/20150109110903920?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
