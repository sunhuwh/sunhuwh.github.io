---
layout: post
title: jQuery find()
date: 2015-06-15 02:04
categories: [javascript, jQuery]
tags: []
---
jQuery find方法注意，直接find()是不能取到任何数据的。
必须用find("*")来获取所有下面的子元素。
例如：


```javascript
<div id="level_one"> 
    我是最外一层的div纯文本内容 
    <div> 
        我是第二层div的纯文本内容 
        <span>jquery基础教程</span> 
        <span class="item">jquery教程</span> 
    </div> 
    <div> 
        我也是第二层div的纯文本内容 
        <span class="item">PHP学习</span> 
        <span>PHP教程</span> 
    </div> 
</div>
$("#level_one").find("*").length;//这个就是获取id为“level_one”的div中的所有的元素的个数，结果为6。 
$("#level_one").find("div").length;//会获取到2个元素 
$("#level_one").find("span").length;//会获取到4个元素 
$("#level_one").find("span.item").length;//会获取到2个元素
```

