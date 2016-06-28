---
layout: post
title: kindeditor去掉图片空间
date: 2014-05-28 00:25
categories: [E-learning]
tags: [kindeditor, 图片空间]
---
图片空间使用一般的话只有管理员才可以用的，因为这是操作服务器上的图片。然后使用它，必须得把插件fileManager加上去，并且需要在/kindeditor/jsp中加入：file_manager_json.jsp。至于里面怎么用，还没细细的研究
很像把图片空间删除掉，但是不知道怎么删，这插件东西太多了。又因为图片空间实在网络图片上传的那块区域内，一般而言，很多网站中用户是用使用本地上传，网络上传还是蛮少的。不过多了解一下最好，免得以后又用上。kindeditor网络上传（不带图片空间）：KindEditor.ready(function(K) {editor = K.create('textarea[name="content"]', {resizeType : 1,allowPreviewEmoticons : false,allowImageUpload : false,items : ['fontname', 'fontsize', '|', 'forecolor', 'hilitecolor', 'bold', 'italic', 'underline','removeformat', '|', 'justifyleft', 'justifycenter', 'justifyright', 'insertorderedlist','insertunorderedlist', '|', 'emoticons', 'image', 'link']});});下面是由网络图片和本地上传的，但是没有图片空间var editor = K.editor({        allowFileManager : false,        allowImageManager : true    });