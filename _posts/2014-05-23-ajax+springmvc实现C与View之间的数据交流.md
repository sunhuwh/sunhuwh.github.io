---
layout: post
title: ajax+springmvc实现C与View之间的数据交流
date: 2014-05-23 00:44
categories: [E-learning, javascript, spring mvc, ajax]
tags: [js处理日期, ajax+springmvc, 回复功能]
---
jQuery.post(url, [data], [callback], [type])

url,[data],[callback],[type]String,Map,Function,StringV1.0url:发送请求地址。

data:待发送 Key/value 参数。

callback:发送成功时回调函数。

type:返回内容格式，xml, html, script, json, text, _default。

套用格式：


```javascript
$.post("test.php", function(data){
   alert("Data Loaded: " + data);
 });
```


```javascript
$.get("comment/getComments?parentId="+parentId+"&topicId="+topicId,function(data){
		var appendButton ="";
		var append = "";
		if(data!=""){
			var arr = data.split("$");
			var allTr="";
			for(var i = 0;i<arr.length;i++){
				var arr2 = arr[i].split(',');
				var name = arr2[3];
				var content = arr2[0];
				var time= "/Date("+arr2[1]+")/";
				time = DateFormat(time);
				var id = arr2[2];
				var table = "<table><tr><td>"+content+"</td></tr><tr><td>"+time+"</td></tr></table>";
				appendButton = appendButton+table+"<button type = 'button' id = 'toAddCommentId' onclick = 'replaceFrom("+parentId+",\""+name+"\""+")'>回复</button>";
			}
			appendButton = appendButton+"<button type = 'button' onclick = 'replaceFrom("+parentId+","+"\""+userName+"\""+")'>我也说一句</button>";
		}
		appendButton = appendButton+"<div id = 'commentButton' ></div><div id = 'textareaId'></div>";
		if(data==""){
			appendButton = appendButton+"<textarea id='textareaId"+parentId+"' rows='2' cols='77' validate='required' validate-message='不能为空！'  name = 'content' >@"+userName+"...."+"...."+parentId+":</textarea><button type = 'button' id = 'commentContentId' onclick = 'submit("+topicId+","+parentId+","+"\""+userName+"\""+")'>发表</button>";
		}
		$("#addCommentId"+parentId).html(appendButton);
	});
```

后台：

```java
@RequestMapping(value = "/saveAndGetComments", params = {"topicId","parentId"}, method = RequestMethod.POST)
	@ResponseBody
	public String saveAndGetComments(long topicId,Comment comment,long parentId) throws UnsupportedEncodingException{
		comment.setParentId(parentId);
		commentService.save(comment,topicId);
		List<Comment> comments=commentService.listByCommentId(parentId);
		return append(comments);
	}
	
	private String append(List<Comment> comments) {
		StringBuffer sb=new StringBuffer();
		for(int i=0;i<comments.size();i++){
			Comment comment = comments.get(i);
			sb.append(comment.getContent());
			sb.append(",");
			sb.append(comment.getCreateTime().getTime());
			sb.append(",");
			sb.append(comment.getId());
			sb.append(",");
			sb.append(comment.getUser().getName());
			if(i!=comments.size()-1){
				sb.append("$");
			}
		}
		return sb.toString();
	}
```

注意，用springmvc3的注解@responseBody来传递参数。

经常用到的js函数:
上面由于使用json来传递的数据，而js解析json传过来的日期时，不是我们想要的格式，这时需要对日期进行操作：
首先传过去的日期将它设为time传过去 date.getTime()
然后再在js中操作：


```javascript
var date= "/Date("+time+")/";
date = DateFormat(date);
```


```javascript
/**
 * 处理时间
 * @param value
 * @returns {String}
 */
function DateFormat(value) {
    var date = new Date(parseInt(value.replace("/Date(", "").replace(")/", ""), 10));
    var month = date.getMonth() + 1 < 10 ? "0" + (date.getMonth() + 1) : date.getMonth() + 1;
    var currentDate = date.getDate() < 10 ? "0" + date.getDate() : date.getDate();
    var Hours = date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
    var Minutes = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
    var Seconds = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();

    return date.getFullYear() + "/" + month + "/" + currentDate + " " + Hours + ":" + Minutes + ":" + Seconds;
}
```

