---
title: es5可选链
author: zss
date: 2022-01-02 16:16:41
tags:
---

```js
function safeGet(obj, path) {
  var keys = path.split(",");
  for (key of keys) {
    if (obj) {
      obj = obj[key];
    }
  }
  return obj;
}
```
