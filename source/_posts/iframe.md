---
title: 'iframe'
date: 2020-01-01 11:04:02
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## iframe常用属性:
```
1. frameborder:是否显示边框，1(yes),0(no)
2. height:框架作为一个普通元素的高度，建议在使用css设置。
3. width:框架作为一个普通元素的宽度，建议使用css设置。
4. name:框架的名称，window.frames[name]时专用的属性。
5. scrolling:框架的是否滚动。yes,no,auto。
6. src：内框架的地址，可以使页面地址，也可以是图片的地址。
7. srcdoc , 用来替代原来HTML body里面的内容。但是IE不支持, 不过也没什么卵用
8. sandbox: 对iframe进行一些列限制，IE10+支持
```
---
## 获取iframe里的内容
```
 var iframe = document.getElementById("iframe1");
 var iwindow = iframe.contentWindow;
 var idoc = iwindow.document;
        console.log("window",iwindow);//获取iframe的window对象
        console.log("document",idoc);  //获取iframe的document
        console.log("html",idoc.documentElement);//获取iframe的html
        console.log("head",idoc.head);  //获取head
        console.log("body",idoc.body);  //获取body
```
```
<iframe src ="/index.html" id="ifr1" name="ifr1" scrolling="yes">
  <p>Your browser does not support iframes.</p>
</iframe>
<script type="text/javascript">
	console.log(window.frames['ifr1'].window);
console.dir(document.getElementById("ifr1").contentWindow);
</script>
```
## 在iframe中获取父级内容
```
window.parent 获取上一级的window对象，如果还是iframe则是该iframe的window对象
window.top 获取最顶级容器的window对象，即，就是你打开页面的文档
window.self 返回自身window的引用。可以理解 window===window.self(脑残)
```