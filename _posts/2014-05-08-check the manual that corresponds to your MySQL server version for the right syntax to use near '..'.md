---
layout: post
title: check the manual that corresponds to your MySQL server version for the right syntax to use near '..'
date: 2014-05-08 17:36
categories: [Hibernate, E-learning, JPA]
tags: []
---
[School InFormatization -->]-->ERROR{SchemaUpdate.java:212}-Unsuccessful: create table group (id bigint not null auto_increment, createTime datetime, updateTime datetime, primary key (id)) ENGINE=InnoDB
  [School InFormatization -->]-->ERROR{SchemaUpdate.java:213}-You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'group (
        id bigint not null auto_increment,
        createTime datetime,
' at line 1

原因是因为group是关键字属性，group换个名字后就好了。
一定要记住这一点，关键字是不能做表名的！！！
