---
layout: post
title: 富文本kindeditor
date: 2014-05-20 03:02
categories: [E-learning, Jsp]
tags: [kindeditor, 富文本, request.getContextPa, 路径]
---
kindeditor来做富文本。
springmvc+kindeditor
以前也用过，但是没有很清楚的了解kindeditor的适用方法，今天花了大量时间弄它。
首先，kindeditor能够帮助我们实现富文本的操作。
他怎么实现的呢？
看下例子就可以知道，比方说example中的simple.html:


```html
<!doctype html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>Simple Examples</title>
		<style>
			form {
				margin: 0;
			}
			textarea {
				display: block;
			}
		</style>
		<link rel="stylesheet" href="../themes/default/default.css" />
		<script charset="utf-8" src="../kindeditor-min.js"></script>
		<script charset="utf-8" src="../lang/zh_CN.js"></script>
		<script>
			var editor;
			KindEditor.ready(function(K) {
				editor = K.create('textarea[name="content"]', {
					resizeType : 1,
					allowPreviewEmoticons : false,
					allowImageUpload : false,
					items : [
						'fontname', 'fontsize', '|', 'forecolor', 'hilitecolor', 'bold', 'italic', 'underline',
						'removeformat', '|', 'justifyleft', 'justifycenter', 'justifyright', 'insertorderedlist',
						'insertunorderedlist', '|', 'emoticons', 'image', 'link']
				});
			});
		</script>
	</head>
	<body>
		<h3>默认模式</h3>
		<form>
			<textarea name="content" style="width:700px;height:200px;visibility:hidden;">KindEditor</textarea>
		</form>
	</body>
</html>

```

首先先把改用的js加载进去：

```html
<link rel="stylesheet" href="../themes/default/default.css" />
		<script charset="utf-8" src="../kindeditor-min.js"></script>
		<script charset="utf-8" src="../lang/zh_CN.js"></script>
```
然后再确定哪个textarea需要设置为富文本：


```html
<textarea id="content" name="content" style="width:700px;height:300px;"></textarea>
```

是这个。然后就进行设置：

```html
<script>
			var editor;
			KindEditor.ready(function(K) {
				editor = K.create('textarea[name="content"]', {
					resizeType : 1,
					allowPreviewEmoticons : false,
					allowImageUpload : false,
					items : [
						'fontname', 'fontsize', '|', 'forecolor', 'hilitecolor', 'bold', 'italic', 'underline',
						'removeformat', '|', 'justifyleft', 'justifycenter', 'justifyright', 'insertorderedlist',
						'insertunorderedlist', '|', 'emoticons', 'image', 'link']
				});
			});
		</script>
```

就是这么个流程，这只是最基础的。而如果复杂一点，要将图片上传到某个地方，并且自动插入到textarea标签中，怎么做呢？
在前面我做过一个图片、视频上传的一个功能:[图片上传](http://blog.csdn.net/sunhuwh/article/details/25087111)。这里就需要用到它。
先来处理上传位置的问题：
upload_json.jsp中：


```javascript
//文件保存目录路径
String savePath = pageContext.getServletContext().getRealPath("/") + "attached/";
//文件保存目录URL
String saveUrl  = request.getContextPath() + "/attached/";
```

将其改下路劲就行，我这里改成的是绝对路径。"D:/upload/"。两个都改成这。接下来解决插入图片：
在没有改变的时候，会报错，通过火狐可以看具体路径。
仔细看upload_json.jsp，会发现有个url，obj.put("url", saveUrl+newFileName);
JSONObject设置了url，就会运行该url对应的方法。我是这样设置的：


```javascript
String path = request.getContextPath();
		String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
		String picturePath = basePath+"/comment/getImage?path="+saveUrl + newFileName;
		obj.put("url", picturePath);
```

然后匹配url：

```java
@RequestMapping(value = "/getImage",params = {"path"},method = RequestMethod.GET)
    public void getImage(HttpServletResponse response,String path) throws IOException {
        File file = new File(path);
        commentService.getImage(file, response);
    }
```


```java
@Override
	public void getImage(File file,HttpServletResponse response) throws IOException {
        
        FileInputStream inputStream = new FileInputStream(file);
        byte[] data = new byte[(int)file.length()];
        inputStream.read(data);
        inputStream.close();
        
        String[] f =  file.getPath().split("\\.");
        String contentType = f[f.length-1].toLowerCase();
        //contentType = MIMEPropertiesReader.getProperty(contentType);
        response.setContentType(contentType);
        
        OutputStream stream = response.getOutputStream();
        stream.write(data);
        stream.flush();
        stream.close();
    }
```

这样就整个完成了




<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>
path IS: /jspSmartUpLoad
basePath IS: http://yangm1203.oicp.net:8080/jspSmartUpLoad/[](http://yangm1203.oicp.net:8080/jspSmartUpLoad/)
request.getScheme() IS: http
request.getServerName() IS: yangm1203.oicp.net
request.getServerPort() IS: 8080
