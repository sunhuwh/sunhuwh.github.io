---
layout: post
title: instanceof
date: 2014-08-23 00:06
categories: [java, E-learning]
tags: [instanceof]
---

```java
public interface  A  {
	
	
}
```



```java
/**
 * 
 * @author thinkpad
 * Description :父类,实现接口A
 */
public class B implements A{
}
```


```java
/**
 * 
 * @author thinkpad
 * Description :子类,继承B
 */
public class C extends B{
}
```


```java
public class InstanceTest {
    
	
	@Test
	public void testBestPractice() {
		A ab = new B();
        A ac = new C();
 
        B bb = new B();
        B bc = new C();
 
        C cc = new C();
 
 
        //..instanceof A
        System.out.println("ab instanceof A = " + (ab instanceof A));//ab instanceof A = true
        System.out.println("ac instanceof A = " + (ac instanceof A));//ac instanceof A = true
        System.out.println("bb instanceof A = " + (bb instanceof A));//bb instanceof A = true
        System.out.println("bc instanceof A = " + (bc instanceof A));//bc instanceof A = true
        System.out.println("cc instanceof A = " + (cc instanceof A));//cc instanceof A = true
        System.out.println("null instanceof A = " + (null instanceof A));//null instanceof A = false
        System.out.println("-------------------------------------");//
        //..instanceof B
        System.out.println("ab instanceof B = " + (ab instanceof B));//ab instanceof B = true
        System.out.println("ac instanceof B = " + (ac instanceof B));//ac instanceof B = true
        System.out.println("bb instanceof B = " + (bb instanceof B));//bb instanceof B = true
        System.out.println("bc instanceof B = " + (bc instanceof B));//bc instanceof B = true
        System.out.println("cc instanceof B = " + (cc instanceof B));//cc instanceof B = true
        System.out.println("null instanceof B = " + (null instanceof B));//null instanceof B = false
        System.out.println("-------------------------------------");
        //..instanceof C
        System.out.println("ab instanceof C = " + (ab instanceof C));//ab instanceof C = false
        System.out.println("ac instanceof C = " + (ac instanceof C));//ac instanceof C = true
        System.out.println("bb instanceof C = " + (bb instanceof C));//bb instanceof C = false
        System.out.println("bc instanceof C = " + (bc instanceof C));//bc instanceof C = true
        System.out.println("cc instanceof C = " + (cc instanceof C));//cc instanceof C = true
        System.out.println("null instanceof C = " + (null instanceof C));//null instanceof C = false
        System.out.println("-------------------------------------");//
    }
	
}

```

