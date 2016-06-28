---
layout: post
title: springMVC因表单参数不匹配报错
date: 2014-10-04 22:00
categories: [spring mvc, java, Spring]
tags: []
---
这里有三个：
一，前段时间遇到过了的:@RequestParam没有指定默认值。表单内也没定义。
二，超出spring设置的上传大小：


```java
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">  
    <!-- 设置上传文件的最大尺寸1024字节=1K，这里是10K -->  
    <property name="maxUploadSize">  
        <value>10240</value>  
    </property>
    <property name="defaultEncoding">  
           <value>UTF-8</value>  
    </property>  
</bean>
```

三，时间转换问题



```java
@SuppressWarnings("deprecation")
@RequestMapping("/test")
public String hello(HttpServletRequest request,HttpServletResponse response,
		@RequestParam(value="userName",defaultValue="佚名") String user,
		Date dateTest
){
	request.setAttribute("user", user);
	System.out.println(dateTest.toLocaleString());
	return "hello";
}
```

这里用的是Date。你是jsp上是：


```html
<input type="text" name="dateTest" value="2014-10-04">
```
这时加个转型：


```java
@InitBinder  
public void initBinder(WebDataBinder binder) {  
    SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
    dateFormat.setLenient(false);  
    binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));  
}
```






