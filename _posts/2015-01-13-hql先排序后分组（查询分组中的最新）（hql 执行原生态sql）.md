---
layout: post
title: hql先排序后分组（查询分组中的最新）（hql 执行原生态sql）
date: 2015-01-13 23:34
categories: [java, Hibernate]
tags: []
---
如果用这种方法进行查询：


```java
String queryString = "select * from (select * from resource r order by r.createTime desc) t group by t.resId";
Query query = entityManager.createQuery(queryString);
```

会报错，因为Hibernate不支持这种查询。


```java
select * from (select * from resource r order by r.createTime desc) t group by t.resId
```
是原生态的sql查询。
所以可以利用:


```java
Query query = entityManager.createNativeQuery(queryString, Resource.class);
```

createNativeQuery来创建一个实例的查询执行一个原生SQL查询。

注意：查询语句必须使用的是原生的sql。而有时实体名和表名会不一致，这时就需要注意一些。
