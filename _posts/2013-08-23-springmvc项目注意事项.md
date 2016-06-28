---
layout: post
title: springmvc项目注意事项
date: 2013-08-23 09:01
categories: [spring mvc]
tags: []
---
构建springmvc项目需要注意的地方：
要提供springmvc annotation，不然根本就不能够访问Controller类了。
默认：<mvc:annotation-driven />
<context:annotation-config/>
他的作用是式地向 Spring 容器注册
AutowiredAnnotationBeanPostProcessor、CommonAnnotationBeanPostProcessor、
PersistenceAnnotationBeanPostProcessor 以及 RequiredAnnotationBeanPostProcessor 这 4 个BeanPostProcessor。
注册这4个 BeanPostProcessor的作用，就是为了你的系统能够识别相应的注解。
第二个就是要注意路径
第三个注意是PSOT方式还是GET方式
上面是建一个很简单的项目所需要注意的，现在是将springmvc、hibernate、spring合起来使用所需要注意的：
出现问题是：tomcat启动的时候会报这样的错：
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'xx': Injection of autowired dependencies failed;
这是因为配置出错了，有些包没有扫描到，使得里面的注解根本就没有被机器解析出来。
扫描时要扫到我们使用了@Controller、@Service、@Repositoryde 的包。
还有一个主题的是，springmvc的底层与数据库的实现变了：
下面是springmvc中Controller向视图之间传数据的方式：
一：Controller→视图
通过Model对象进行传递，例：
public String index(Model model){
model.addAttribute("list", "list33");
}
视图使用该list，是用EL表达式   ${}  来获取的。
如果list是复合对象，即list有两个属性，那么：
一样可通过${list}获取，如果要它的属性，那么${list.property}
如果该list是一个集合，那么如果要循环得到其数据，视图获取方式是：
<c:forEach var="fuwa" items="${list}">
....
Model和Map传参数有什么不同
Map要更严谨一些，Map可以控制传递参数的类型。
二：视图→Controller
传简单类型，int、String
就在Controller函数声明中，@RequestParam(“”)String XX
对于对象，在视图中通过对对象的属性设值，然后在对应的方法中声明。
如果要从一个Controller跳转到另一个Controller，return “redirect:...”



