---
layout: post
title: lastIndexOf
date: 2014-10-01 23:42
categories: [E-learning, java, 工具]
tags: [lastIndexOf, 倒数第几个]
---
这里用lastIndexOf来找寻倒数第几个字符串在什么位置


```java
public class LastIndexOfTest {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		String Str = new String("Welcome to Tutorialspoint.com");
		String SubStr1 = new String("Tutorials" );
		String SubStr2 = new String("Sutorials" );
		
		System.out.print("Found Last Index :" );
		//最后一个
		System.out.println(Str.lastIndexOf( 'o' ));
		System.out.print("Found Last Index :" );
		//返回字符在此对象是小于或等于fromIndex,在这里是指小于或等于5的，
		//如果字符点之前不出现表示的字符序列的最后一个匹配项的索引。
		System.out.println(Str.lastIndexOf( 'o', 5 ));
		System.out.print("Found Last Index :" );
		System.out.println( Str.lastIndexOf( SubStr1 ));
		System.out.print("Found Last Index :" );
		//小于15
		System.out.println( Str.lastIndexOf( SubStr1, 15 ));
		System.out.print("Found Last Index :" );
		System.out.println(Str.lastIndexOf( SubStr2 ));
		
		//所以根据这个我们就可以找到倒数第二个的了
		//现在测试倒数第二个o在何处.结果为21，right
		System.out.println(Str.lastIndexOf('o', Str.lastIndexOf('o')-1));
		
		//写了个工具类，专门找倒数第几个的
		System.out.println(lastIndexOF(Str,"o",2));
		System.out.println(lastIndexOF(Str,"o",3));
	}
	
	/**
	 * 
	 * @param str 目标字符串
	 * @param fStr 所寻找的字符串
	 * @param num 倒数第几个
	 * @return
	 */
	protected static int lastIndexOF(String str,String fStr,int num){
		str.lastIndexOf(fStr, num);
		int indexOf = -1;
		for(int i =0;i<num;i++){
			if(i==0){
				indexOf = str.lastIndexOf(fStr);
			}else{
				indexOf = str.lastIndexOf(fStr, indexOf-1);
			}
		}
		return indexOf;
	}

}

```

