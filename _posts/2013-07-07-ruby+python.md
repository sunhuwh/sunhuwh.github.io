---
layout: post
title: ruby+python
date: 2013-07-07 01:30
categories: [ruby, python]
tags: []
---
Ruby的理念：
以人的思想为起点来进行编程。这样使得编程更直观，改变了以往从机器进行考虑的思想，使得编程时间缩短。
它的强悍之处：
动态修改对象、类型：
如这串代码：
class MyClass
  def the_method
    "general method"
  end
end
 
mc = MyClass.new
def mc.the_method
  "special for this instance."
end
 
mc.the_method
将会执行下面的方法。
Ruby具有强大的反射机制和元编程：
强到可以取出private变量、调用拦截方法。
可以与前面所说的修改对象和类型结合，来实现元编程：即可以根据程序员提供的信息 来自行生成、修改对象和类型。
还有下面这些特点：
面对对象，什么都是对象，没有基础类型。
变量也没有类型，硬是要说叫个类型，那么就是动态类型。

Python：
Python也是完全面对对象的语言，函数、模块、数字、字符串都是对象。并且完全支持继承、重载、派生、多继承，有益于增强源代码的复用性。
Python编译器本身也可以被集成到其它需要脚本语言的程序内，因此被很多人称为“胶水语言”。
Python的设计理念：用一种方法，最好是只有一种方法来做一件事。这就和java大大的不同，java是一个功能多个方法来实现。

Eclipse+PyDev插件
打开Eclipse，进入到help中的Install New Software，name随意，Location是http://pydev.org/updates。→选择PyDev，一路next。再重启。
但是接下来，配置的时候出了问题，试了很多遍，都是这样：
error getting info interpreter.
common reasons include
using an unsupport version
python and Jython require at least version 2.1 and Iron Python 2.6
specifying an invalid interpreter on Mac or Linux

