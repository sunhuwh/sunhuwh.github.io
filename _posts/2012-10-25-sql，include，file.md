---
layout: post
title: sql，include，file
date: 2012-10-25 19:16
categories: [sql, NEW Thinkphp]
tags: []
---
·body onload：当文档被载入时执行脚本。
 
·orde by( id desc)是什么意思？是sql的命令语句
一般是跟在查询语句末尾的
例如select * from tablename order by id desc
order by 是排序的命令
order by id就是将查询结果根据id的内容升序排列
order by id desc就是将查询结果根据id的内容降序排列
 
·clude,可以使用Include标签来包含外部的模板文件。1、 使用完整文件名包含，格式：<include file="完整模板文件名" />例如：<include file="./Tpl/default/Public/header.html" />，模板文件名必须包含后缀，使用完整文件名包含的时候，特别要注意文件包含指的是服务器端包含，而不是包含一个URL地址，也就是说file参数的写法是服务器端的路径，如果使用相对路径的话，是基于项目的入口文件位置；2、包含当前模块的其他操作模板文件，格式：<include
 file="操作名" />；3、 包含其他模块的操作模板，格式：<include file="模块名:操作名" />；4、包含其他模板主题的模块操作模板，格式：<include file="主题名@模块名:操作名" />；5、 用变量控制要导入的模版，格式：<include file="$变量名" />；6、使用快捷方式包含文件，格式：{include:模板文件规则}。
 
·htmlspecialchars是一个函数，功能是把html标签转化为字符串html。　预定义的字符是： 　　&（和号） 成为&amp; 　　" （双引号） 成为 &quot; 　　' （单引号） 成为 ' 　　< （小于） 成为 &lt; 　　> （大于） 成为 &gt;
 
·file_get_contents() 函数把整个文件读入一个字符串中。

·highlight_file() 函数对文件进行语法高亮显示。
