---
layout: post
title: hql regexp
date: 2014-07-02 02:11
categories: [E-learning, Hibernate]
tags: []
---
今天出了一个小错误，太不注意了，在这里记下：


```java
@Override
	public List<Chapter> findChildByCourseId(String sortCode, Long id) {
		String queryString = "from Chapter c where (c.course.id=?) and (regexp(c.sortCode,?)=1) ";
        Object[] objects = { "^" + sortCode + "-[0-9]*$" };
        return executeQueryWithoutPaging(queryString,id,objects);
	}
```
objects是同事定义的，我没有注意，就改成上面那样，报错都没报错，不过查询不是这个这么查的。


```java
public List<Chapter> findChildByCourseId(String sortCode, Long id) {
		String queryString = "from Chapter c where (c.course.id=?) and (regexp(c.sortCode,?)=1) ";
	    String sortCodeString = "^" + sortCode + "-[0-9]*$";
	    return executeQueryWithoutPaging(queryString,id,sortCodeString);
	}
```

