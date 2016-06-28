---
layout: post
title: springmvc @ResponseBody
date: 2014-05-06 01:34
categories: [HTTP, Spring, 简单学习网, spring mvc]
tags: []
---
@ResponseBody
 将内容或对象作为 HTTP 响应正文返回，使用@ResponseBody将会跳过视图处理部分，而是调用适合HttpMessageConverter，将返回值写入输出流。
```java
@RequestMapping(params="method=view")
@ResponseBody
public String view(@RequestParam("id") Long id,
HttpServletRequest request, 
HttpServletResponse response){
...
return jsonData;
}
```

      如上可以直接返回json字符串。如果不配置@ResponseBody，也可以使用response输出数据然后 return null，达到返回json字符串的效果。      @ResponseBody之后返回字符串中中文可能会出现乱码，因为sping mvc默认是text/plain;charset=ISO-8859-1，要支持中需做如下配置：
```html
<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter">
<property name="messageConverters">
<list>
<bean class="org.springframework.http.converter.StringHttpMessageConverter">
<property name="supportedMediaTypes">
<list>
<value>text/plain;charset=UTF-8</value>
</list>
</property>
</bean>
</list>
</property>
</bean>
```


