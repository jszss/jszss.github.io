---
title: 'css 多行文字和序号顶部对齐'
date: 2021-03-12 18:22:01
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```html
<!doctype html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>css 多行文字和序号顶部对齐</title>
  <style>
    .ul {
      list-style-type: none;
      overflow: hidden;
    }

    /* 加一个padding的目的是因为负的text-indent会把序号挤到标签外，如果父级设置了overflow:hidden;序号就会被隐藏掉，为了防止出现这种情况，所以加上，也为了以后不给自己留坑 */
    .ul li {
      text-indent: -1em;
      padding-left: 1em;
    }
  </style>
</head>

<body>
  方式1
  <hr>
  <ol>
    <li>单行文本</li>
    <li>多行文本多行文本多行文本多行文本多行文本多行文本</li>
  </ol>
  方式2
  <hr>
  <ul style="list-style-type: none;">
    <li style="text-indent:-1.5em; padding-left:1.5em;">1、单行文本</li>
    <li style="text-indent:-1.5em; padding-left:1.5em;">2、多行文本多行文本多行文本多行文本多行文本多行文本</li>
  </ul>
  方式3
  <hr>
  <ul class="ul">
    <li>
      1.大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多
    </li>
    <li>
      2.大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多
    </li>
    <li>
      3.大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多撒多无群的无群二无群大萨达撒多
    </li>
  </ul>
</body>

</html>
```