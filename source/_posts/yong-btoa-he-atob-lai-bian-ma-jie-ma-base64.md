---
title: '用 btoa 和 atob 来编码解码Base64'
date: 2019-12-13 10:50:33
tags: []
published: true
hideInList: false
feature: 
---
btoa和atob是window对象的两个函数，其中btoa是binary to ascii，用于将binary的数据用ascii码表示，即Base64的编码过程，而atob则是ascii to binary，用于将ascii码解析成binary数据，看一个例子：
```js
// Define the string
var string = 'Hello World!';

// Encode the String
var encodedString = btoa(string);
console.log(encodedString); // Outputs: "SGVsbG8gV29ybGQh"

// Decode the String
var decodedString = atob(encodedString);
console.log(decodedString); // Outputs: "Hello World!"
```
atob和btoa不能编码Unicode字符：
```js
var string = "Hello, 中国！";
window.btoa(string);
```
那如何用这种方式支持汉字呢？这里我们可以先将带有非Latin1字符的串先用encodeURIComponent编码：
```
var string = "Hello, 中国！";
//"SGVsbG8lMkMlMjAlRTQlQjglQUQlRTUlOUIlQkQlRUYlQkMlODE="
var encodedString = btoa(encodeURIComponent(string));
var decodedString = decodeURIComponent(atob(encodedString));
console.log(decodedString); //"Hello, 中国！"
```
https://my.oschina.net/itblog/blog/1613977
https://scotch.io/tutorials/how-to-encode-and-decode-strings-with-base64-in-javascript