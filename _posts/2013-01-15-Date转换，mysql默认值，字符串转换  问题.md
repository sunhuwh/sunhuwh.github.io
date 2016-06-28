---
layout: post
title: Date转换，mysql默认值，字符串转换  问题
date: 2013-01-15 17:01
categories: [Hibernate]
tags: [java.sql.Date, java.util.Date]
---
由于mysql中的Date型格式为0000-00-00，而java.util.Date型为long型的，所以要将其转换为java.sql.Date型的。先开始的时候我将其用SimpleDateFormat来得到了一个String型的0000-00-00，但是其储存不进db中。
方法：
Date date1 = new Date();
        long l = date1.getTime();
        java.sql.Date date = new java.sql.Date(l);
        System.out.println(date);




mysql中设置了字段为默认值的时候，hibernate却报错了，不允许为空。我想到了一个办法，那就是在储存进数据库之前，我们在action类中弄个if，如果为空，则为啥子。但是我觉得这种方法也有坏处，字段太多的时候我们弄起来就很麻烦。


遇到一个问题，jsp中我写了这个代码，input type='submit' name='typ' value="Published an article"/>传给的是一个action类，然后这个action类，
 if(typ=="Published an article"){
        theContent.setTyp(1);
        }else{
        theContent.setTyp(0);
        }但是却执行的else。
php用惯了，java比较字符串相同是用equals方法，a.equals(b);
==号就是实现两个对象内存的比对
equals就是实现两个对象内容的比对
   