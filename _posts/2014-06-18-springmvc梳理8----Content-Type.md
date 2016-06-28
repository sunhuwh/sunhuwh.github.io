---
layout: post
title: springmvc梳理8----Content-Type
date: 2014-06-18 02:08
categories: [spring mvc, E-learning]
tags: [Content-Type]
---

```java
@Controller
@RequestMapping("/requestContentType")
public class RequestContentTypeController {
	
	
    @RequestMapping(value = "/ContentType", method = RequestMethod.GET)
    public String showForm() throws IOException {
        //form表单，使用application/x-www-form-urlencoded编码方式提交表单
        return "/contentType/index";
    }
    
    @RequestMapping(value = "/ContentType", method = RequestMethod.POST, 
    		headers = "Content-Type=application/x-www-form-urlencoded")
    public String request1(HttpServletRequest request) throws IOException {
        //得到请求的内容区数据的类型
        String contentType = request.getContentType(); 
        System.out.println("========ContentType:" + contentType);
        //得到请求的内容区数据的编码方式，如果请求中没有指定则为null
        //CharacterEncodingFilter这个过滤器设置了编码(UTF-8)
        //编码只能被指定一次，即如果客户端设置了编码，则过滤器不会再设置
        String characterEncoding = request.getCharacterEncoding();
        System.out.println("========CharacterEncoding:" + characterEncoding);
        
        //表示请求的内容区数据为form表单提交的参数，此时我们可以通过request.getParameter得到数据（key=value）
        System.out.println(request.getParameter("realname"));
        System.out.println(request.getParameter("userName"));
        return "index";
    }
}
```




```html
<form valid="true" action="<c:url value="/requestContentType/ContentType"/>" method="post" enctype="application/x-www-form-urlencoded">
	  <p>登录名：</p>
	  <p>
	      <input type="text" name=userName  validate="required" 
	      validate-message="用户名不能为空！"></input>
	  </p>
	  
	  <p>really登录名：</p>
	  <p>
	      <input type="text" name="realname"  validate="required" 
	      validate-message="用户名不能为空！"></input>
	  </p>
	  <p class="button">
	      <input type="submit" class="load" value="确定" />
	  </p>
	</form>
```

form的enctype="application/x-www-form-urlencoded"，在提交时请求的内容类型头为“Content-Type:application/x-www-form-urlencoded”；
上面是设置请求的内容类型头为“Content-Type:application/x-www-form-urlencoded”。
下面设置响应头的内容类型：


```java
    @RequestMapping("/response/ContentType")
    public void response1(HttpServletResponse response) throws IOException {
        //表示响应的内容区数据的媒体类型为html格式，且编码为utf-8(客户端应该以utf-8解码)
        response.setContentType("text/html;charset=utf-8");
        //写出响应体内容
        response.getWriter().write("<font style='color:red'>hello</font>");
    }

```

Content-Type的作用：![](http://dl.iteye.com/upload/attachment/0074/8072/27814e77-86c8-3dbf-83f1-94f118e5ded9.jpg)

指定内容体的媒体类型。

如果用生产者和消费者来解释：
![](http://dl.iteye.com/upload/attachment/0074/8076/0c0271ea-80c5-3d35-9fcb-0c0e25e40cb8.jpg)


spring3.1中就引用了这个：
@RequestMapping(value = "/consumes", consumes = {"application/json"})：此处使用consumes来指定功能处理方法能消费的媒体类型，其通过请求头的“Content-Type”来判断。
@RequestMapping(value = "/produces", produces = "application/json")：表示将功能处理方法将生产json格式的数据，此时根据请求头中的Accept进行匹配，如请求头“Accept:application/json”时即可匹配;
代码没什么太大改动：


```java
@RequestMapping(value = "/ContentType2", method = RequestMethod.GET)
    public String showForm2() throws IOException {
        //form表单，使用application/x-www-form-urlencoded编码方式提交表单
        return "/contentType/index2";
    }
    
    @RequestMapping(value = "/ContentType2", method = RequestMethod.POST, consumes = {"application/x-www-form-urlencoded"})
    public String request2(HttpServletRequest request) throws IOException {
        //得到请求的内容区数据的类型
        String contentType = request.getContentType(); 
        System.out.println("========ContentType:" + contentType);
        //得到请求的内容区数据的编码方式，如果请求中没有指定则为null
        //CharacterEncodingFilter这个过滤器设置了编码(UTF-8)
        //编码只能被指定一次，即如果客户端设置了编码，则过滤器不会再设置
        String characterEncoding = request.getCharacterEncoding();
        System.out.println("========CharacterEncoding:" + characterEncoding);
        
        //表示请求的内容区数据为form表单提交的参数，此时我们可以通过request.getParameter得到数据（key=value）
        System.out.println(request.getParameter("realname"));
        System.out.println(request.getParameter("userName"));
        return "index";
    }
    
    @RequestMapping(value = "/response/ContentType2",produces = "text/html;charset=utf-8")
    public void response2(HttpServletResponse response) throws IOException {
        //表示响应的内容区数据的媒体类型为html格式，且编码为utf-8(客户端应该以utf-8解码)
        //response.setContentType("text/html;charset=utf-8");
        //写出响应体内容
        response.getWriter().write("<font style='color:red'>hello</font>");
    }
```

感谢涛哥：http://jinnianshilongnian.iteye.com/blog/1695047


