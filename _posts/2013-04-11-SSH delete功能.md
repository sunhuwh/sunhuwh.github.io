---
layout: post
title: SSH delete功能
date: 2013-04-11 12:42
categories: [SSH]
tags: []
---


```java
/**
     * @param obj
     * @param table
     * @id
     * 
     */
    
    public boolean delete(Object obj,String table,Integer id){
    	
    	String field_name="id";
    	Integer id2 = id;
    	String field_value = String.valueOf(id2);
    	String desc = null;
    	String descId = null;
    	List list = this.selete(field_name,field_value,desc,table,descId);
    	
    	for(int i=0;i<list.size();i++){
    		obj = (Object)list.get(i);
    	}
    	session.delete(obj);
    	session.beginTransaction().commit();
    	return true;
       
    }
```

跟前面写的增改查是差不多的，查询后删除对象
