---
layout: post
title: js replace
date: 2014-08-15 00:21
categories: [javascript, E-learning]
tags: [replace]
---

```javascript
var stringObj="师父，师父"; 
             var newstr=stringObj.replace("师父","师傅");
             alert(newstr);
```

如果适用上面的方式，最后出来的智慧是师傅，师父。而不是师傅，师傅
使用正则表达式对象可以解决这个问题，即：


```objc
var reg=new RegExp("师父","g"); //创建正则RegExp对象
             var stringObj="师父，师父"; 
             var newstr=stringObj.replace(reg,"师傅");
             alert(newstr);
```

这样结果才是师傅，师傅

