---
layout: post
title: springmvc annotation 2
date: 2013-08-23 09:00
categories: [spring mvc]
tags: []
---
Springmvc annotation:
@PathVariable是用来对指定请求的URL路径里面的变量 eg: Java代码 @RequestMapping(value = "form/{id}/apply", method = {RequestMethod.PUT, RequestMethod.POST}) {id}在这个请求的URL里就是个变量，可以使用@PathVariable来获取。
@PathVariable和@RequestParam的区别就在于：@RequestParam用来获得静态的URL请求的参数

@ModelAttribute注释的方法会在此controller每个方法执行前被执行。
如果把@ModelAttribute用来注解一个实体类，那么这个实体类可以直接在视图中使用。如：
public String index(Model model,@ModelAttribute("o")Message o){

List<Message> list = this.messageService.getMessageList();
o.setName("user");
return "index/show";
}



