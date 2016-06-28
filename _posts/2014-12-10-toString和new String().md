---
layout: post
title: toString和new String()
date: 2014-12-10 23:31
categories: [java]
tags: []
---
一个对象toString()方法如果没有被重写,那么默认调用它的父类Object的toString()方法,而Object的toString()方法是打印该对象的hashCode,一般hashCode就是此对象的内存地址!
--------------------------------------------------------------------------------------------------------------------------------------

Object 类的 toString 方法返回一个字符串，该字符串由类名（对象是该类的一个实例）、at 标记符“@”和此对象哈希码的无符号十六进制表示组成。换句话说，该方法返回一个字符串，它的值等于:
getClass().getName() + '@' + Integer.toHexString(hashCode())
--------------------------------------------------------------------------------------------------------------------------------------

一个数组，在java中，数组是一个对象。
每一个对象都有toString方法，默认情况下，toString方法的返回值是该对象的哈希码，除非某些特别的类把toString方法重载了，才可能返回一些有意义的东西。

很显然，数组对象的toString方法没有被重载，因此它返回的是该对象的哈希码，举例：也就是[C@35ce36
--------------------------------------------------------------------------------------------------------------------------------------
本质上说，是因为String类的构造方法：String(char[])和Object类的toString()不同。一个返回char[]的数值，一个返回引用地址。java
 API是这么写的：

public String(char[] value)
Allocates a new String so that it represents the sequence of characters currently contained in the character array argument. The contents of the character array are copied; subsequent modification of the character array does not affect the newly
 created string. 

toString
public String toString()Returns a string representation of the object.

