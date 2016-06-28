---
layout: post
title: 避免NullPointException
date: 2014-10-27 22:15
categories: [E-learning, java]
tags: [NullPointException]
---

```java
public class NullPointException {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		String a = null;
		String b = "";
		//错误，这样会报空指针错误
		//equals(a,b);
		//正确
		//equals(b, a);
		
		//会报空指针错误
		valuesAndToString(a);
		//正确
		valuesAndToString(b);
	}
	
	public static boolean equals(String a ,String b){
		if(a.equals(b)){
			System.out.println("equals");
		}
		return true;
	}
	
	public static boolean valuesAndToString(String str){
		//若str为null，
		System.out.println(str.toString());
		//正确
		System.out.println(String.valueOf(str));
		return true;
	}

}

```

