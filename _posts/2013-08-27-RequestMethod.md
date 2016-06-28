---
layout: post
title: RequestMethod
date: 2013-08-27 08:59
categories: [spring mvc]
tags: []
---

spring3.0添加了一个过滤器，可以将这些请求转换为标准的http方法，使得支持GET、POST、PUT与DELETE请求
配置：
<filter>   
<filter-name>HiddenHttpMethodFilter</filter-name>   
<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>   
</filter>   

<filter-mapping>
<filter-name>HiddenHttpMethodFilter</filter-name>
<url-pattern>/*</url-pattern>
</filter-mapping>
/** 进入新增 */
@RequestMapping(value="/new")  
     
/** 显示 */  
@RequestMapping(value="/{id}")  
      
/** 编辑 */  
@RequestMapping(value="/{id}/edit")  
     
/** 保存新增 */  
@RequestMapping(method=RequestMethod.POST)  
     
/** 保存更新 */  
@RequestMapping(value="/{id}",method=RequestMethod.PUT)  
      
/** 删除 */    
@RequestMapping(value="/{id}",method=RequestMethod.DELETE)  

/** 批量删除 */  
@RequestMapping(method=RequestMethod.DELETE)


