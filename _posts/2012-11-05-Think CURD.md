---
layout: post
title: Think CURD
date: 2012-11-05 23:42
categories: [NEW Thinkphp]
tags: []
---
·{原样输出，可以使用literal标签来防止模板标签被解析
·file_get_contents() 函数把整个文件读入一个字符串中。·htmlspecialchars是一个函数，功能是把html标签转化为字符串html。　预定义的字符是： 　　&（和号） 成为&amp; 　　" （双引号） 成为 &quot; 　　' （单引号） 成为 ' 　　< （小于） 成为 &lt; 　　> （大于） 成为 &gt;}
·为什么在浏览器上数据显示不出来而在mysql中运行sql查询语句可以显示出来啊。就是因为数据库的名字没对。
·模型自动验证：其名字为$_validate，其格式array(验证字段，验证规则，错误提示，验证条件，附加规则，验证时间)。
`验证条件：（可选）
 Model::EXISTS_TO_VAILIDATE 或者0 存在字段就验证 （默认）
 Model::MUST_TO_VALIDATE 或者1 必须验证
 Model::VALUE_TO_VAILIDATE或者2 值不为空的时候验证

验证字段：可为数据库字段也可不为，可为密码等；
验证规则：结合附加规则即可。附加规则，包括regex正则验证（不懂），function（函数验证），callback方法验证是否属于当前Model类的一个方法。confirm验证表单中两个字段是否相同。equal验证是否等于某个值。in是否在某个范围内，必须是个数组。unique验证是否是唯一的。
还有常用的正则验证规则，require，email，currency货币，number数字，url URL地址。
·自动完成：名字$_auto,格式array(填充字段，填充内容，填充条件，附加规则);
填充条件包括：
Model::MODEL_INSERT或1表示新增时处理。
Model::UPDATE或2表示更新后处理。
Model::BOTH或3表示以上都处理。
`附加规则包括：
 function ：使用函数，表示填充的内容是一个函数名
 callback ：回调方法 ，表示填充的内容是一个当前模型的方法
 field ：用其它字段填充，表示填充的内容是一个其他字段的值
 string ：字符串（默认方式）
 
·window.setTimeout是定时功能函数。
