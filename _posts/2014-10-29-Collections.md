---
layout: post
title: Collections
date: 2014-10-29 23:51
categories: [E-learning, java]
tags: [Collections]
---

```java
package com.boventech.learning.test.collection;

import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

import com.google.common.collect.Lists;

public class Test {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//最小值
		min();
		//最大值
		max();
		//打乱顺序
		intList();
		//拷贝n个
		nCopiesList();
		//排序
		sort();
		//对半查找
		binarySearch();
		//复制
		copy();
		//获取某个元素在集合中出现的次数。
		frequency();
		//第一次出现的位置
		indexOfSubList();
		//最后一次出现的位置
		lastIndexOfSubList();
		//
		checkedList();
		//反转列表中的元素顺序。
		reverseCandidate();
		//两个列表中是否有重复
		disjoint();
		//使用指定的元素替换List中的数据
		fill();
		//替换指定的元素
		replaceAll();
		//利用索引交换位置
		swap();
		//将索引前面的部分放到最后去
		rotate();
		//倒序放入另一个list中
		reverseOrder();
	}
	
	public static void min(){
		List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);
		// 6
		System.out.println("min:"+java.util.Collections.min(intList));
	}
	
	public static void max(){
		List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);
		// 99
		System.out.println("max:"+java.util.Collections.max(intList));
	}
	
	public static void intList(){
		List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);
		Collections.shuffle(intList);
		// 一次测试的结果
		// [6, 18, 33, 24, 99, 9]
		System.out.println("intList:"+intList);
	}
	
	public static void nCopiesList(){
		// 生成一个由10个100组成的整数列表
		List<Integer> nCopiesList = Collections.nCopies(10, 100);
		//[100, 100, 100, 100, 100, 100, 100, 100, 100, 100]
	    System.out.println("nCopiesList:"+nCopiesList);
	}
	
	public static void sort(){
		List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);
		Collections.sort(intList);
		System.out.println("sort:"+intList);
	}
	
	
	public static void binarySearch(){
		List<Integer> intList = Arrays.asList(33, 24, 18, 6, 9, 99);
		Collections.sort(intList);
		System.out.println("binarySearch:"+intList);
	}
	
	
	public static void copy(){
		List<String> listOne = Arrays.asList("A", "B", "C", "D");
	    List<String> listTwo = Arrays.asList("X", "Y", "Z");
	    Collections.copy(listOne, listTwo);
	    System.out.println("copy:"+listOne);// [X, Y, Z, D]
	    System.out.println("copy:"+listTwo);//[X, Y, Z]
	}
	
	public static void frequency(){
		List<String> testList = Arrays.asList("A", "B", "C", "D","A");
		int freq = Collections.frequency(testList, "A");
		// 1
		System.out.println("frequency:"+freq);
	}
	
	public static void indexOfSubList(){
		int index = Collections.indexOfSubList(Arrays.asList("A", "B", "C"),
	            Arrays.asList("B"));
	    // Print 1
	    System.out.println("index:"+index);
	}
	
	public static void lastIndexOfSubList(){
		int lastIndex = Collections.lastIndexOfSubList(
		        Arrays.asList("A", "B", "C", "B"), Arrays.asList("B"));
		// Print 3
		System.out.println("lastIndexOfSubList:"+lastIndex);
	}
	
	public static void checkedList(){
		List<String> stringList = Arrays.asList("A", "B", "C", "D");
		List<String> typeSafeList = Collections.checkedList(stringList, String.class);
		List integerList = Lists.newArrayList();
		integerList.add(1);
		integerList.add(2);
		integerList.add(3);
		integerList.add("a");
		List<Integer> typeSafeList2 = Collections.checkedList(integerList, Integer.class);
		System.out.println("checkedList:"+typeSafeList2);
		//[A, B, C, D]
		System.out.println("checkedList:"+typeSafeList);
	}
	
	public static void reverseCandidate(){
		List<String> reverseCandidate = Arrays.asList("A", "B", "C");
	    Collections.reverse(reverseCandidate);
	    // [C, B, A]
	    System.out.println("reverseCandidate:"+reverseCandidate);
	}
	
	public static void disjoint(){
		List<String> list3 = Arrays.asList("A", "B", "C", "D");
		List<String> list4 = Arrays.asList("X", "Y", "Z");
		boolean disJoint = Collections.disjoint(list3, list4);
		// true
		System.out.println(disJoint);
	}
	
	public static void fill(){
		List<String> testList = Arrays.asList("A", "B", "C", "D");
		Collections.fill(testList, "Z");
		// [Z, Z, Z, Z]
		System.out.println(testList);
	}
	
	public static void replaceAll(){
		List<String> replaceAllCandidate = Arrays.asList("A", "B", "C");
	    // 将A用Z代替
	    Collections.replaceAll(replaceAllCandidate, "A", "Z");
	    // [Z, B, C]
	    System.out.println(replaceAllCandidate);
	}
	
	public static void swap(){
		List<String> swapCandidate = Arrays.asList("A", "B", "C");
	    // 首尾元素交换
	    Collections.swap(swapCandidate, 0, 2);
	    // [C, B, A]
	    System.out.println(swapCandidate);
	}
	
	public static void rotate(){
		List<String> rotateList = Arrays.asList("A", "B", "C", "D", "E", "F");
		// [F, A, B, C, D, E]
		// Collections.rotate(rotateList, 1);
		// System.out.println(rotateList);
		 
		Collections.rotate(rotateList, 3);
		// [D, E, F, A, B, C]
		System.out.println(rotateList);
	}
	
	public static void reverseOrder(){
		List<String> reverseOrderTest = Arrays.asList("A", "B", "C", "D", "E",
		        "F");
		Comparator c = Collections.reverseOrder();
		Collections.sort(reverseOrderTest, c);
		// [F, E, D, C, B, A]
		System.out.println(reverseOrderTest);
	}
	
	
}

```

