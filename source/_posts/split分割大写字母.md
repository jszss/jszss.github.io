---
title: "split 分割大写字母"
date: 2021-06-04 11:12:54
tags: [split, 正则]
published: true
hideInList: false
feature:
isTop: false
---

## 大写字母分割字符串

```js
"taxAdmin".split(/(?=[A-Z])/); // ["tax", "Admin"]
```
