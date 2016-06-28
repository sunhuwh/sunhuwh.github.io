---
layout: post
title: java/while和do-while循环,for循环
date: 2012-03-06 18:47
categories: [java]
tags: []
---
1. while循环先判断->决定是否执行循环
2.do-while是先执行循环->判断是否->再继续看是否
3.while(a<15000){
            Sysout(“A工资为:"+a)
   do{
          Sysout("A工资为:"+a)
       }while(a<15000)
4.for循环：先执行初始化循环；然后执行判断，先调用，后执行循环体的内容，将变量值打印出来;然后再才执行参数修改的部分。就是先判断再执行。
