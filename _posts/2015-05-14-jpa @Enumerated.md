---
layout: post
title: jpa @Enumerated
date: 2015-05-14 23:06
categories: [JPA]
tags: []
---
@Enumerated(EnumType.STRING)

    private ActionType actionType;

ActionType是一个枚举。
但是需要注意的是，如果当第一次加载这个的时候，而我们没有加上这个注解，而下次再加入此注解，这个是没用的。
它默认是为Integer
