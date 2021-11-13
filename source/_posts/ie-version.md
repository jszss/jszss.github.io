---
title: 'javascript判断IE浏览器版本和Edge代码'
date: 2019-10-10 16:54:41
tags: []
published: true
hideInList: false
feature: 
---
[javascript判断IE浏览器版本和Edge代码](https://www.xinran001.com/frontend/284.html)

## IE不标准的地方，unshift方法会返回新数组的长度，但IE6与IE7则返回undefined。
```js
console.log([1].unshift(8))
//IE6、IE7下返回undefined，其它都是返回2
```
## 判断是否为IE8及以下版本
```js
if (!+[1,]) {
    alert('<=8');
}
```
## 判断是否为IE9及以下版本
```js
//方法一：
if (!('placeholder' in document.createElement('input'))) {
        alert('<=9');
}
//（IE9及以下版本不支持placeholder，代码较少） 

//方法二： 
if (navigator.appName == "Microsoft Internet Explorer" && parseInt(navigator.appVersion.split(";")[1].replace(/[ ]/g, "").replace("MSIE", "")) < 10) {
        alert('<=9');
    }
```
## 判断是否为 IE10 及以下版本
```js
if (!!document.all) {
    alert('<=10');
}
```
## 判断是否为 IE 浏览器
```js
if(!!window.ActiveXObject || "ActiveXObject" in window){
    alert('Is IE');
}
```
## 判断是否为 Edge 浏览器
```js
if (navigator.userAgent.indexOf("Edge") > -1) {
        alert('Is Edge');
}
```
## 判断是否为指定版本IE，比如判断是否为IE8或者IE10
```js
if (
    navigator.appName == "Microsoft Internet Explorer" 
    && 
    navigator.appVersion.split(";")[1].replace(/[ ]/g, "")
    in 
    {
    'MSIE8.0': '',
    'MSIE10.0': ''
    }
) {
    alert(true)
}
```