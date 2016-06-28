---
layout: post
title: bootstrap 模态框
date: 2015-06-17 22:57
categories: [jQuery]
tags: [bootstrap]
---
我们需要引入bootstrap.min.js
先创建模态框的触发装置：


```html
<button class="btn btn-primary btn-lg" data-toggle="modal"
   data-target="#myModal">
   开始演示模态框
</button>
```

data-toggle：插件，这里选择模态框。
data-target：定义模态框id的值。注意如果模态框的id="myModal"，那么data-target="#myModal"
模态框：


```html
<!-- 模态框（Modal） -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" 
   aria-labelledby="myModalLabel" aria-hidden="true">
   <div class="modal-dialog">
      <div class="modal-content">
         <div class="modal-header">
            <button type="button" class="close" 
               data-dismiss="modal" aria-hidden="true">
                  ×
            </button>
            <h4 class="modal-title" id="myModalLabel">
               模态框（Modal）标题
            </h4>
         </div>
         <div class="modal-body">
            在这里添加一些文本
         </div>
         <div class="modal-footer">
            <button type="button" class="btn btn-default" 
               data-dismiss="modal">关闭
            </button>
            <button type="button" class="btn btn-primary">
               提交更改
            </button>
         </div>
      </div><!-- /.modal-content -->
</div><!-- /.modal -->
```


class="close" ,关闭的样式
data-dismiss：表示关闭，值model
class="modal-body",模态框主体样式

还有其余的插件，使用方法跟这个类似。


