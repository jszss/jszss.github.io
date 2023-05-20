---
title: js 判断数字类型
author: zss
date: 2022-01-21 22:07:48
tags:
---

```js
function isNumber(num){
  return !isNaN(parseFloat(num)) && isFinite(num);
}
isNumber(7); //returns true
isNumber("Hello"); //returns false
```