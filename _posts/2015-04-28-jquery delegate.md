---
layout: post
title: jquery delegate
date: 2015-04-28 23:12
categories: [jQuery]
tags: []
---
当用脚本创建html代码后，如果想触发click方法，是不能用$("a").click()的。
因为没有绑定。
需要用委托。
jQuery delegate可以帮助我们完成此事
使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。



```javascript
$("div").delegate("p","click",function(){    $(this).slideToggle();  });
```

