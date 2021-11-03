---
title: 'bind call 快排 数组的扁平化'
date: 2020-10-15 15:01:31
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 数组扁平化
```js
function flatDeep(arr) {
    return arr.reduce((res, cur) => {
        if(Array.isArray(cur)){
            return [...res, ...flatDeep(cur)]
        }else{
            return [...res, cur]
        }
    },[])
}

```
## 手写bind函数
```js
Function.prototype.mybind = function(context, ...args) {
    return (...newArgs) => {
        return this.call(context, ...args, ...newArgs)
    }
}
```
## 实现call
```js
Function.prototype.mycall = function (context, ...args) {
    context = Object(context) || window
    let fn = Symbol(1)
    context[fn] = this
    let result = context[fn](...args)
    delete context[fn]
    return result
}

```
## 实现一个快排
```js
function quickSort(arr){

    if (arr.length <= 1) return arr;
    let index = Math.floor(arr.length / 2)
    let pivot = arr.splice(index, 1)[0],
        left = [],
        right = [];
    for(let i = 0; i < arr.length; i++){
        if(pivot > arr[i]){
            left.push(arr[i])
        }else{
            right.push(arr[i])
        }
    }
    return quickSort(left).concat([pivot],quickSort(right))
}

```
```js
function deepClone(obj, hash = new WeakMap()) {
    if (obj instanceof RegExp) return new RegExp(obj)
    if (obj instanceof Date) return new Date(obj)

    if (obj === null || typeof obj !== 'object') return obj

    if (hash.has(obj)) return obj

    let res = new obj.constructor();
    hash.set(obj, res)
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            res[key] = deepClone(obj[key],hash)
        }
    }
    return res
}

```