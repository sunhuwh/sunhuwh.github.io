---
layout: post
title: GeneratedValue
date: 2015-04-03 23:09
categories: [java]
tags: []
---
@GeneratedValue和@Id一起来标注主键。
@GeneratedValue源码：


```java
@Target({METHOD,FIELD})    
    @Retention(RUNTIME)    
    public @interface GeneratedValue{    
        GenerationType strategy() default AUTO;    
        String generator() default "";    
    }
```

GenerationType：

```java
public enum GenerationType{    
    TABLE,    
    SEQUENCE,    
    IDENTITY,    
    AUTO   
}
```

TABLE：使用一个特定的数据库表格来保存主键
SEQUENS:根据底层数据库的序列来生成主键，条件是数据库支持序列。INENTITY：主键由数据库自动生成（主要是自动增长型）
AUTO：主键由程序控制
默认为AUTO
