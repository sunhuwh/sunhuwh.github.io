---
layout: post
title: spring @responsebody（死循环）
date: 2014-05-25 03:13
categories: [E-learning, ajax, json]
tags: [responsebody, .get, .post, JsonBackReference, JsonManagedReference]
---
@responsebody是一个非常好的方法去解决我们传递map，list给js，而且他传过去的不是xml，xml解析起来特别麻烦。
虽然他很好，但是用起来却不一定那么容易。
当传递一个list，而这个list关联到了另一个对象时，就会发生死循环的现象。一般情况我们是不会调用。在不调用的时候可以适用一个注解将那些属性给注解起来。
@JsonBackReference，@JsonManagedReference这两个注解可以帮助将那些不需要的属性给忽略掉。
但是如果是一个一对一，而现在一定要用到一对一另一端里面的属性时，而他却被忽略掉了。所以这时要换一种办法了。
我用的是用一个类将所有要的属性全部封装起来，然后实例化，设置所有的属性。
例子：
这是那个类：


```java
public class CommentAndUserWrapper {
	
	
	/**
	 * 评论内容
	 */
	private String content;
	
	/**
	 * 评论id
	 */
	private Long id;
	
	
	/*评论者
	 */
	private String name;
	
	
	private Date createTime;


	public String getContent() {
		return content;
	}


	public void setContent(String content) {
		this.content = content;
	}


	public String getName() {
		return name;
	}


	public void setName(String name) {
		this.name = name;
	}


	public Date getCreateTime() {
		return createTime;
	}


	public void setCreateTime(Date createTime) {
		this.createTime = createTime;
	}


	public Long getId() {
		return id;
	}
	
	
}

```

service层实例化了它，并进行设值，然后都存到list中去了。最后将其对应到map中（其实也可以不用）

```java
@Override
	public HashMap<String, Object> getCommentAndUserWrapper(long parentId) {
		List<Comment> comments = commentDao.listByCommentId(parentId);
		List<CommentAndUserWrapper> wrappers = Lists.newArrayList();
		for(Comment comment:comments){
			CommentAndUserWrapper cWrapper = new CommentAndUserWrapper();
			cWrapper.setName(comment.getUser().getName());
			cWrapper.setContent(comment.getContent());
			cWrapper.setCreateTime(comment.getCreateTime());
			wrappers.add(cWrapper);
		}
		HashMap<String, Object> model = Maps.newHashMap();
		model.put("data", wrappers);
		model.put("success", true);
		return model;
	}
```

controller中就只用调用这个方法即可：

```java
@ResponseBody
	public HashMap<String, Object> getComments(long parentId,long topicId,HttpServletResponse response,JsonConfig jsonConfig){
		return commentService.getCommentAndUserWrapper(parentId);
		
	}
```

js怎么解析？做了一个方法专门用来处理传过来的data


```javascript
function appendButtonAndTextarea(data,parentId,userName){
	var appendButton ="";
	if(data.data!=null){
		$.each(data.data, function(i, item){
			var name = item["name"];
			var content = item["content"];
			var time= "/Date("+item["createTime"]+")/";
			time = DateFormat(time);
			var id = item["id"];
			var table = "<table><tr><td>"+content+"</td></tr><tr><td>"+time+"</td></tr></table>";
			appendButton = appendButton+table+"<button type = 'button' id = 'toAddCommentId' onclick = 'replaceFrom("+parentId+",\""+name+"\""+")'>回复</button>";
		});
		appendButton = appendButton+"<button type = 'button' onclick = 'replaceFrom("+parentId+","+"\""+userName+"\""+")'>我也说一句</button>";
	}
	return appendButton;
}
```
总结：最主要的是要想到去使用一个类将这些要用到的属性给包装起来。我先开始想到的是直接在controller中建个list，然后把那些想要的属性的值全部都给存到里面去，然后再在js用进行解析。
那种方法很不规范，而且代码重用性不高。
联想：有一种更好的办法，只用设置需要的属性。
我做不出来，今天做了很长时间但是最后还是卡住了。以后有时间再去解决，现在先记住流程
流程是这样的：
做一个数组，里面是需要的属性，还有加上该属性所属的哪个类。因为后来要从类中调用get方法。String[] properties = {};Course.class。还要一个list，这个list是查询出来的数据。我们要从数据中淘到一些有用的数据出来。
有一个专门的类去接收传过来的数组，并根据类名和属性名来获取get方法。
然后循环courseList,就有course对象了。course对象再利用上面的get方法来获取到许多的值，将其存放好即可。
我卡住就是卡在这里，如果course里面有个user对象，我需要使用user对象里面的name怎么办呢？
整个user传过去也没用。




