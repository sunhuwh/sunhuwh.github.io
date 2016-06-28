---
layout: post
title: replaceAll有$情况下报错
date: 2014-10-03 22:41
categories: [java]
tags: [replaceAll]
---
replaceAll(regex, replacement)函数，由于第一个参数支持正则表达式，replacement中出现“$”,会按照$1$2的分组模式进行匹配。
当“$”后跟的不是整数的时候会报错。

如：


```java
public class Test {
	public static void main(String[] args) {
		String str = "123ABC456";
		String re = "#7T$/#";
		System.out.println(str.replaceAll("ABC", re));
	}
}
```

解决方法：
利用split，再拼接：


```java
String[] strArr = ex.split("\\$");
StringBuffer sb = new StringBuffer();
for(int i=0;i<strArr.length-1;i++){
 sb = sb.append(strArr[i]).append("{replaceString}");
}
sb.append(strArr[strArr.length-1]);
ex = sb.toString();
```



