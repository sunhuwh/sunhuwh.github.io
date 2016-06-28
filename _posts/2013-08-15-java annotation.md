---
layout: post
title: java annotation
date: 2013-08-15 23:55
categories: [java]
tags: []
---
Annotation用来与程序元素（类、方法、成员变量等）关联任何的信息或者任何元数据。
它从不影响java文件的运行，但是对例如编译器警告或者像文档生成器等辅助工具产生影响。
常用的annotation列表：
Annotation：名字+成员。
Annotation类型：定义了名字、类型、成员默认值。

@Override:只能用在方法之上的，用来告诉别人这一个方法是改写父类的。
@Deprecated:建议别人不要使用旧的API的时候用的,编译的时候会用产生警告信息,可以设定在程序里的所有的元素上.
@Deprecated:建议别人不要使用旧的API的时候用的,编译的时候会用产生警告信息,可以设定在程序里的所有的元素上.
通常自己设计的annotation与源代码的出入并不是很大，所以先来了解下java.lang.annotation的源文件：
1、源文件Target.java


```java
   @Documented
   @Retention(RetentionPolicy.RUNTIME)
   @Target(ElementType.ANNOTATION_TYPE)
   public @interface Target {
      ElementType[] value();
   }
```

其中的@interface是一个关键字，在设计annotations的时候必须把一个类型定义为@interface。2、源文件Retention.java


```java
   @Documented
   @Retention(RetentionPolicy.RUNTIME)
   @Target(ElementType.ANNOTATION_TYPE)
   public @interface Retention {
      RetentionPolicy value();
   }
```

比较1、2，区别并不是很大。RetentionPolicy是个java文件，源代码：


```java
    public enum RetentionPolicy {
     SOURCE,
     CLASS,
     RUNTIME
    }
```

SOURCE代表的是这个Annotation类型的信息只会保留在程序源码里，源码如果经过了编译之后，Annotation的数据就会消失,并不会保留在编译好的.class文件里面。ClASS的意思是这个Annotation类型的信息保留在程序源码里,同时也会保留在编译好的.class文件里面,在执行的时候，并不会把这一些信息加载到虚拟机(JVM)中去。
系统默认值是CLASS. RUNTIME,表示在源码、编译好的.class文件中保留信息，在执行的时候会把这一些信息加载到JVM中去的．
源文件ElementType.java：


```java
   public enum ElementType {
    TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR,
    LOCAL_VARIABLE, ANNOTATION_TYPE,PACKAGE
   }
```

＠Target里面的ElementType是用来指定Annotation类型可以用在哪一些元素上的.说明一下：TYPE(类型), FIELD(属性), METHOD(方法), PARAMETER(参数), CONSTRUCTOR(构造函数),LOCAL_VARIABLE(局部变量), ANNOTATION_TYPE,PACKAGE(包),其中的TYPE(类型)是指可以用在Class,Interface,Enum和Annotation类型上.
@Documented,@Documented的目的就是让这一个Annotation类型的信息能够显示在javaAPI说明文档上;



具体参考资料：http://qzzf1987.iteye.com/blog/564579
