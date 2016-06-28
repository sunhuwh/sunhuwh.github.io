---
layout: post
title: <%@ attribute 中的参数使用jsp表达式来获取
date: 2015-04-20 00:03
categories: [Jsp]
tags: []
---
rtexprvalue的全称是 Run-time Expression Value， 它用于表示是否可以使用JSP表达式.
当在<attribute>标签里指定<rtexprvalue>true</rtexprvalue>时， 表示该自定义标签的某属性的值可以直接指定或者通过动态计算指定
如：<%@ attribute name="href" required="true" type="java.lang.String" rtexprvalue="true" %>
