---
layout: post
title: java/Object类，封装类
date: 2012-04-18 23:05
categories: [java]
tags: [语言, object, equals, string, jvm]
---
##Object类
##equals方法是用来判断两个对象是否是同一个对象的，即判断它在内存中是否是同一块区域。

·当判断的是原始数据类型的类引用时，只需要根据内容来判断。否则得根据常规方法。Test14·当我们只需要判断类中的某个属性时，就可以直接覆盖父类Object的equals方法。
toString方法：·对于原始数据类型String和其他类型数据我们可以将其加起来，而对于非原始数据，我们需要通过调用“Object”的 toString方法方法来实现。Test15
Object的Hashcode（）方法是用来返回一个唯一标识一个对象的整数，在集合类中进行搜索和排序时会用到。Object的clone（）方法是用来复制一个对象的。由于protected方法，不能直接使用，必须在子类中覆盖该方法。
程序在运行时，可以通过Class对象获取对象运行时的详细信息。java中的类在装入jvm时会产生这样一个对象，该对象包含了关于这个类的各种信息。反射类难度有点大，以后再讨论。##

##封装类
记忆加理解原始数据类型和封装类原始数据类型封装类原始数据类型封装类booleanBooleancharCharacterbybeBybeshortShortintIntergerfloatFloatlongLongdoubleDouble
我们可以将原始数据类型封装成类类型。
##






