---
layout: post
title: Hibernate Annotation配置主键生成策略
date: 2013-05-05 11:36
categories: [Hibernate]
tags: []
---
通过annotation来映射hibernate实体的，基于annotation的hibernate主键标识为@Id
其生成规则由**@GeneratedValue**设定的，这里的@Id和@GenertedValue都是JPA的标准用法
JPA提供的四种标准用法为**TABLE，SEQUENCE，IDENTITY，AUTO**
**TABLE**:使用一个特定的数据库表格来保存主键
**SEQUENCE**:根据地层数据库的序列来生成主键，条件是数据库支持序列，主要是Oracle
**IDENTITY**:主键由数据库自动生成(主要是自动增长型)
**AUTO**:主键由程序控制

**SEQUENCE**
**[java]**[view plain](http://blog.csdn.net/itmyhome/article/details/7460378# "view plain")[copy](http://blog.csdn.net/itmyhome/article/details/7460378# "copy")1. /* 
2.  * name属性表示该表主键生成策略的名称，它被引用在@GeneratedValue中设置的"generator"值中。 
3.  * sequenceName属性表示生成策略用到的数据库序列名称。 
4.  */  
5. @Entity  
6. @SequenceGenerator(name="shcoolSQN",sequenceName="school_SQN")  

**[java]**[view plain](http://blog.csdn.net/itmyhome/article/details/7460378# "view plain")[copy](http://blog.csdn.net/itmyhome/article/details/7460378# "copy")1. /* 
2.      * 属性stragegy 生成的策略类型 
3.      * generator  
4.      */  
5.     @Id  
6.     @GeneratedValue(strategy=GenerationType.SEQUENCE,generator="shcoolSQN")  


**IDENTITY**
**[java]**[view plain](http://blog.csdn.net/itmyhome/article/details/7460378# "view plain")[copy](http://blog.csdn.net/itmyhome/article/details/7460378# "copy")1. @Id  
2.     @GeneratedValue(strategy=GenerationType.IDENTITY)  


**AUTO****[java]**[view plain](http://blog.csdn.net/itmyhome/article/details/7460378# "view plain")[copy](http://blog.csdn.net/itmyhome/article/details/7460378# "copy")1. @Id  
2.     @GeneratedValue(strategy=GenerationType.AUTO)  


**Hibernate主键策略生成器**

hibernate提供多种主键生成策略，有点是类似于JPA 有的是hibernate特有：

**native**: 对于oracle采用sequence方式，对于 MySql和sql server采用identity(自增主键生成机制)
            native就是将主键的生成工作交由数据库完成

**uuid**: 采用128位的uuid算法生成主键，uuid被编码为一个32位16进制数字的字符串占用空间大(字符串类型)

**identity**:使用SQL Server和MySQL的自增字段，这个方法不能放到Oracle中，Oracle不支持自增字段，要设定sequence

**sequence**: 调用底层数据库的序列来生成主键，要设定序列名 不然hibernate无法找到

increment: 插入数据的时候hibernate会给主键添加一个自增的主键，但是一个hibernate实例就维护一个计数器，所以在多个实例运行的时候不能使用这个方法

foreign: 使用另外一个相关联的对象的主键，通常和<one-to-one>联系起来使用。

guid: 采用数据库底层的guid算法机制。对应MySQl的uuid()函数 SQL Server的newid()函数 Oracle的sys_guid()函数
   