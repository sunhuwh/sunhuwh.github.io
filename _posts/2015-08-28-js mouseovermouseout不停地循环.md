---
layout: post
title: js mouseover/mouseout不停地循环
date: 2015-08-28 21:35
categories: [jQuery]
tags: [鼠标, mouseout, mouseover]
---
情形：
我要在鼠标经过tbody中的tr时，会产生事件。
这个事件是给tr中的td写内容，内容是带标签的，如：
	<p>abc</p>。
结果发现，当鼠标经过abc的时候会不停地产生事件。
解决方案：
用hover：
	$("#tab tr").hover(function(){
	
	}，function(){
	
	});
