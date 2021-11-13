---
title: '💰金额千分位格式化函数实现方法'
date: 2019-09-16 09:17:25
tags: []
published: true
hideInList: false
feature: 
---
## 正则表达式
```
String(Number).replace(/(\d)(?=(\d{3})+$)/g, "$1,");
```
## toLocaleString()方法
```
(123456789).toLocaleString('en-US')
```
![](http://zssjs.coding.me/post-images/1568596856868.jpg)
![](http://zssjs.coding.me/post-images/1568596863204.jpg)