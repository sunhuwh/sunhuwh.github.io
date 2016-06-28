---
layout: post
title: list remove-----删除数据
date: 2014-12-17 23:36
categories: [java]
tags: []
---

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;


public class RemoveTest {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		remove();
		forRemove();
	}
	
	public static boolean remove(){
		List<String> list=new ArrayList<String>();
		list.add("hello");
		list.add("world1");
		list.add("world2");list.add("world3");
		list.add("world4");
		
		
		for(Iterator<String>it=list.iterator();it.hasNext();){
			String s=(it.next());
			System.out.println(s);
			it.remove();
		}

		
		System.out.println(list);
		return true;
	}
	
	public static boolean forRemove(){
		List<String> list=new ArrayList<String>();
		list.add("hello");
		list.add("world1");
		list.add("world2");list.add("world3");
		list.add("world4");
		/**
		 * 根据时间来进行删除（用这个方法的目的是为了定期清理一些数据）
		 */
		/*for(String o:list){
		  if(o.createTime-currentT>xxx){
		     list.remove(o);
		  }
		}*/
		for(String s: list){
			list.remove(s);
		}
		return true;
		//会报错，具体查看源代码，源代码调用fastRemove(index);
		 /*private void fastRemove(int index) {
		        modCount++;
		        int numMoved = size - index - 1;
		        if (numMoved > 0)
		            System.arraycopy(elementData, index+1, elementData, index,
		                             numMoved);
		        elementData[--size] = null; // Let gc do its work
		    }*/
		//这里实际上是让数组先位移，后删除最后一个。
		/*以数组打比方：每次执行完fastRemove, 集合里面的数组的size直接就减小1了。同时后面的数组内的对象全部被左移。 
		也就是说： 
		[0,1,2,3] 
		执行for循环第一轮变为-> [1,2,3] 
		第二轮的时候，指针已经指向了2， 此时 1就被留了下来，并且没有被做任何处理。。 */
	}

}

```

