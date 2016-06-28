---
layout: post
title: controller
date: 2015-07-22 23:08
categories: [java, 笔记]
tags: [回滚]
---
controller层不要将两个有紧密联系的save，update，delete放在一起，我们要考虑到如果controller层中这些个操作是否执行成功。而不成功的话会带来严重后果。
所以我们要将这些操作放在service层进行包装。然后用@Transational进行注解。这样就可以回滚
