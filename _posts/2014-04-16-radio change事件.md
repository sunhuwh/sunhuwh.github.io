---
layout: post
title: radio change事件
date: 2014-04-16 14:57
categories: [jQuery, 简单学习网]
tags: []
---
radio change事件
$('input:radio[name="role"]').change( function()


当一个元素，或者其内部任何一个元素失去焦点的时候会触发这个事件。这跟blur事件区别在于，他可以在父元素上检测子元素失去焦点的情况。
$("#username").focusout(function()

var roles = document.getElementsByName("role");
for....

密码重复验证：
$("#add_form").validate({
        rules : {
            password : {required:true,minlength:6},
            newpassword : {required:true,minlength:6, equalTo: "#password"},
        }
    });

