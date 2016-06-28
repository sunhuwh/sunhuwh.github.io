---
layout: post
title: spring mvc 过滤器-HiddenHttpMethodFilter 表单method标准化
date: 2014-05-04 20:17
categories: [简单学习网, spring mvc]
tags: []
---
浏览器form表单只支持GET与POST请求，而DELETE、PUT等method并不支持，spring3.0添加了一个过滤器，可以将这些请求转换为标准的http方法，使得支持GET、POST、PUT与DELETE请求，该过滤器为HiddenHttpMethodFilter。

HiddenHttpMethodFilter的父类是OncePerRequestFilter，它继承了父类的doFilterInternal方法，工作原理是将jsp页面的form表单的method属性值在doFilterInternal方法中转化为标准的Http方法，即GET,、POST、 HEAD、OPTIONS、PUT、DELETE、TRACE，然后到Controller中找到对应的方法。例如，在使用注解时我们可能会在Controller中用于@RequestMapping(value
 = "list", method = RequestMethod.PUT)，所以如果你的表单中使用的是<form method="put">，那么这个表单会被提交到标了Method="PUT"的方法中。
      

需要注意的是，由于doFilterInternal方法只对method为post的表单进行过滤，所以在页面中必须如下设置：


```html
<form method = "put" ...>
这种事错误的，应该是这样：
<form method = "post">


```html
<input type = "hidden" name = "_method" value = "put"/>
```


	


	

web.xml配置：




```html
<servlet>
        <servlet-name>root</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value></param-value>
        </init-param>


        <load-on-startup>1</load-on-startup>
    </servlet>


    <servlet-mapping>
        <servlet-name>root</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <filter>   
        <filter-name>HiddenHttpMethodFilter</filter-name>   
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>   
    </filter>   

    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```







   

```
