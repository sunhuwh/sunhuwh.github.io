---
layout: post
title: Address already in use
date: 2014-07-12 00:43
categories: [tomcat, E-learning]
tags: []
---
自安装的tomcat程序设置开机自动运行,或者在之前运行过,先关闭ecplipse或jbuilder,在任务管理器中找到Tomcat的进程,将其 kill掉,即可.有时候Tomcat非法关闭时,在进程中,仍然存在,仍然占用8080端口.所以只要将其进程杀掉.就可以解决.

