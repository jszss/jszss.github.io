---
title: 'vw&rem实现移动端布局'
date: 2019-09-10 11:51:26
tags: []
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
  <title>vw&rem实现移动端布局</title>
  <style>
    *{ margin: 0;padding: 0 }
    
    /* 核心代码 */
    html{ font-size:  13.333333vw; }
    body{ max-width: 750px;min-width: 320px; margin: 0 auto }
    @media screen and ( min-width:750px ){ html{ font-size: 100px; } }
    /* 核心代码 */
    
    #app{ height: 100vh;background-color: #ccc;font-size: 0px; }
    #app .item{font-size:.3rem; display: inline-block; width: 1.80rem; height: 1.80rem;line-height: 1.80rem; text-align: center; background-color: #fff; margin-right: 0.1rem; }
    #app .item:last-child{  margin-right: 0; }
  </style>
</head>
<body>
    <div id="app">
      <div class="item"> 1 </div>
      <div class="item"> 2 </div>
      <div class="item"> 3 </div>
      <div class="item"> 4 </div>
    </div>
</body>
</html>
```