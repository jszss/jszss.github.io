---
title: '正则 模糊搜索'
date: 2021-07-11 00:38:35
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
//value就是要搜索的值
let str = ['',...value,''].join('.*'); 
let reg = new RegExp(str);
let newData = data.filter(item => reg.test(item.title));
```