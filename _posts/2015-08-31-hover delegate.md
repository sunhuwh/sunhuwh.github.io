---
layout: post
title: hover delegate
date: 2015-08-31 17:29
categories: [javascript]
tags: []
---
hover的代理：
因hover是由两个函数组成，这两个触发的事件是mouseenter，mouseleave
所以，可以这样代理：


```javascript
$("tbody").delegate("tr", "mouseenter", function (event) {

}).delegate("tr", "mouseleave", function (event) {

});
```

