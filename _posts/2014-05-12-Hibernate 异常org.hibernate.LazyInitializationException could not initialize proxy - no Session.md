---
layout: post
title: Hibernate 异常org.hibernate.LazyInitializationException could not initialize proxy - no Session
date: 2014-05-12 17:34
categories: [E-learning, servlet]
tags: []
---
关于Hibernate lazy，这个一个lazy使用后带来的异常，由于session关闭后引用了对象，而该对象本身是没有被加载。根本就没有加入内存中。
我的情况是这样的：
给了前端一个对象，该对象中与另一个对象关联着在。而我想在前端使用被引用的对象，丢出了这种异常。

所以解决方案分为两种，一个是延时加载禁止掉，第二种办法，在view层使用这些数据时，session是打开的。
第一种：lazy ="false"
第二种：使用openSessionInView。

什么是OpenSessionInView在hibernate中使用load方法时，并未把数据真正获取时就关闭了session，当我们真正想获取数据时会迫使load加载数据，而此时session已关闭，所以就会出现异常。 比较典型的是在MVC模式中，我们在M层调用[持久层](http://baike.baidu.com/view/198047.htm)获取数据时(持久层用的是load方法加载数据)，当这一调用结束时，session随之关闭，而我们希望在V层使用这些数据，这时才会迫使load加载数据，我们就希望这时的session是open着得，这就是得名Open
 Session In view 。
后来我配置了下：

```java
@WebFilter(filterName="openEntityManagerInViewFilter"
			,urlPatterns={"/*"}
			,asyncSupported=true
			 )
public class OpenEntityManagerInViewFilter extends org.springframework.orm.jpa.support.OpenEntityManagerInViewFilter{

}
```

还是不行。在OpenEntityManagerInViewFilter的doFilterInternal方法处打了断点，跑进去了，但是还是不可以。
最后只有改为用web.xml配置。
回去再弄！！！！






