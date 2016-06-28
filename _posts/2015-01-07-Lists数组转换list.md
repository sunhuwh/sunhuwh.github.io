---
layout: post
title: Lists数组转换list
date: 2015-01-07 00:01
categories: [Guava, java]
tags: []
---
将数组转换为list的时候，
尽量不要用Arrays.asList，Arrays.asList()只是把数组伪装成List，里面有些方法没有具体实现
用Lists.newArrayList();
