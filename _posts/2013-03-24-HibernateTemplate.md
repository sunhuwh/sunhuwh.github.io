---
layout: post
title: HibernateTemplate
date: 2013-03-24 06:13
categories: [Spring]
tags: []
---
HibernateTemplate，Spring的Template-callback机制在Hibernate的实现提供了org.springwork.orm.hibernate3.HibernateTemplate类与org.spring.orm.hibernate3.HibernateCallback接口，所以要用到他们，首先要加入spring-orm.jar包。它们有什么作用呢？：


```java
HibernateTemplate hibernateTemplate = new Hibernate(seeionFactory);
HibernateTemplate.execute(new HibernateCallback(){
   public Object doInHibernate(Session session)throw Exception{
      return sesssion.load(User.class);
   }
}
);
```
将上面执行完毕后就可以实Session对象自动关闭。自动建立HibernateCallback对象，除了上面的load()以外，还能使用get(),save(),delete()等方法。不过load()有些不同，如果使用Session的load()方法，将会使用到Hibernate3默认的延时功能，执行完毕后会直接关闭Session，若再次取得User的属性，将会发生错误。这里我们就比较下get(),load()，


```java
public User find(Integet id){
    User user = (User)getTemplate().get(User.class.id);
    return user;
}
```

```java
public User find(final Integer id){
    User user = (User)hibernateTemplate.execute(public Object doInHibernate(Session session)throw HibernateException,SQLExeception{
    User user = (User)session.load(User.class,id);
    Hibernate.initalize(user);
    return user;

});
    return user;
}
```
二者区别：

	1.get()采用立即加载方式,而load()采用延迟加载;
	   get()方法执行的时候,会立即向数据库发出查询语句,
	   而load()方法返回的是一个代理(此代理中只有一个id属性),只有等真正使用该对象属性的时候,才会发出sql语句
	2.如果数据库中没有对应的记录,get()方法返回的是null.而load()方法出现异常ObjectNotFoundException
	

Hibernate编程事物管理得与JDBC的事务管理结合起来看。

