---
title: 'background-clip'
date: 2019-09-10 11:53:02
tags: [CSS3,CSS]
published: true
hideInList: false
feature: 
---
``` html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>文本颜色渐变</title>
  <style>
    .text {
      font-size: 50px;
      /* background-image: -webkit-gradient(linear, left 0, right 0, from(rgb(4, 94, 170)), to(rgb(1, 152, 216))); */
      /* background: linear-gradient(to top right, #CDDC39 0%, #8BC34A 25%, #FFEB3B 100%); */
      background-image: url(http://ww.yiweb.com.cn/jinghua/dist/images/ServiceProject-pic01.jpg);
      -webkit-background-clip: text;
      /*必需加前缀 -webkit- 才支持这个text值 */
      -webkit-text-fill-color: transparent;
      /*text-fill-color会覆盖color所定义的字体颜色： */
    }
  </style>
</head>

<body>  
  <h1 class="text">文本颜色渐变</h1>
</body>

</html>
```