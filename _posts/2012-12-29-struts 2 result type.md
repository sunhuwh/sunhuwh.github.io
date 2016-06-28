---
layout: post
title: struts 2 result type
date: 2012-12-29 20:24
categories: [Struts 2]
tags: []
---
chain          用来处理Action链，将一个action的执行与另外一个配置好的action串连起来。用第一个action的getter方法和第二个action的setter方法来完成action之间属性的复制。      com.opensymphony.xwork2.ActionChainResult     

dispatcher          用来转向JSP页面，这是默认的结果类型，假如在action配置中没有配置其他的结果类型，它就会被使用org.apache.struts2.dispatcher.ServletDispatcherResult   

freemaker          处理FreeMarker模板          org.apache.struts2.views.freemarker.FreemarkerResult       

httpheader          控制非凡HTTP行为的结果类型           org.apache.struts2.dispatcher.HttpHeaderResult      

redirect          重定向到一个URL            org.apache.struts2.dispatcher.ServletRedirectResult      

redirectAction        重定向到一个Action        org.apache.struts2.dispatcher.ServletActionRedirectResult       

stream          向浏览器发送InputSream对象，通常用来处理文件下载，还可用于返回AJAX数据         org.apache.struts2.dispatcher.StreamResult      

velocity          处理Velocity模板         org.apache.struts2.dispatcher.VelocityResult       

xslt         处理XML/XLST模板         org.apache.struts2.views.xslt.XSLTResult      

plainText          显示原始文件内容，例如文件源代码        org.apache.struts2.dispatcher.PlainTextResult
