---
layout: post
title: 前台怎么接收spring @ResponseBody返回的json数据 map
date: 2014-08-08 00:24
categories: [Spring, E-learning]
tags: [ResponseBody]
---
传的时候设键值：
比如要传一个用户的id及他的名字，就
Map<Stirng,String> map = Maps.newHashMap();
map.put("id",id);
map.put("name",name);
然后获取的话就是:
data.id
data.name
