---
layout: post
title: springmvc解决post中文乱码问题
date: 2014-06-12 02:16
categories: [E-learning, spring mvc]
tags: []
---
org.springframework.web.filter.CharacterEncodingFilter解决中文乱码
web.xml配置的：


```html
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>utf-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

注解配置的：

```java
import javax.servlet.annotation.WebFilter;
import javax.servlet.annotation.WebInitParam;

/**
 * 项目启动时，配置请求编码的过滤器
 */
@WebFilter(filterName = "characterEncodingFilter"
			, urlPatterns = { "/*" }
			,asyncSupported=true
			,initParams={
				@WebInitParam(name="encoding" ,value="UTF-8"),
				@WebInitParam(name="forceEncoding",value="true")
			})
public class CharacterEncodingFilter extends org.springframework.web.filter.CharacterEncodingFilter {

}
```

