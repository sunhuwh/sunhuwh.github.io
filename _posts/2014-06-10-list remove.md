---
layout: post
title: list remove
date: 2014-06-10 00:34
categories: [E-learning, java]
tags: []
---
案例是这样的：
list remove方法，删除的是对象，并且要判断对象是否相等再来进行删除。
通过登录将user全部存进session中。这是这个user其实是与book有着ManyToOne的关系在。user为many方。
想从book方getUsers().remove(user)。但是user是从session中取到的，相当于是该user是new的，但是他们的信息却是一模一样的。

而如果是new了一个对象，并且id及其他信息完全相同。再来remove它，那是没有任何用处的。

所以还得

```java
book.getUsers().remove(userService.findById(user.getId()));

```
根据session获取的user的id再来重新获取user。

拓展：list remove尽量少用，在数据多的时候将会很占内存。
还有list的contains同样是对于对象的，这里跟上面一样，如果是从session中获取的就需要再根据id来重新获取。
