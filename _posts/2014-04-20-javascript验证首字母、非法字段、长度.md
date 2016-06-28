---
layout: post
title: javascript验证首字母、非法字段、长度
date: 2014-04-20 22:36
categories: [javascript, 简单学习网]
tags: []
---

```javascript
function isLegal(ch){
	if(ch >= '0' && ch <= '9')return true;
	if(ch >= 'a' && ch <= 'z')return true;
	if(ch >= 'A' && ch <= 'Z')return true;
	return false;
}
function length(str1){
	if(str1.length < 4 || str1.length > 16){
		return false;
	}
	return true;
}

function isAllLegal(str1){
	if(length(str1)){
		for (var i=0; i<str1.length; i++) {
			if(i==0){
				if(!((str1[i]>="a"&&str1[i]<="w")||(str1[i]>="A"&&str1[i]<="W"))){
				    return false;
				}
			}
			if (!isLegal(str1.charAt(i))){
				return false;
			}
		}
	}else{
		return false;
	}
	return true;
}

```



