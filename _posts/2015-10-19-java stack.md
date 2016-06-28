---
layout: post
title: java stack
date: 2015-10-19 19:36
categories: [java]
tags: []
---
java stack使用时需要注意，因为statck是在内存以指针的形式存在的。
当我么add一个进去，然后remove出来。而当stack是空的时，如果再remove，就会把stack给破坏掉，从而报错。
所以使用时需要contains，然后再remove。
