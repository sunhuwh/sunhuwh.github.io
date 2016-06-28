---
layout: post
title: uploadify参数
date: 2014-11-30 23:56
categories: []
tags: []
---
##上传的时候由于文件过大，3G，4G，就很可能造成data得不到：
'onUploadSuccess':function(file, data, response)
就会造成报错的。
要将successTimeout设置大一些。
##

##Uploadify3.2参数
Uploadify Version 3.2
**Options选项设置**
auto    选择文件后自动上传
buttonClass    给“浏览按钮”加css的class样式
buttonCursor    鼠标移上去形状：arrow箭头、hand手型（默认）
buttonImage    鼠标移上去变换图片
buttonText    按钮文字
checkExisting    在目录中检查文件是否已上传成功（1 ture,0 false）
debug        是否显示调试框（默认不显示false）
fileObjName    设置一个名字，在服务器处理程序中根据该名字来取上传文件的数据。默认为Filedata，$tempFile = $_FILES['Filedata']['tmp_name']
fileSizeLimit    设置允许上传文件最大值B, KB, MB, GB 比如：'fileSizeLimit' : '20MB'
fileTypeDesc    选择的文件的描述。这个字符串出现在浏览文件对话框中文件类型下拉框处。默认：All Files
fileTypeExts    允许上传的文件类型。格式：'fileTypeExts' : '*.gif; *.jpg; *.png'
formData    附带值，需要通过get or post传递的额外数据，需要结合onUploadStart事件一起使用
height        “浏览按钮”高度px
itemTemplate    <itemTemplate>节点表示显示的内容。这些内容中也可以包含绑定到控件DataSource属性中元素集合的数据。
method        上传方式。默认：post
multi        选择文件时是否可以【选择多个】。默认：可以true
overrideEvents    不执行默认的onSelect事件
preventCaching    随机缓存值 默认true ，可选true和false.如果选true,那么在上传时会加入一个随机数来使每次的URL都不同,以防止缓存.但是可能与正常URL产生冲突
progressData    进度条上显示的进度:有百分比percentage和速度speed。默认百分比
queueID        给“进度条”加背景css的ID样式。文件选择后的容器ID
queueSizeLimit    允许多文件上传的数量。默认：999
removeCompleted    上传完成后队列是否自动消失。默认：true
removeTimeout    上传完成后队列多长时间后消失。默认 3秒    需要：'removeCompleted' : true,时使用
requeueErrors    队列上传出错，是否继续回滚队列，即反复尝试上传。默认：false
successTimeout    上传超时时间。文件上传完成后,等待服务器返回信息的时间(秒).超过时间没有返回的话,插件认为返回了成功。 默认：30秒
swf        swf文件的路径,本文件是插件自带的,不可用其它的代替.本参数不可省略
uploader    上传处理程序URL，本参数不可省略
uploadLimit    限制总上传文件数,默认是999。指同一时间，如果关闭浏览器后重新打开又可上传。
width        “浏览按钮”宽度px

**Events 事件**
onCancel    当取消一个上传队列中的文件时触发,删除时触发 
onClearQueue    清除队列。当'cancel'方法带着*参数时,也就是说一次全部取消的时候触发.queueItemCount是被取消的文件个数（另外的按钮）
onDestroy    取消所有的上传队列（另外的按钮）
onDialogClose    当选择文件对话框关闭时触发,不论是点的'确定'还是'取消'都会触发.如果本事件被添加进了'overrideEvents'参数中,那么如果在选择文件时产生了错误,不会有错误提示框弹出
onDialogOpen    当选择文件框被打开时触发,没有传过来的参数
onDisable    关闭上传
onEnable    开启上传
onFallback    检测FLASH失败调用
onInit        每次初始化一个队列时触发
onQueueComplete    当队列中的所有文件上传完成时触发
onSelect    当文件从浏览框被添加到队列中时触发
onSelectError    选择文件出错时触发
onSWFReady    flash准备好时触发
onUploadComplete当一个文件上传完成时触发
onUploadError    当文件上传完成但是返回错误时触发
onUploadProgress上传汇总
onUploadStart    一个文件上传之间触发
onUploadSuccess    每个上传完成并成功的文件都会触发本事件

**Methods 方法**
cancel        取消一个上传队列
destroy        取消所有上传队列
disable        禁止点击“浏览按钮”
settings    返回或修改一个 uploadify实例的settings值
stop        停止当前的上传并重新添加到队列中去
upload        上传指定的文件或者所有队列中的文件
