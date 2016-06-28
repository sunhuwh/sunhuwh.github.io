---
layout: post
title: switch string
date: 2015-04-23 01:05
categories: [java]
tags: []
---

```java
/**
 * switch String支持
 *
 */
public class SwitchTest {
	
	public static void main(String[] args){
		test("ff");
	}
	
	public static void test(String str){
		switch(str){
		case"abc":
			System.out.println("abc");
			break;
		case"def":
			System.out.println("def");	
		default:
			System.out.println("default");
		}
		
	}
	
}

```

