---
layout: post
title: Caused by-- org.hibernate.MappingException-- collection foreign key mapping has wrong number of column
date: 2014-05-08 17:36
categories: [Hibernate, JPA, E-learning]
tags: []
---
模型创建错误，这个是由于继承时没注意到已经有了
 @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private Long id;

id被声明了两遍。

