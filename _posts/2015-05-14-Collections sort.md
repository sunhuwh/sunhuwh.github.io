---
layout: post
title: Collections sort
date: 2015-05-14 23:07
categories: [java]
tags: []
---
Collections.sort(logs, new Comparator<ResLog>() {

@Override

public int compare(ResLog o1, ResLog o2) {

return o1.getCreateTime().after(o2.getCreateTime())?-1:1;

}

});
当我们用Collections.sort（logs）的时候是会报错的。需要加上后面的条件。
