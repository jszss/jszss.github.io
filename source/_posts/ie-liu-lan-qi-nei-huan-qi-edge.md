---
title: 'ie浏览器内唤起edge'
date: 2021-04-28 14:23:41
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
if (isWin10IE) {
    window.location.href = `microsoft-edge:${document.URL}`;
}
```