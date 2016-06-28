---
layout: post
title: Hibernate原理，与JDBC比较
date: 2013-01-04 23:26
categories: [Hibernate]
tags: []
---
Hibernate是一个持久化框架。
那什么是持久化呢？我们先来理解下瞬间状态，保存在内存中的程序数据在程序退出后数据就消失了，这就称之为瞬间状态。而持久状态是我们保存在了磁盘上，就成为程序数据的持久化状态。持久化就是将程序数据在瞬间状态和持久状态之间装换的机制。用JDBC完成数据在持久和瞬间状态的转换。
什么是JDBC呢？java data base connectivity，java数据库连接。是一种执行SQL语句的Java API。


JDBC和Hibernate的比较：
相同点： 1.都是JAVA的数据库操作中间件。2.两者对于数据库进行直接操作的对象都不是线程安全的，都需要及时关闭。3.两者都可以对数据库的更新操作进行显式的事物处理。
不同点：1.使用的SQL语言不同，JDBC是基于关系型数据库的标准SQL语言，Hibernate使用的是HQL（Hibernate query language）语言。2.操作的对象不同：JDBC操作的是数据，将数据通过SQL语句直接传送到数据库中执行，而Hibernate操作的是持久化对象，由底层持久化对象的数据更新到数据库中。3.数据状态不同：JDBC操作的数据时“瞬时"的，变量值无法与数据库中的值保持一致，而Hibernate操作的数据时刻持久的，就是持久化对象的数据属性的值时可以跟数据库中的值保持一致的。


ORM（对象----关系映射）：也就是对象数据到关系型数据的映射。类中的属性映射到了数据库中对应的字段中。表现层中数据传给业务逻辑层，有了对象数据，然后再通过持久化层成为了关系型数据。


Hibernate7个步骤：Configuration(Hibernate.cfg.xml)->SessionFactory(User.hbm.xml)->Session->开始一个事物->持久化操作（save,update,delete,find）->提交事物->关闭Session。
   