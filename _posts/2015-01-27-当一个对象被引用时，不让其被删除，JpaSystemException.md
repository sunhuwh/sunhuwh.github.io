---
layout: post
title: 当一个对象被引用时，不让其被删除，JpaSystemException
date: 2015-01-27 22:59
categories: [JPA, java]
tags: []
---
比如：
试卷和试题分别为两个独立的对象，
现在试卷要添加试题，这个两个就是一个独立的一体。
如果要删除试题，我不允许，这个时候该怎么办?
捕捉异常。JpaSystemException


```java
try {
            resourceTypeService.delete(id);
        } catch (JpaSystemException e) {
            return "";
        }
```

也可以在其中加一些信息，如：catch完毕后输出一些信息。
