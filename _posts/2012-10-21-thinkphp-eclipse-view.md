---
layout: post
title: thinkphp-eclipse-view
date: 2012-10-21 19:07
categories: [NEW Thinkphp]
tags: [xhtml, user, html, div, 数据库, 浏览器]
---
·view-url-Trace-timt-include-hello-form-db-curd不懂得百度，实在不懂立刻放下，问。必须搞懂每行代码，搞懂后blog记下来。虽然不懂里面的东西是什么，但要弄懂是什么结构，得到的是什么，语法是什么样的。
`protected:同一个类、继承的类可以访问protected成员，但是不能访问private成员；public全公开；private，Private 变量只能在包含其声明的模块中使用。
·模型的实例化：1.M函数实例化基础模型类，这是在没有定义任何模型的时候才能使用的。只能完成最基本的CURD操作。2.而D函数是实例化自定义的模型类。调用跨项目模型需要使用$User->D("User","Admin");//实例化Admin项目下的user模型。3.实例化空模型类，如果只是进行sql语句的查询，实例化空模型类即可操作。4.实例化其他模型类，就按其字面上的理解就很清晰了。由于第一种方法只支持基础操作，一些额外的逻辑方法很难封装起来的。如果需要的话就可以用$User
 = M('User', 'CommonModel');或者$User = new CommonModel("User");
`field()设置要查询的数据库字段,起标识作用。
·limit（）查询限制。
·assign(name,value='') 模板变量赋值。
·display() 输出模板.
`视图模型，用于多表联合查询。举个例子：‘Category'=>array('title'=>'categoryName');表示BlogView还包含category模型里面的title字段。
·htnl中的这行代码是什么含义：<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">。该标记用来说明你用的XHTML或者HTML是什么的版本。如果删除可能会导致该文件在用浏览器打开时乱码。
 
 
N:表明哪个早期Netscape版本支持这个标签 
E:表明哪个早期InternetExplorer版本支持这个标签 
DTD:表明符合XHTML的版本 
DTD何级别的定义了trict（严格）,Transitional（过渡）Frameset（框架） 
开始标签用途（Purpose）NNIEDTD
`load标签也支持同时导入多个资源文件，甚至是不同类型的资源文件。
·<div> 可定义文档中的分区或节。<div> 是一个块级元素。换行是它的固有的唯一格式表现。
