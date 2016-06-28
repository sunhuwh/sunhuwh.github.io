---
layout: post
title: iframe+dialog实现对话框为iframe
date: 2015-06-25 00:57
categories: [jQuery]
tags: [iframe, dialog]
---
举例：


```javascript
function preparePreview() {
	var explorer = $("#explorer");
	if(explorer.length==0) {
		$("body").append("<div id=\"explorer\" style=\"display:none;\"><iframe name=\"selectorFrame\" id=\"selectorFrame\" width=\"100%\" height=\"100%\" frameborder=\"0\" scrolling=\"auto\" src=\"\"></iframe></div>");
	}
}

function preview(id) {
	var url = "";
	var dialog_width, dialog_height, screen_width = window.screen.width;
	if(screen_width < 1440) {
		dialog_width = 800;
		dialog_height = 650;
	} else {
		dialog_width = 1280;
		dialog_height = 720;
	}
	preparePreview();
	var explorer = $("#explorer");
	$("#explorer iframe").attr("src", url);
	explorer.dialog({
		modal: true,
		height: dialog_height,
		width: dialog_width,
		beforeClose: function(event, ui) {
			window.frames["selectorFrame"].document.body.innerHTML="";
		}
	});
}
```

具体来讲dialog的参数：
autoOpen ，这个属性为true的时候dialog被调用的时候自动打开dialog窗口。当属性为false的时候，一开始隐藏窗口，知道.dialog("open")的时候才弹出dialog窗口。默认为：true。

buttons 显示一个按钮，并写上按钮的文本，设置按钮点击函数。默认为{}，没有按钮。
$('.selector').dialog({ buttons: { "Ok": function() { $(this).dialog("close"); } } });

draggable、resizable : draggable是否可以使用标题头进行拖动，默认为true，可以拖动;resizable是否可以改变dialog的大小，默认为true，可以改变大小。

width、height ，dialog的宽和高，默认为auto，自动。

maxWidth、maxHeight、minWidth、minHeight ，dialog可改变的最大宽度、最大高度、最小宽度、最小高度。maxWidth、maxHeight的默认为false，为不限。minWidth、 minHeight的默认为150。要使用这些属性需要ui.resizable.js 的支持。

hide、show ，当dialog关闭和打开时候的效果。默认为null，无效果

modal,是否使用模式窗口，模式窗口打开后，页面其他元素将不能点击，直到关闭模式窗口。默认为false不是模式窗口。

title，dialog的标题文字，默认为空。

position ，dialog的显示位置：可以是'center', 'left', 'right', 'top', 'bottom',也可以是top和left的偏移量也可以是一个字符串数组例如['right','top']。

 stack 默认值为true，当dialog获得焦点是，dialog将在最上面。

事件：
beforeclose类型dialogbeforeclose ， 当dialog尝试关闭的时候此事件将被触发，如果返回false，那么关闭将被阻止。

 close类型：dialogclose ，当dialog被关闭后触发此事件。

open 类型：dialogopen ，当dialog打开时触发。

focus 类型：dialogfocus ，当dialog获得焦点时触发。

dragStart 类型：dragStart，当dialog拖动开始时触发。

drag 类型：drag ，当dialog被拖动时触发。

dragStop 类型：dragStop ，当dialog拖动完成时触发。

resizeStart 类型：resizeStart ，当dialog开始改变窗体大小时触发。

resize 类型：resize，当 dialog被改变大小时触发。

resizeStop 类型：resizeStop，当改变完大小时触发。


方法
destroy ， 例：.dialog( 'destroy' ) 

disable，dialog不可用，例：.dialog('disable');

enable,dialog可用

close，open，关闭、打开dialog

option ，设置和获取dialog属性，例如：.dialog( 'option' , optionName , [value]) ，如果没有value，将是获取。

isOpen ，如果dialog打开则返回true，例如：.dialog('isOpen')

moveToTop ,将dialog移到最上层，例如：.dialog( 'moveToTop' )
