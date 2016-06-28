---
layout: post
title: thinkphp的where，页面跳转，时间配置，分页
date: 2012-11-10 18:20
categories: [NEW Thinkphp]
tags: []
---
·thinkphp里面的where函数和php里面的where运用方法不一样，但是道理是一样的。比如说这几行代码：
$condition['id']=array('gt',0);
$condition['status']=1;
$vo=$Form->where($condition)->field('id,title')->find();
只谈where，这里的意思就是where id>o and status =1 .需要注意的是，不能用><=什么的，只能用模板文件的比较标签，还可以用NOT IN  num1,num2 ;like %;or。%符号前面的内容必须得满足才可以。


·页面跳转，带有提示信息的跳转页面，如操作成功或失败跳转的特面，Action类中内置了两个方法，success和error，用于页面跳转提示，而且可以支持ajsx提交。success对应的模板就是public:success，error对应着public:error。可以使用下面的模板标签：$magTitle：操作标题，$message页面提示信息，$status操作状态 1表示成功 0表示失败 具体还可以由项目本身定义规则。$waitSecond跳转等待的时间。$jumpUrl跳转页面地址。


·对时间进行配置后，可以在刷新后看见现在的时间，模板使用{:date('H:i:s',time())}。


·import("@.ORG.Page"); //导入分页类
$count = $Form->count();    //计算总数
$p = new Page ( $count, 5 );//控制位5条一显示
