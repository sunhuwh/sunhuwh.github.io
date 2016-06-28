---
layout: post
title: <a>事件，criteria.createAlias
date: 2014-07-05 02:28
categories: [Jsp, E-learning, Hibernate]
tags: []
---

```html
<a href="/index.html" onmouseover="alert('Welcome');return false">测试用</a>
```
onmouseover，鼠标浮上


```java
DetachedCriteria criteria = DetachedCriteria.forClass(Course.class);
	    
		if(!Strings.isNullOrEmpty(name))criteria.add(Restrictions.like("name",name,MatchMode.ANYWHERE));
		
		//由于course和property之间的关系是，一对多
		//如果增加个查询条件，=propertyId
		//那么这样：
		if(propertyId!=0)criteria.createAlias("properties","properties")
							.add(Restrictions.eq("properties.id",propertyId)).add(Restrictions.eq("properties.id",propertyId2));
		
		//if(propertyId!=0)criteria.createAlias("properties","properties")
		//					.add(Restrictions.eq("properties.id",propertyId));
```

