---
layout: post
title: initBinder解决Json日期转换为date类型
date: 2015-03-29 00:48
categories: [Spring]
tags: []
---
{‘date':’2015-01-01 00:00:00‘}
在目前springMVC3 中通过配置 annotation 注解自动封装为javaBean 对象 <mvc:annotation-driven /> ，不能将 String 日期封装为Date 日期。
解决： 通过 WebDataBinder 种的 registerCustomEditor() 方法可以进行解决这一问题，主要实现是在自己实现Controller 类中增加 如下方法即可:

```java
/**
* 前提 String 日期 转换为 javaBean 对应 Date
* @param binder
*/
@InitBinder
private void dateBinder(WebDataBinder binder) {
   // 转换日期表达式
   SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
   //创建  CustomDateEditor 对象
   CustomDateEditor editor = new CustomDateEditor(dateFormat, true);
   //注册为日期类型的自定义编辑器
   binder.registerCustomEditor(Date.class, editor);
}
```


