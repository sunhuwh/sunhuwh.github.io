---
layout: post
title: javascript 将HTML转为 word，pdf
date: 2014-08-23 23:58
categories: [javascript, E-learning]
tags: []
---

```javascript
/**
 *  wsf html转换工具
 */

var filePath = "d:";

function exportHtml() {
    if (filePath != null) {
        var file;
        try {
            var fso = new ActiveXObject("Scripting.FileSystemObject");
            file = fso.createtextfile(filePath + "/测试导出.html", true); // 创建文件
            file.WriteLine(content.innerHTML); // 写入数据
            alert("导出成功");
        } catch(e) {
            alert("导出失败");
        } finally {
            if (file != null) file.close(); // 关闭连接
        }
    }
}

function exportWord() {
    if (filePath != null) {
        try {
            var word = new ActiveXObject("Word.Application");
            var doc = word.Documents.Add("", 0, 1);
            var range = doc.Range(0, 1);
            var sel = document.body.createTextRange();
            try {
                sel.moveToElementText(content);
            } catch(notE) {
                alert("导出数据失败，没有数据可以导出。");
                window.close();
                return;
            }
            sel.select();
            sel.execCommand("Copy");
            range.Paste();
            // word.Application.Visible = true;// 控制word窗口是否显示
            doc.saveAs(filePath + "/导出测试.doc"); // 保存
            alert("导出成功");
        } catch(e) {
            alert("导出数据失败，需要在客户机器安装Microsoft Office Word(不限版本)，将当前站点加入信任站点，允许在IE中运行ActiveX控件。");
        } finally {
            try {
                word.quit()
            } catch(ex) {}
        }
    }
}

function exportPdf() {
    if (filePath != null) {
        try {
            var word = new ActiveXObject("Word.Application");
            var doc = word.Documents.Add("", 0, 1);
            var range = doc.Range(0, 1);
            var sel = document.body.createTextRange();
            try {
                sel.moveToElementText(content);
            } catch(notE) {
                alert("导出数据失败，没有数据可以导出。");
                window.close();
                return;
            }
            sel.select();
            sel.execCommand("Copy");
            range.Paste();
            // word.Application.Visible = true;// 控制word窗口是否显示
            doc.saveAs(filePath + "/导出测试.pdf", 17); // 保存为pdf格式
            alert("导出成功");
        } catch(e) {
            alert("导出数据失败，需要在客户机器安装Microsoft Office Word 2007以上版本，将当前站点加入信任站点，允许在IE中运行ActiveX控件。");
        } finally {
            try {
                word.quit()
            } catch(ex) {}
        }
    }
}
```

