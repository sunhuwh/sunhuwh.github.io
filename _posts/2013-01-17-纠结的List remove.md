---
layout: post
title: 纠结的List remove
date: 2013-01-17 06:51
categories: [java, Hibernate]
tags: []
---
remove()这个方法最大的毛病就是改变List的结构，它会将List中想要移除的元素后面的所有元素向前移动一位。


```java
public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("java");
        list.add("C++");
        list.add("java");
        list.add("java");
        list.add("java");
        list.add("C");
        System.out.println("看看原先要删除的元素所在的位置：");
        for (int i = 0, len = list.size(); i < len; i++) {
            if (list.get(i).equals("java")) {
                System.out.println("location:" + i + ":" + list.get(i));
            }

        }
        System.out.println("看看是哪些位置的元素被删除：");
        for (int i = 0, len = list.size(); i < len; i++) {
            if (list.get(i).equals("java")) {
                System.out.println("delete:" + i + ":" + list.get(i));
                list.remove(i);
            }
        }
        System.out.println("看看现在那些剩下的元素的位置：");
        for (int i = 0, len = list.size(); i < len; i++) {
            System.out.println(i + ":" + list.get(i));
        }
    }
```
输入结果如下：
看看原先要删除的元素所在的位置：
location:0:java
location:2:java
location:3:java
location:4:java
看看是哪些位置的元素被删除：
delete:0:java
delete:1:java
delete:2:java
看看现在那些剩下的元素的位置：
0:C++
1:java
2:C

而removeAll（）则是删除了所有重复的元素。如上面的，则删除了所有的java。解决remove的方法就是反向循环：


```java
for(int i = list.size() - 1; i >= 0; i++){
    ...
}
```

