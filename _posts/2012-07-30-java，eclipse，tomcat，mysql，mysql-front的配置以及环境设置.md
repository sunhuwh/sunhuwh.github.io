---
layout: post
title: java，eclipse，tomcat，mysql，mysql-front的配置以及环境设置
date: 2012-07-30 23:58
categories: [Web, 数据库]
tags: [eclipse, mysql, tomcat, java, wizard]
---
·java的环境变量设置。先下载jdk，最好在官网上下，下好了其实环境变量就已经设置好了。但如果是已经下好的要配置的话就直接把Java_HOME改为jdk的路径就行了。
·eclipse与tomcat的安装与配置。下载eclipse后再下载tomact，这时tomcat有个路径的设置，直接设置在jdk的jre中就行了。然后在任务栏中将tomact给关掉，在eclipse中就可以使用了。
·mysql和mysql-front的配置，先下个mysql的服务器，再下个mysql-front。注意的地方：再名为mysql server instance configuration wizard的窗口中，设置standard configuration，再在下个窗口将两个选项全部选中。
再配置这时我犯了个很低级的错误，就是一直认为password是用户名，这就是英语不达标的后果啊。还有我将服务器名给弄成是我的ip名，其实就是localhost。还好我这次算是真正的弄懂了这个。
