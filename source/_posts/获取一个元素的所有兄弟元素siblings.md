---
title: 获取一个元素的所有兄弟元素siblings
author: zss
date: 2021-10-28 21:17:26
tags:
---

<!-- more -->

```js
const siblings = (ele) =>
  .slice.call(ele.parentNode.children).filter((child) => child !== ele);

```
