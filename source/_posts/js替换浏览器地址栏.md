---
title: js替换浏览器地址栏
date: 2021-10-18 11:40:28
tags: BOM
---

```js
function locationReplace(url) {
  if (history.replaceState) {
    history.replaceState(null, document.title, url);
    history.go(0);
  } else {
    location.replace(url);
  }
}
```