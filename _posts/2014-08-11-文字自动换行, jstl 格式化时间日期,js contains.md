---
layout: post
title: 文字自动换行, jstl 格式化时间日期,js contains
date: 2014-08-11 00:01
categories: [Jsp, E-learning, javascript]
tags: [文字自动换行, jstl 格式化时间日期, js contains]
---
文字自动换行；
加style="word-break:break-all"



```html
<fmt:formatDate value="${date}" /><br/>
<!-- 2014-8-9 -->

<fmt:formatDate value="${date}" type="time" /><br/>
<!-- 16:34:33 -->

<fmt:formatDate value="${date}" type="both" /><br/>
<!-- 2014-8-9 16:34:33 -->

<fmt:formatDate value="${date}" dateStyle="short" /><br/>
<!--14-8-9  -->

<fmt:formatDate value="${date}" dateStyle="medium" /><br/>
<!-- 2014-8-9 -->

<fmt:formatDate value="${date}" dateStyle="long" /><br/>
<!--2014年8月9日  -->

<fmt:formatDate value="${date}" dateStyle="full" /><br/>
<!-- 2014年8月9日 星期六 -->

<fmt:formatDate value="${date}" pattern="yyyy/MM/dd  HH:mm:ss" /><br/>
<!-- 2014/08/09 16:34:33 -->

<fmt:formatDate value="${date}" pattern="yyyy/MM/dd  HH:mm:ss" var="d" />
${d}<br/>
<!-- 2014/08/09 16:34:33 -->

<!-- 有时不能换行，就需要使用word-break:break-all来自动换行 -->
<p style="word-break:break-all"></p>

<button onclick="indexOf()">测试indexOf</button>		
		
<script>
	//js中没有contains，但是可以通过indexOf来实现是否包含
	function indexOf(){
		var a = "a";
		var b="ab";
		if(b.indexOf(a)==-1){
			alert("b中没有a");
		}else{
			alert("b中有a");
		}
	}
		
</script>		
```

