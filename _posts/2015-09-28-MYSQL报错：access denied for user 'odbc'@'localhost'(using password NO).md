---
layout: post
title: MYSQL报错--access denied for user 'odbc'@'localhost'(using password NO)
date: 2015-09-28 19:58
categories: [mysql]
tags: [mysql]
---
几个可能：
1. 用户名、密码错误，所以无法访问
2. 数据库端设置了IP访问权限，不能用localhost访问。换成具体的IP地址试试。
3. 数据库端设置了相关操作权限，该用户没有create权限。
跑命令行：
mysql -u root -p获取权限
mysql>use mysql;使用哪个数据库
