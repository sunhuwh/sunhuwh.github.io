---
layout: post
title: List subList()
date: 2015-06-04 00:18
categories: [java]
tags: []
---
一见到这个方法，就很容易想起String subString方法。
但是使用这个方法注意了：
当List Father如果使用subList，生成List children。
但是如果我们接下来对List Father再次进行操作，如添加，List children也会跟着添加该元素。remove是一样的。
例：


```java
public class SubListDemo
{
    public static void main(String[] args)
    {
        System.out.println("---------------ArrayList------------");
        subListTest(new ArrayList<Integer>());
        System.out.println("---------------LinkedList------------");
        subListTest(new LinkedList<Integer>());
    }
 
    private static void subListTest(List<Integer> list)
    {
        if(list == null)
        {
            throw new IllegalArgumentException("Argument " + list + " is null.");
        }
        for(int i = 0; i<5; i++)
        {
            list.add(i);
        }
         
        List<Integer> subList = list.subList(2, list.size());
        // 期望输出和实际输出一致，都是[0, 1, 2, 3, 4]
        System.out.println("Original list: " + list); 
        // 期望输出和实际输出一致，都是[2, 3, 4]
        System.out.println("Sublist:       " + subList);
         
        subList.add(10);
        // 但这里，实际输出结果却可能会出乎我们的意料，我们可能会认为输出结果不变，
 // 但却发现实际输出结果竟然变化了，比原先多了个元素10，变为 [0, 1, 2, 3, 4, 10]
        System.out.println("Original list: " + list);
        // 期望输出和实际输出一致，都是[2, 3, 4, 10]
        System.out.println("Sublist:       " + subList);
    }
}
```
如果想要避免这种情况，直接new一个Lists.newArr...
