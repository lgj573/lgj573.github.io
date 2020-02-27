---
layout: post
title: tinymce 重新初始化错误
category: 前端
tags: [tinymce]
description: tinymce 重新初始化错误
---
tinymce 为4.9.8
## tinymce 初始化没有问题
```html
<textarea id="messageEditor" name="detail" class="tinymce"></textarea>
```
```
tinymce.init({
        selector: 'textarea.tinymce', 
        menubar: false,
        statusbar: false 
    });
```

现在这部分要重新加载，tinymce重新初始化时没起作用。如果把id删掉是可以重新初始化的，但是不能把内容保存到textarea。
我是用tinyMCE.triggerSave();来同步到textarea的。
删除后初始化也不行。
```
tinymce.remove()
```
后来发现是textarea的id问题。设置一个不一样的id就可以了。