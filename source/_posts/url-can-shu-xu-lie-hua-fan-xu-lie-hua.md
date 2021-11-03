---
title: 'url参数 序列化 反序列化'
date: 2020-07-21 10:44:21
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## url参数反序列化
一般会通过location.search拿到路由传递的参数，并进行反序列化得到对象
```js
function parseUrlSearch() {
  const search = '?age=25&name=TYJ'
  return search.replace(/(^\?)|(&$)/g, "").split("&").reduce((t, v) => {
    const [key, val] = v.split("=");
    t[key] = decodeURIComponent(val);
    return t;
  }, {});
}

console.log(parseUrlSearch()); // { age: "25", name: "TYJ" }

```
## url参数序列化
将对象序列化成url参数传递
```js
function stringifyUrl(search = {}) {
  return Object.entries(search).reduce(
    (t, v) => `${t}${v[0]}=${encodeURIComponent(v[1])}&`,
    Object.keys(search).length ? "?" : ""
  ).replace(/&$/, "");
}

console.log(stringifyUrl({ age: 27, name: "YZW" })); // "?age=27&name=YZW"

```