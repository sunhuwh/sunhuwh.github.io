---
layout: post
title: tp/字符串拼接，volist循环
date: 2012-11-15 23:51
categories: [thinkphp]
tags: []
---
当var_dump出现问题的时候，将调试里面的sql语句放进mysql中运行，因为thinkphp不管怎么变化，他总得与mysql产生关系，但是mysql只认识sql语句，所以都可看做是sql语句。


反省字符串拼接，由于很长时间没写sql语句了，结果里面的一些很小的细节给忘记了，比如说SELECT * FROM think_content
WHERE title='任意'。里面就是一个''搞忘记了就会导致我出错很长时间都找不出来，这就是细节。而虽然我把细节找出来了，但是却忘记字符串拼接怎么拼了。先把调试中的sql语句与原本是怎样的sql语句进行比较，然后再利用字符串拼接完成。


volist出来的结果，比如说是这个
array(2) { [0]=> array(6) { ["id"]=> string(1) "1" ["title"]=> string(9) "发顺丰" ["contents"]=> string(6) "撒旦" ["date"]=> string(10) "2012-08-16" ["typ"]=> string(1) "1" ["classification"]=> string(6) "真的" } [1]=> array(6) { ["id"]=> string(1) "2" ["title"]=>
 string(12) "沙发沙发" ["contents"]=> string(18) "啊实打实为期" ["date"]=> string(10) "2012-08-14" ["typ"]=> string(1) "1" ["classification"]=> string(6) "tittle" } [2]=> array(6) { ["id"]=> string(1) "4" ["title"]=> string(9) "大使馆" ["contents"]=> string(9) "艾丝凡" ["date"]=>
 string(10) "2012-08-14" ["typ"]=> string(1) "1" ["classification"]=> string(6) "tittle" },其中就只有3条记录，如果是volist循环，如果不加id循环，因为是个多维数组，所以需要用键名定位。但是如果给其用id定位了的话，id就代表了当前循环的变量，也就是这里面的0.1.2等等。如果是foreach进行循环，而他的语法形式是foreach(name = ''   item = ''） ,这就很像是php里面的foreach循环了。
   