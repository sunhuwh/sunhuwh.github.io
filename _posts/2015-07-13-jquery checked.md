---
layout: post
title: jquery checked
date: 2015-07-13 23:06
categories: [jQuery]
tags: [checked]
---
	jquery判断checked的三种方法:
	.attr('checked'):   //看版本1.6+返回:"checked"或"undefined" ;1.5-返回:true或false
	.prop('checked'): //16+:true/false
	.is(':checked'):    //所有版本:true/false//别忘记冒号哦
	
	jquery赋值checked的几种写法:
	
	所有的jquery版本都可以这样赋值:
	
	// $("#cb1").attr("checked","checked");
	// $("#cb1").attr("checked",true);
	
	jquery1.6+:prop的4种赋值:
	
	// $("#cb1").prop("checked",true);//很简单就不说了哦
	// $("#cb1").prop({checked:true}); //map键值对
	// $("#cb1").prop("checked",function(){
	return true;//函数返回true或false
