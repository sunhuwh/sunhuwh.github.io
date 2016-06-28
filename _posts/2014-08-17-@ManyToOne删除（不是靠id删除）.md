---
layout: post
title: Hibernate@ManyToOne删除（不是靠id删除）
date: 2014-08-17 23:36
categories: [E-learning, java]
tags: []
---
当关系为@ManyToOne
目标：删除对方。
但是删除是有条件的。
比如一个班级有很多的学生。
我要依据班级的编号，来删除所有学生。
比如编号是1-1
1-2
1-3
1-4
1-5
而要模糊的删除以1开头的。
这个时候删除，将以1开头的编号都给找出来，然后循环删除。
