---
title: "正则获取url参数"
date: 2021-09-10 11:46:00
tags: [utils, 正则]
published: true
hideInList: false
feature:
top: true
---

replace 正则获取 url 请求参数

```js
function query(url) {
  let reg = /([^=?&]+)=([^=?&#]+)/g,
    obj = {};
  if (!url) return obj;
  url.replace(reg, function () {
    obj[arguments[1]] = arguments[2];
  });
  return obj;
}
```

<!-- more -->

```js
/**
 * replace 正则获取 url 请求参数
 */
function query(url) {
  let reg = /([^=?&]+)=([^=?&#]+)/g,
    obj = {};
  if (!url) return obj;
  url.replace(reg, function () {
    obj[arguments[1]] = arguments[2];
  });
  return obj;
}

query(location.href);
query("http://www.baidu.com/?name=zss&id=2");
// {name: 'zss', id: '2'}
```
