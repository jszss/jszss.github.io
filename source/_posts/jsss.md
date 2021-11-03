---
title: 'js 基础知识'
date: 2019-01-09 10:04:34
tags: []
published: true
hideInList: false
feature: 
---
## JS中如何将页面重定向到另一个页面？
* 使用 location.href：`window.location.href ="https://www.baidu.com/"`
* 使用  location.replace：`window.location.replace(" https://www.baidu.com/")`
## JS中的`Array.splice()`和`Array.slice()`方法有什么区别
```
var arr=[0,1,2,3,4,5,6,7,8,9];//设置一个数组
console.log(arr.slice(2,7));//2,3,4,5,6
console.log(arr.splice(2,7));//2,3,4,5,6,7,8
//由此我们简单推测数量两个函数参数的意义,
slice(start,end)第一个参数表示开始位置,第二个表示截取到的位置(不包含该位置)
splice(start,length)第一个参数开始位置,第二个参数截取长度
```
```
var x=y=[0,1,2,3,4,5,6,7,8,9]
console.log(x.slice(2,5));//2,3,4
console.log(x);[0,1,2,3,4,5,6,7,8,9]原数组并未改变
//接下来用同样方式测试splice
console.log(y.splice(2,5));//2,3,4,5,6
console.log(y);//[0,1,7,8,9]显示原数组中的数值被剔除掉了
```
函数参数上slice和splice第一个参数都是截取开始位置,slice第二个参数是截取的结束位置(不包含),而splice第二个参数(表示这个从开始位置截取的长度),slice不会对原数组产生变化,而splice会直接剔除原数组中的截取数据!
## 解释JS中的高阶函数？
高阶函数是JS函数式编程的最佳特性。它是以函数为参数并返回函数作为结果的函数。一些内置的高阶函数是map、filter、reduce 等等。
##  substr() 和 substring() 区别
substr()  函数的形式为substr(startIndex,length)。 它从startIndex返回子字符串并返回'length'个字符数。
```
var s = "hello";
( s.substr(1,4) == "ello" ) // true
``` 
substring() 函数的形式为substring(startIndex,endIndex)。 它返回从startIndex到endIndex - 1的子字符串。
```
var s = "hello";
( s.substring(1,4) == "ell" ) // true 
```