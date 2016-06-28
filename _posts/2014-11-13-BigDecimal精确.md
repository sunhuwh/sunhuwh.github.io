---
layout: post
title: BigDecimal精确
date: 2014-11-13 23:05
categories: [java, E-learning]
tags: []
---
BigDecimal(int) 创建一个具有参数所指定整数值的对象。BigDecimal(double) 创建一个具有参数所指定双精度值的对象。BigDecimal(long) 创建一个具有参数所指定长整数值的对象。BigDecimal(String) 创建一个具有参数所指定以字符串表示的数值的对象。BigDecimal 的运算方式 不支持 + - * / 这类的运算 它有自己的运算方法BigDecimal add(BigDecimalaugend) 加法运算BigDecimal subtract(BigDecimal subtrahend) 减法运算BigDecimal multiply(BigDecimal multiplicand) 乘法运算BigDecimal divide(BigDecimal divisor) 除法运算


```java
public static void main(String[] args) {
		float a = 12345.01f;
		System.out.println(new BigDecimal(a));//12345.009765625
		
		BigDecimal volumn=new BigDecimal("0");
		System.out.println(volumn);//0
		volumn=volumn.add(new BigDecimal("1"));
		System.out.println(volumn);//1
	}
```

