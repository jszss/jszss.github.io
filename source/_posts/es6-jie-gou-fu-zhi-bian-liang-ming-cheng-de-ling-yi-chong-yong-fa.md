---
title: 'es6解构赋值变量名称的另一种用法'
date: 2021-05-06 10:48:20
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
const obj = { a:"姓名", b:18, c:"内容" }
const data = {}
obj = { a: data.name, b: data.age, c: data.xx } = obj
console.log(obj) // { a:"姓名", b:18, c:"内容" }
console.log(data) // { name:"姓名", age:18, xx:"内容" }
```