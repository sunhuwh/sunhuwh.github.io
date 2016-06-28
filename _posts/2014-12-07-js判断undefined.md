---
layout: post
title: js判断undefined
date: 2014-12-07 23:20
categories: [javascript]
tags: []
---

```javascript
<script type="text/javascript" charset="utf-8">
	var test;
	if(typeof(test)=="undefined"){
		alert("undefined");
	}
	if(test==null){
		alert("null");
	}
	if(!test){
		alert("is null");
	}
</script>
```

