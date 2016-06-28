---
layout: post
title: IE8及以下版本HTML5 placeholder解决方案
date: 2013-10-29 20:23
categories: [javascript, HTML]
tags: []
---
placeholder 是HTML5的新屬性，在做input 的預設值還蠻方便的，但無奈IE8以下不支援，因此需要額外做fix。在實際應用中，卻愈到了很多問題：
例如在官網查到的plugin：[http://plugins.jquery.com/project/input-placeholder](http://plugins.jquery.com/project/input-placeholder)，就不支援type="password"的結果。因為僅改變value，對於password的顯示方式
以下是我找到支援度最好地plugin:
DEMO:[http://mathiasbynens.be/demo/placeholder](http://mathiasbynens.be/demo/placeholder)
plugin:[https://github.com/mathiasbynens/Placeholder-jQuery-Plugin](https://github.com/mathiasbynens/Placeholder-jQuery-Plugin)
然而在實做中愈到了一些bug，最後追source code追到plugin本身對於type="password"還有些bug, 一般的情況可能不會遇到，但偏偏就是讓我遇到了，原因在於這一段程式
[sourcecode language="javascript"] if ($input.data('placeholder-password')) { $input.hide().next().show().focus(); } else { $input.val('').removeClass('placeholder'); } [/sourcecode]
當這隻程式在做dom Traversing時，用到了$input.hide().next().show().focus();，而bug就是因為在查找.next()時查找錯誤而造成。因此我將這幾段程式做了一點小修改，簡單解釋如下：
[sourcecode language="javascript"] if ($input.data('placeholder-password')) { //$input.hide().next().show().focus(); //avoiding dom traversing by unsure dom structure $input.hide().data('placeholder-src').show().focus(); } else { $input.val('').removeClass('placeholder');
 } [/sourcecode]
先用.data儲存要替換的input element，將原本用DOM Traversing查出的Element改用.data取回物件。That's all.
另外，我也順手修正了一個小bug
[sourcecode language="javascript"] $replacement = $input.clone().attr({ type: 'text' }); $replacement .removeAttr('id') //we don't need id, it will be confused by selector within id .removeAttr('name') .data('placeholder-password', true) .data('placeholder-src',
 $input) .bind('focus.placeholder', clearPlaceholder); [/sourcecode]
我們也不需要複製id，尤其在做一些表單驗證時，很多人會用id 來榜定做檢查，這時這個element就會取得錯誤。
 
當然，我也commit上去給原作者，不過不曉得他會不會採用就是了。若需要修改後的版本請參考：[Download
 jquery.placeholder.js](http://blog.blackbing.net/wp-content/uploads/2011/01/jquery.placeholder.js.txt)
這讓我想到在開發API時，如何建立自己的sandbox是很重要的。
1. 不管你怎麼處理事情，只要畫面不是你能控制的，永遠不要相信被渲染過後的DOM結構，因此盡可能不要用模糊的DOM Travesing來查找元素。
2. 盡可能不要影響別人的行為，就如同clone Element 之後，你應該要避免複製id 以及name，否則有可能會影想到其他程式。

隨著jQuery越來越強大，plugin的質跟量也開始備受考驗，不重新造輪子，但人家的輪子跑起來就是跑不遠，怎辦？有時候這也是很麻煩的一件事情，上述的例子還只是很單純的事件，若遇到更複雜的專案可就不是簡單trace source code就可以解決的事情。
