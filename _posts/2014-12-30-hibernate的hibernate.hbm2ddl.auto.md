---
layout: post
title: hibernate的hibernate.hbm2ddl.auto
date: 2014-12-30 00:23
categories: [Hibernate]
tags: []
---
hibernate.hbm2ddl.auto=none

当该参数设置为none时，框架无法自动生成表，因此才有前面找不到表的异常。现将该参数取值做一个总结：
1、create
如果设置为该值，则每次加载hibernate时（准确说应是创建SessionFactory时）都会删除以前创建的表而根据model重新生成表，即使前后的表没有任何变化，通常会造成数据库数据丢失，需谨慎使用这个取值
2、create-drop
与create差不多，所不同的是每次sessionFactory关闭时，就会删除所有表
3、update
这个取值比较常用，需要先建立数据库，在第一次加载hibernate时会自动创建表，以后创建hibernate会自动根据model更新表结构，即使表结构改变了，以前的行不会被删除
4、validate
每次加载hibernate时，验证创建数据库表结构，只会和数据库中的表进行比较，不会创建新表，但是会插入新值

