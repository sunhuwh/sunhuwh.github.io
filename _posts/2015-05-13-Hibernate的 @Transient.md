---
layout: post
title: Hibernate的 @Transient
date: 2015-05-13 00:06
categories: [Hibernate]
tags: []
---
@Transient表示该属性并非一个到数据库表的字段的映射,ORM框架将忽略该属性.
如果一个属性并非数据库表的字段映射,就务必将其标示为@Transient,否则,ORM框架默认其注解为@Basic