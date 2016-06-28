---
layout: post
title: JsonIgnore
date: 2015-04-03 23:09
categories: [java]
tags: []
---
 Jackson默认是针对get方法来生成JSON字符串的
@JsonSerialize可以过滤掉生成的json中不需要的多余字段
