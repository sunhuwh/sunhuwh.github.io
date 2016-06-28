---
layout: post
title: <aop:aspectj-autoproxy/>
date: 2014-05-07 18:44
categories: [XML, Spring, E-learning]
tags: []
---
报错：
Multiple annotations found at this line:
    - cvc-complex-type.2.4.c: The matching wildcard is strict, but no declaration can be found for element 'aop:aspectj-autoproxy'.
    - schema_reference.4: Failed to read schema document 'http://www.springframework.org/schema/aop/spring-aop-3.1.xsd', because 1) could not
     find the document; 2) the document could not be read; 3) the root element of the document is not <xsd:schema>.

大概意思是读取spring-aop-3.1.xsd失败，1.没找到，2.不能被读取，3.文档根元素不是<xsd:schema>。
3.可以排除了。

先来看看为什么要使用schema

XML Schema 最重要的能力之一就是对数据类型的支持。
###通过对数据类型的支持：
- 可更容易地描述允许的文档内容
- 可更容易地验证数据的正确性
- 可更容易地与来自数据库的数据一并工作
- 可更容易地定义数据约束（data facets）
- 可更容易地定义数据模型（或称数据格式）
- 可更容易地在不同的数据类型间转换数据


另一个关于 XML Schema 的重要特性是，它们由 XML 编写。
###由 XML 编写 XML Schema 有很多好处：
- 不必学习新的语言
- 可使用 XML 编辑器来编辑 Schema 文件
- 可使用 XML 解析器来解析 Schema 文件
- 可通过 XML DOM 来处理 Schema
- 可通过 XSLT 来转换 Schema


感觉都没有什么问题，找到和读取的问题，也应该不是的，因为我在头上加了：

```html
xmlns:aop="http://www.springframework.org/schema/aop"
http://www.springframework.org/schema/aop
 http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
```

后来我想可不可能是eclipse出问题了，然后将<aop:aspectj-autoproxy/>删除后又复制了下，没问题了。
