---
layout: post
title: uploadify上传注意
date: 2014-10-21 23:49
categories: [java, E-learning]
tags: [uploadify]
---
上传成功后要返回一个文件地址回来。
'onUploadSuccess':function(file, data, response){//上传成功后获得回调函数,这里为了取得文件上传成功后的保存路径
            adjunctPath+=data;
            $("#dirPath").val(adjunctPath);
            //onUploadSuccess();
            if(canSubmit){
                document.dataForm.submit();
            }
        },
成功后再提交。
不然会出现问题。
因为提交的时候要将path交给后台，但是如果在整个上传动作还没结束的时候就提交了表单，则会造成path为空。
