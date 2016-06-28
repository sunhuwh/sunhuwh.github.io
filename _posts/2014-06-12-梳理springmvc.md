---
layout: post
title: 梳理springmvc
date: 2014-06-12 02:15
categories: [spring mvc, E-learning]
tags: []
---
流程：
1.首先用户发送请求—>前端控制器，前端控制器根据请求信息（如URL）来决定选择哪一个页面控制器进行处理并把请求委托给它。
2.页面控制器接收到请求后，进行功能处理，首先需要收集和绑定请求参数到一个对象，这个对象在Spring WebMVC中叫命令对象，并进行验证，然后将命令对象委托给业务对象进行处理；处理完毕后返回一个ModelAndView（模型数据和逻辑视图名）
3.前端控制器收回控制权，然后根据返回的逻辑视图名，选择相应的视图进行渲染，并把模型数据传入以便视图渲染
4.前端控制器再次收回控制权，将响应返回给用户
![](http://sishuok.com/forum/upload/2012/7/14/529024df9d2b0d1e62d8054a86d866c9__1.JPG)


大致了解Spring Web MVC架构图，不用太关注些细节：

![](http://sishuok.com/forum/upload/2012/7/14/57ea9e7edeebd5ee2ec0cf27313c5fb6__2.JPG)


借鉴涛哥的文章：http://jinnianshilongnian.iteye.com/blog/1594806
