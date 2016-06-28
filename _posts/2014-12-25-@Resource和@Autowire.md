---
layout: post
title: spring注解@Resource和@Autowire
date: 2014-12-25 23:10
categories: [Spring]
tags: []
---
**@Resource** 注解被用来激活一个命名资源（named resource）的依赖注入，在JavaEE应用程序中，该注解被典型地转换为绑定于JNDI context中的一个对象。 Spring确实支持使用**@Resource**通过JNDI
 lookup来解析对象，默认地，拥有与**@Resource**注解所提供名字相匹配的“bean name（bean名字）”的Spring管理对象会被注入。 在下面的例子中，Spring会向加了注解的setter方法传递bean名为“**dataSource**”的Spring管理对象的引用。


```java
@Resource(name="dataSource")
public void setDataSource(DataSource dataSource) {
this.dataSource = dataSource;
}
```
直接使用**@Resource**注解一个域（field）同样是可能的。通过不暴露setter方法，代码愈发紧凑并且还提供了域不可修改的额外益处。正如下面将要证明的，**@Resource**注解甚至不需要一个显式的字符串值，在没有提供任何值的情况下，域名将被当作默认值。


```java
@Resource
private DataSource dataSource; // inject the bean named 'dataSource'
```
该方式被应用到setter方法的时候，默认名是从相应的属性衍生出来，换句话说，命名为**'setDataSource'**的方法被用来处理名为**'dataSource'**的属性。



```java
private DataSource dataSource;

@Resource
public void setDataSource(DataSource dataSource) {
this.dataSource = dataSource;
}

<bean id="whiteNameListDao" class="xxx.impl.WhiteNameListDaoImpl" autowire="byName" /> 

@Autowired 
IWhiteNameListDao whiteNameListDao;
```

