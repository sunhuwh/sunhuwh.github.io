---
layout: post
title: java for循环多变量和for each
date: 2012-12-27 23:46
categories: [java]
tags: []
---
java,for循环，多个变量一起循环：for(a=1,b=2,c=3;a<b;a++,b--,c++){}逗号隔开就行。
String[] arr {"a","b","c"}以下两种方法等效。
for(String a:arr){System.out.println(a);}
for(int i=0;i<arr.length;i++){System.out.println(arr[i]);}

