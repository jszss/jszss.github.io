---
title: Object.seal 创建受控对象
author: zss
date: 2021-10-27 21:17:31
tags: [Object.seal]
---

> `Object.seal()` 方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变，`Object.freeze` 是啥都不能做，`Object.seal()` 可以改变属性的值。

<!-- more -->

```js
const controlledObject = {
  name: "前端小智",
};
Object.seal(controlledObject);
controlledObject.name = "王大冶";
controlledObject.hero = "英雄";

console.log(controlledObject); // {name: "王大冶"}
```
