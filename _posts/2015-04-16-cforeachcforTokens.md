---
layout: post
title: <c:foreach><c:forTokens>
date: 2015-04-16 21:44
categories: [HTML]
tags: []
---
<c:forEach>
<c:forEach>标签用于通用数据，它有以下属性 属 性 描 述 是否必须 缺省值 
items 进行循环的项目 否 无 
begin 开始条件 否 0 
end 结束条件 否 集合中的最后一个项目 
step 步长 否 1 
var 代表当前项目的变量名 否 无 
varStatus 显示循环状态的变量 否 无
<c:forEach begin="0" end="100" var="i" step="1">
count=<c:out value="${i}"/><br>
</c:forEach>

<c:forTokens>
<c:forTokens>标签有以下属性 属 性 描 述 是否必须 缺省值 
items 进行循环的项目 是 无 
delims 分割符 是 无 
begin 开始条件 否 0 
end 结束条件 否 集合中的最后一个项目 
step 步长 否 1 
var 代表当前项目的变量名 否 无 
varStatus 显示循环状态的变量 否 无 


例子 
<c:forTokens items="a:b:c:d" delims=":" var="token">
<c:out value="${token}"/>
</c:forTokens>
