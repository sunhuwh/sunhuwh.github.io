---
layout: post
title: JQuery validate验证规则
date: 2014-04-19 09:19
categories: [jQuery]
tags: []
---
> //定义中文消息
> var cnmsg = {
> required: “必选字段”,
> remote: “请修正该字段”,
> email: “请输入正确格式的电子邮件”,
> url: “请输入合法的网址”,
> date: “请输入合法的日期”,
> dateISO: “请输入合法的日期 (ISO).”,
> number: “请输入合法的数字”,
> digits: “只能输入整数”,
> creditcard: “请输入合法的信用卡号”,
> equalTo: “请再次输入相同的值”,
> accept: “请输入拥有合法后缀名的字符串”,
> maxlength: jQuery.format(“请输入一个长度最多是 {0} 的字符串”),
> minlength: jQuery.format(“请输入一个长度最少是 {0} 的字符串”),
> rangelength: jQuery.format(“请输入一个长度介于 {0} 和 {1} 之间的字符串”),
> range: jQuery.format(“请输入一个介于 {0} 和 {1} 之间的值”),
> max: jQuery.format(“请输入一个最大为 {0} 的值”),
> min: jQuery.format(“请输入一个最小为 {0} 的值”)
> };
> jQuery.extend(jQuery.validator.messages, cnmsg);
***
## Jquery Validate 验证规则
(1)required:true              必输字段
(2)remote:”check.php”         使用ajax方法调用check.php验证输入值
(3)email:true                 必须输入正确格式的电子邮件
(4)url:true                   必须输入正确格式的网址
(5)date:true                  必须输入正确格式的日期
(6)dateISO:true               必须输入正确格式的日期(ISO)，例如：2009-06-23，1998/01/22 只验证格式，不验证有效性
(7)number:true                必须输入合法的数字(负数，小数)
(8)digits:true                必须输入整数
(9)creditcard:                必须输入合法的信用卡号
(10)equalTo:”#field”          输入值必须和#field相同
(11)accept:                   输入拥有合法后缀名的字符串（上传文件的后缀）
(12)maxlength:5               输入长度最多是5的字符串(汉字算一个字符)
(13)minlength:10              输入长度最小是10的字符串(汉字算一个字符)
(14)rangelength:[5,10]        输入长度必须介于 5 和 10 之间的字符串”)(汉字算一个字符)
(15)range:[5,10]              输入值必须介于 5 和 10 之间
(16)max:5                     输入值不能大于5
(17)min:10        
