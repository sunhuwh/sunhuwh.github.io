---
layout: post
title: jpa  @Temporal
date: 2015-05-13 23:49
categories: [JPA]
tags: []
---

```plain
1.日期：

@Temporal(TemporalType.DATE)
 @Column(name = "applyDate", nullable = false, length = 10)
 public Date getApplyDate() {
  return applyDate;
 }

在页面端取值：2011-04-12

 

 

 2.时间：

@Temporal(TemporalType.TIME)

在页面端取值：22:50:30

 3.日期和时间(默认)：

@Temporal(TemporalType.TIMESTAMP) 
在页面端取值：2011-04-12 22:51:34.0
```

