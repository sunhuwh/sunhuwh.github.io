---
layout: post
title: jdbcTemplate SQL in
date: 2016-05-24 11:56
categories: [Spring, sql]
tags: [sql]
---
当我们in的时候，可能不能具体清楚的知道参数具体有多少。但是我们可以将这个做成变动的：
	public String placeHolder(Integer cloumsLength){
	        String wens = "";
	        for (int i=0;i<cloumsLength;i++) {
	            wens = wens+ ((i<cloumsLength-1) ? "?," : "?");
	        }
	        return wens;
	    }
上面的方法，根据参数的数目，可以得到有多少个问号。
完整的sql语句：
Integer[] ids = {1,2,3};
this.jdbcTemplate.query(“select * from courses where class_id in (“+placeHolder(ids.length)+”) “,
ids, (rs, rowNum) -> {
return this.initXXX(rs);
});
