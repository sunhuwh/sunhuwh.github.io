---
layout: post
title: Unable to read jar mainfest from C:\.....\.m2\repository\me\donnior\rtl{ title }.3\rtl-0.3.jar
date: 2014-07-14 00:23
categories: [maven, E-learning]
tags: []
---
今天碰见一个bug，弄了好长时间才解决。
昨天想集成JSF。结果导入集成JSF所需要的jar。
一运行最后报错：he absolute uri: http://java.sun.com/jsp/jstl/core cannot be resolved in either web.xml or the jar files deployed with this application] with root cause
按网上说的应该是1.1,1.2版本不同的原因：1.1不要jsp，1.2要加上jsp：
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
但是我原本就是1.2版本，且写的是<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>。所以不是这个错。所以排除这个。
但是当我将项目用svn还原，却还是报这样的错。很奇怪。将项目完全删除后再svn检出。结果依然报错。以前是完全没有这种事情的。
接下来我糊里糊涂的，将maven仓库里的东西全部给剪切掉了，然后重新导入了一遍。
现在主要说的是下面的的问题，上面
he absolute uri: http://java.sun.com/jsp/jstl/core cannot be resolved in either web.xml or the jar files deployed with this application] with root cause
这个问题怎样解决的我现在都感觉很奇怪。先说下面的问题：
用mvn eclipse:eclipse，结果：
Unable to read jar mainfest from C:\.....\.m2\repository\me\donnior\rtl\0.3\rtl-0.3.jar
在\me\donnior\rtl\0.3下明明又rtl-0.3.jar文件，但是却报错了。
弄了好长时间才发现，这里有个_maven.repositories文件，内容：


```html
#NOTE: This is an internal implementation file, its format can be changed without prior notice.
#Thu May 08 21:47:00 CST 2014
rtl-0.3.jar>=
rtl-0.3.jar>artifactory=
rtl-0.3.pom>artifactory=
```

将其改为：

```html
#NOTE: This is an internal implementation file, its format can be changed without prior notice.
#Thu May 08 21:47:00 CST 2014
rtl-0.3.jar

```

这个时候也没有报错：he absolute uri: http://java.sun.com/jsp/jstl/core cannot be resolved in either web.xml or the jar files deployed with this application] with root cause
   