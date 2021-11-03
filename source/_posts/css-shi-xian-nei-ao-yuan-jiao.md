---
title: 'css 实现内凹圆角'
date: 2020-01-07 13:41:29
tags: [CSS3]
published: true
hideInList: false
feature: 
isTop: false
---

     我们经常会去实现那种圆角的按钮，图片等等，但是想要实现这种内凹的圆角形状的块状还是比较复杂，我先讲讲思路：
-  第一，需要一个大块进行包裹，需要设置宽度和高度等；
-  第二，需要四个小块，来使用圆角的属性border-radius，进行不同方向的圆角设置；
-  第三，为这些块加上border属性。
![](https://img-blog.csdn.net/20170803151329578?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxNDIzMDE5OA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
```html
<html>
<head>
<meta charset="utf-8"/>
<title>内凹圆角</title>
<style type="text/css">
    .cro {
        width: 100px;
        height: 100px;
        border: 1px solid #58C4E6;
        position: relative;
    }
 
    .cro_left_top, .cro_right_top, .cro_left_bottom, .cro_right_bottom {
        position: absolute;
        width: 20px;
        height: 20px;
        border: 1px solid #fff;
        z-index: 1;
        background: #fff;
    }
 
    .cro_left_top {
        top: -1px;
        left: -1px;
        border-radius: 0 0 20px 0;
        border-bottom: 1px solid #58C4E6;
        border-right: 1px solid #58C4E6;
    }
 
    .cro_right_top {
        top: -1px;
        right: -1px;
        border-radius: 0 0 0 20px;
        border-bottom: 1px solid #58C4E6;
        border-left: 1px solid #58C4E6;
    }
 
    .cro_left_bottom {
        left: -1px;
        bottom: -1px;
        border-radius: 0 20px 0 0;
        border-top: 1px solid #58C4E6;
        border-right: 1px solid #58C4E6;
    }
 
    .cro_right_bottom {
        right: -1px;
        bottom: -1px;
        border-radius: 20px 0 0 0;
        border-top: 1px solid #58C4E6;
        border-left: 1px solid #58C4E6;
    }
</style>
</head>
<body>
<div class="cro">
    <div class="cro_left_top"></div>
    <div class="cro_right_top"></div>
    <div class="cro_left_bottom"></div>
    <div class="cro_right_bottom"></div>
</div>
</body>
</html>
```