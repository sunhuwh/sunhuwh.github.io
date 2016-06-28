---
layout: post
title: criterial查询
date: 2014-05-29 03:51
categories: [E-learning, Hibernate]
tags: []
---
criterial查询非常的方便，只用在Ｃ层更改就行了。


```java
criteria.add(Restrictions.like("name",name));
```

模糊查询



```java
criteria.createAlias("properties","properties")
                            .add(Restrictions.eq("properties.id",propertyId));
```
多对多查询．

查询时需要注意的是要注意有时本该是ｌｏｎｇ类型别弄成Ｓｔｒｉｎｇ或者其他的了
ｃｏｎｔｒｏｌｌｅｒ


```java
@RequestMapping(value ="/join/query" ,params={"propertyId","name"}, method = RequestMethod.GET)
	public String queryJoin(@RequestParam(value = "page", required = false, defaultValue = "1" )int page,long propertyId,String name,ModelMap model,HttpServletRequest request){
		User user = getCurrentUser(request);
		DetachedCriteria criteria = DetachedCriteria.forClass(Course.class);
	    
		if(!Strings.isNullOrEmpty(name))criteria.add(Restrictions.like("name",name));
		if(propertyId!=0)criteria.createAlias("properties","properties")
							.add(Restrictions.eq("properties.id",propertyId));
		criteria.createAlias("users","users").add(Restrictions.eq("users.id",user.getId()));
        List<Course> courses = courseService.parsel(criteria,page);
		model.addAttribute("courses", courses);
		model.addAttribute("properties", propertyService.listAll());
		
		return "/mine/course/join";
	}
```
ｄａｏ

```java
@Override
	public List<Course> parsel(DetachedCriteria criteria, int page) {
		Session session = (Session) this.entityManager.getDelegate();
		Criteria c = criteria.getExecutableCriteria(session);
		
		int count  = ((Number)(c.setProjection(Projections.rowCount()).uniqueResult())).intValue();
		
		c.setProjection(null);
		c.setFirstResult((page - 1) * DEFAULT_PAGESIZE);  
 		c.setMaxResults(DEFAULT_PAGESIZE);
 		c.setResultTransformer(CriteriaSpecification.ROOT_ENTITY);
 		
 		@SuppressWarnings("unchecked")
 		List<Course> result = c.list();
　　　　　　　　／／下面分页不用管
　　　　　　　　PaginateSupportArray<Course> paginateList = new PaginateSupportArray<Course>(result,page,DEFAULT_PAGESIZE,count);
        return paginateList;
 		
	}
```

Criteria:在线查询容器
DetachedCriteria：离线查询容器
Example:作为查询容器德参数，创建查询对象的模版
Restrictions:作为查询容器的参数，设置封装限制条件、查询条件的模版，返回类型为Criterion
Order：作为查询容器的参数，用于排序
Projections：作为查询容器的参数，用于统计，对应数据库中的聚会函数

Ｅｘａｍｐｌｅ方法还没完全弄明白，有时间再来弄




