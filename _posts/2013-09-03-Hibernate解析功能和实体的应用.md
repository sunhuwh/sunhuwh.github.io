---
layout: post
title: Hibernate解析功能和实体的应用
date: 2013-09-03 15:43
categories: [JPA, Hibernate]
tags: []
---
1.页面向Controller传数组，Controller这边该怎么写
页面中有个多选，name为id,在Controller中RequestParam(value = "Id")long[] id;


2.content实体中将置顶设置为boolean了，而存进数据库的时候是0,1。这该怎么办。
实体和数据库的对应和操作实体又如何对应着操作数据库的，是通过Hibernate来完成。Hibernate在中间解析。例如：现在有条查询语句：
From Content c where c.user = ? And c.name = "xxx";
由于数据库只能读取SQL语句，而Hibernate在其中就会将上面的语句解析成SQL语句。
这个时候user是怎么才能得到的呢？实体中定义user是这么定义的，多对一，延时加载，joinColumn为user_id。
所以最后数据库中是没有user这个字段的，而是通过user_id来关联的。
所以Hibernate会帮我们自动进行解析，如果我们传过来了一个user，那么最后转换成c.user_id = user.getId();最后成这个样子：
Select * from content as c where c.user_id = userId And c.name = "xxx";
这个是向数据库发送请求的过程，而数据库响应，是怎么样的呢？
假如得到的是一条记录，那么Hibernate就会将这些数据都封装到Content的实例中去。
这个时候又存在着对应关系了，假如Content这个类中有个boolean类型的属性top，那么Hibernate也会自动进行解析，因为实体中为boolean的属性，它在数据库中的表现是tinyInt类型的，true为1，false为0。解析过程top==0?false:true;
说这个意思就是，理解Hibernate的解析功能和实体的应用。
