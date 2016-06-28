---
layout: post
title: mysql start service无响应
date: 2015-03-14 00:37
categories: [sql]
tags: []
---
今天同事装mysql，但是始终在start service那卡住，无响应。
最后究其结果是因为：
数据库只能安装一次，再次安装前必须把以前的全部卸载干净。
mysql卸载，文件删除。
注册表中一样。网上有很多关于清理注册表的：
regedit->
接着：
HKEY_LOCAL_MACHINE/SYSTEM/ControlSet001/Services/Eventlog/Applications/MySQL
HKEY_LOCAL_MACHINE/SYSTEM/ControlSet002/Services/Eventlog/Applications/MySQL
HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Eventlog/Applications/MySQL
删完

