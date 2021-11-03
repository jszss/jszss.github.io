---
title: 'js 正则获取指定字符之后指定字符之前'
date: 2019-12-18 13:38:01
tags: []
published: true
hideInList: false
feature: 
---
## JS正则表达式获取指定字符之后指定字符之前的字符串
```js
var bgImg = "url(\"https://img30.360buyimg.com/sku/jfs/t26203/262/100869187/204098/1d1479e9/5b84b80bNf39db45f.jpg\")";
```
### 方法1
```js
var backgroundImageRegex=/(?<=url\(").+(?="\))/;
var matchResult=bgImg.match(backgroundImageRegex);
if(matchResult.length>0){
  alert(matchResult[0]);
}
```
### 方法2
```js
var backgroundImageRegex=/\((.*)\)/;
var matchResult=bgImg.match(backgroundImageRegex);
```
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions