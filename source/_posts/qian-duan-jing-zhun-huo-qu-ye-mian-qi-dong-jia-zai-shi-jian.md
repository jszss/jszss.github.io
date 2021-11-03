---
title: '前端(performance)精准获取页面启动加载时间'
date: 2021-05-08 18:41:04
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
var t = performance.timing
// 页面加载的耗时
var pageloadtime = t.loadEventStart - t.navigationStart;
// 域名解析的耗时
var dns = t.domainLookupEnd - t.domainLookupStart;
// TCP连接的耗时
var tcp = t.connectEnd - t.connectStart;
// 读取页面第一个字节之前的耗时
var ttfb = t.responseStart - t.navigationStart;
```