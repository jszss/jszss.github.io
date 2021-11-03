---
title: 'call,apply和bind区别'
date: 2019-12-13 14:44:31
tags: []
published: true
hideInList: false
feature: 
---
### 三个函数的作用都是将函数绑定到上下文中，用来改变函数中this的指向；三者的不同点在于语法的不同。
```js
fun.call(thisArg[, arg1[, arg2[, ...]]])
fun.apply(thisArg, [argsArray])
```
所以apply和call的区别是call方法接受的是若干个参数列表，而apply接收的是一个包含多个参数的数组。
而bind()方法创建一个新的函数, 当被调用时，将其this关键字设置为提供的值，在调用新函数时，在任何提供之前提供一个给定的参数序列。
```js
var bindFn = fun.bind(thisArg[, arg1[, arg2[, ...]]])
bindFn()
```
## Demos
```js
var name = 'window';
var sayName = function (param) {
    console.log('my name is:' + this.name + ',my param is ' + param)
};
//my name is:window,my param is window param
sayName('window param')

var callObj = {
    name: 'call'
};
//my name is:call,my param is call param
sayName.call(callObj, 'call param');


var applyObj = {
    name: 'apply'
};
//my name is:apply,my param is apply param
sayName.apply(applyObj, ['apply param']);

var bindObj = {
    name: 'bind'
}
var bindFn = sayName.bind(bindObj, 'bind param')
//my name is:bind,my param is bind param
bindFn();

```