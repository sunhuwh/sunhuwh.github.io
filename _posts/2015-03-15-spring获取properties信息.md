---
layout: post
title: spring获取properties信息
date: 2015-03-15 23:32
categories: [spring mvc]
tags: []
---
class前面注解：


```java
@Configuration  
@PropertySources({  
    @PropertySource("classpath:config.properties"),  
    @PropertySource("classpath:database.properties")  
})  

```
spring推荐使用env来获取：

```java
@Autowired  
    private Environment env;  
```

