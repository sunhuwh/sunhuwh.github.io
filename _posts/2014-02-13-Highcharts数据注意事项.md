---
layout: post
title: Highcharts数据注意事项
date: 2014-02-13 09:19
categories: [报表]
tags: []
---
Highcharts data部分必须为数|组，由于js在处理数字的时候会默认当成是字符串进行处理的，所以这个时候需要将其进行转换，
各种转换方式：
parseFloat(X)：parseFloat() 函数可解析一个字符串，并返回一个浮点数。
Number(X):转换为数字，如无法转换，返回NaX

	isNaN(X):检查是否为数字
	
	
parseInt(X):转换为整数

