---
layout: post
title: sqlDate和javaDate互转
date: 2014-11-02 23:47
categories: [java, E-learning]
tags: []
---

```java
package com.boventech.learning.test.date;

import java.sql.Date;

public class Test {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		java.util.Date jDate = new java.util.Date();
		java.sql.Date sDate = new java.sql.Date(jDate.getTime());
		System.out.println(sDate);
		
		java.sql.Date  date = Date.valueOf("2014-01-08");
		long time = date.getTime();
		java.util.Date uDate = new java.util.Date();
		uDate.setTime(time);
		System.out.println(uDate);
	}

}

```

