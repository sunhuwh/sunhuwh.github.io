---
layout: post
title: jquery validate maxlength汉字及hibernate regexp
date: 2014-05-09 17:27
categories: [E-learning, jQuery]
tags: []
---
maxlength:5 输入长度最多是5的字符串(汉字算一个字符)

SELECT * FROM property WHERE sortCode  REGEXP '^[0-9]-[0-9]$'

##Hibernate3.x 支持MySQL的regexp的办法
		Regexp的语法：
		
	字符含意/做为转意，即通常在"/"后面的字符不按原来意义解释，如/b/匹配字符"b"，当b前面加了反斜杆后//b/，转意为匹配一个单词的边界。 
	-或- 
	对正则表达式功能字符的还原，如"*"匹配它前面元字符0次或多次，/a*/将匹配a,aa,aaa，加了"/"后，/a/*/将只匹配"a*"。
	^匹配一个输入或一行的开头，/^a/匹配"an
	 A"，而不匹配"An a"$匹配一个输入或一行的结尾，/a$/匹配"An a"，而不匹配"an A"*匹配前面元字符0次或多次，/ba*/将匹配b,ba,baa,baaa+匹配前面元字符1次或多次，/ba*/将匹配ba,baa,baaa?匹配前面元字符0次或1次，/ba*/将匹配b,ba(x)匹配x保存x在名为$1...$9的变量中x|y匹配x或y{n}精确匹配n次{n,}匹配n次以上{n,m}匹配n-m次[xyz]字符集(character
	 set)，匹配这个集合中的任一一个字符(或元字符)[^xyz]不匹配这个集合中的任何一个字符[/b]匹配一个退格符/b匹配一个单词的边界/B匹配一个单词的非边界/cX这儿，X是一个控制符，//cM/匹配Ctrl-M/d匹配一个字数字符，//d/
	 = /[0-9]//D匹配一个非字数字符，//D/ = /[^0-9]//n匹配一个换行符/r匹配一个回车符/s匹配一个空白字符，包括/n,/r,/f,/t,/v等/S匹配一个非空白字符，等于/[^/n/f/r/t/v]//t匹配一个制表符/v匹配一个重直制表符/w匹配一个可以组成单词的字符(alphanumeric，这是我的意译，含数字)，包括下划线，如[/w]匹配"$5.98"中的5，等于[a-zA-Z0-9]/W匹配一个不可以组成单词的字符，如[/W]匹配"$5.98"中的$，等于[^a-zA-Z0-9]。
	

