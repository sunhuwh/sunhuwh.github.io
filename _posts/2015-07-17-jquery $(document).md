---
layout: post
title: jquery $(document)
date: 2015-07-17 21:00
categories: [jQuery]
tags: [document, jquery]
---
$(document)意思是说，获取整个网页文档对象（类似的于window.document）
我们通过delegate做托管的时候，可以利用它：
	$(document).delegate("#id","click",function(){
	     alert("success");
	});
