---
layout: post
title: jQuery 多个条件检索,多条件检索的第一个和$（this）
date: 2015-06-15 01:13
categories: [jQuery, javascript]
tags: []
---

```javascript
$("input[name='aa'] [title='bb']")
```



```javascript
$(".aa:first")
```
$(this)需要上下文，如

```javascript
$(":button").click(  function(){  $(this).parent().parent().remove();  }   );
```


