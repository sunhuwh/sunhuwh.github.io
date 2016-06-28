---
layout: post
title: java try catch finally
date: 2014-09-24 00:16
categories: [java, E-learning]
tags: []
---

```java
/**
 * （假设方法需要返回值） 
java 的异常处理中， 
在不抛出异常的情况下，程序执行完 try 里面的代码块之后，该方法并不会立即结束，而是继续试图去寻找该方法有没有 finally 的代码块， 
如果没有 finally 代码块，整个方法在执行完 try 代码块后返回相应的值来结束整个方法； 
如果有 finally 代码块，此时程序执行到 try 代码块里的 return 语句之时并不会立即执行 return，而是先去执行 finally 代码块里的代码， 
若 finally 代码块里没有 return 或没有能够终止程序的代码，程序将在执行完 finally 代码块代码之后再返回 try 代码块执行 return 语句来结束整个方法； 
若 finally 代码块里有 return 或含有能够终止程序的代码，方法将在执行完 finally 之后被结束，不再跳回 try 代码块执行 return。 
 *
 */
public class TryCatchFinallyTest {


	/**
	* @param args
	*/
	public static void main(String[] args) {
		//tryCatchTest();
		//tryCatchFinallyTest();
		tryCatchFinallyTest2();
	}
	
	public static boolean tryCatchTest(){
		try {
			int a = 1/0;
			System.out.println("下面这行代码执行了！");
			return true;
		}catch(Exception e){
			System.out.println("跳到这行代码中！");
			return false;
		}
	}
	
	public static boolean tryCatchFinallyTest(){
		try {
			int a = 1/0;
			System.out.println("try执行了！");
			return true;
		}catch(Exception e){
			System.out.println("跳到catch中！");
			return false;
		}finally{
			System.out.println("跳到finally");
		}
	}
	
	public static boolean tryCatchFinallyTest2(){
		try {
			int a = 1/1;
			System.out.println("try执行了！");
			return true;
		}catch(Exception e){
			System.out.println("跳到catch中！");
			return false;
		}finally{
			System.out.println("跳到finally");
		}
	}
	
}

```

