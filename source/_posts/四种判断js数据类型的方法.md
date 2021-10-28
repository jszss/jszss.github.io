---
title: 四种判断js数据类型的方法
author: zss
date: 2021-10-28 21:04:32
tags:
---

<!-- more -->

```js
typeof
instanceof
constructor
Object.prototype.toString.call()

```

```js
function Person() {}
var Tom = new Person();
// undefined和null没有constructor属性
console.log(
  Tom.constructor == Person,
  num.constructor == Number,
  str.constructor == String,
  obj.constructor == Boolean,
  arr.constructor == Array,
  json.constructor == Object,
  func.constructor == Function,
  date.constructor == Date,
  reg.constructor == RegExp,
  error.constructor == Error
);
// 所有结果均为true
```

1. undefined 和 null 没有 constructor 属性，所以判断时代码可能会报错--这很致命，会导致代码运行不下去，所以只有在确定待判断的值不是 undefined 和 null 才能使用
2. 由于 constructor 属性是可以变更的，也会导致检测出的结果不正确
