---
layout: post
title: eclipse bug？
date: 2013-10-16 15:17
categories: [Jsp]
tags: []
---

```java
<%-- <c:forEach var="commonResponse" items="${commonResponses}">
			<input type="checkBox" name="response" value="${commonResponse.title}"
				<c:forEach  var="response" items="${question.responses}">
					<c:if test="${commonResponse.title == response.title}">
						checked
					</c:if>
				</c:forEach> 
								
			/>  ${commonResponse.title }<br/>
	</c:forEach> 
--%>
					
	<c:forEach items = "${commonResponses}" var="commonResponse">
		<input type = "checkBox" name = "response" value ="${commonResponse.title}" 
			<c:forEach var ="response" items = "${question.responses}">
				<c:if test="${commonResponse.title == response.title}">
					checked
				</c:if>
			</c:forEach>
		/>  ${commonResponse.title }<br/>
	</c:forEach>
					
```
上下俩一样，但是下面那个从 var开始下面都是红线，不了解怎么回事，而且还能正常运行。
将上面的那个注释给去掉后，是没有显示红线的。一模一样的俩兄弟，怎么会出现这种情况。
以后用到两个forEach时就要注意点了
