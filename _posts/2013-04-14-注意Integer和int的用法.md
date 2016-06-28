---
layout: post
title: 注意Integer和int的用法
date: 2013-04-14 22:59
categories: [java]
tags: []
---
	publicstaticvoid main(String args[]){Integer a =100;Integer b =100;int aa=100;int bb=100;if(a == b){System.out.println("true");}else{System.out.println("false");}if(aa== bb){System.out.println("true");}else{System.out.println("false");}Integer c =1000;Integer d =1000;int cc=1000;int dd=1000;if(c == d){System.out.println("true");}else{System.out.println("false");}if(cc == dd){System.out.println("true");}else{System.out.println("false");}}
这会输出：
true
true
false
true

以后在用if做比较的时候，尽量尽量是int类型的做比较。

原因：

int 是基本类型，直接存数值
integer是对象，用一个引用指向这个对象
　　1.Java 中的数据类型分为基本数据类型和复杂数据类型
　　int 是前者>>integer 是后者（也就是一个类）
　　2.初始化时>>
　　int i =1;　　Integer i= new Integer(1);(要把integer 当做一个类看)
　　int 是基本数据类型（面向过程留下的痕迹，不过是对java的有益补充）
　　Integer 是一个类，是int的扩展，定义了很多的转换方法
　　类似的还有：float Float;double Double;string String等
　　举个例子：当需要往ArrayList，HashMap中放东西时，像int，double这种内建类型是放不进去的，因为容器都是装 object的，这是就需要这些内建类型的外覆类了。
　　Java中每种内建类型都有相应的外覆类。
　　Java中int和Integer关系是比较微妙的。关系如下：
　　1.int是基本的数据类型；
　　2.Integer是int的封装类；
　　3.int和Integer都可以表示某一个数值；
　　4.int和Integer不能够互用，因为他们两种不同的数据类型；
Integer类的内部, 有一个常量静态数组, 在Integer类被加载的时候, 预先创建了**-128 ~ 127**的Integer对象, 所以当声明的Integer类型变量的值在**-128
 ~ 127**的范围内时, 不会新创建对象, 直接引用数组中创建好的. 所以第一个结果会输出true，第三个结果为false；
而int是一个基本数据类型，不存在integer那样的创建对象的过程，只要数值不超过-2……31~2^31-1（对于32位的编译器来说），编译器就不会报错，所以第二个和第四个结果都是ture.



