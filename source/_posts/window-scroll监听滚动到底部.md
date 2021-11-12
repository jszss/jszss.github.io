---
title: window.scroll监听滚动到底部
author: zss
date: 2021-11-12 15:20:10
tags:
---

```js
/**
 * 监听滚动到底部
 * @param {object} options 传参对象
 * @param {number} options.distance 距离底部多少像素触发（px）
 * @param {boolean} options.once 是否为一次性（防止重复用）
 * @param {() => void} options.callback 到达底部回调函数
 */
function onScrollToBottom(options) {
  const { distance = 0, once = false, callback = null } = options;
  const doc = document;
  /** 滚动事件 */
  function onScroll() {
    /** 滚动的高度 */
    let scrollTop =
      doc.documentElement.scrollTop === 0
        ? doc.body.scrollTop
        : doc.documentElement.scrollTop;
    /** 滚动条高度 */
    let scrollHeight =
      doc.documentElement.scrollTop === 0
        ? doc.body.scrollHeight
        : doc.documentElement.scrollHeight;
    if (scrollHeight - scrollTop - distance <= window.innerHeight) {
      if (typeof callback === "function") callback();
      if (once) window.removeEventListener("scroll", onScroll);
    }
  }
  window.addEventListener("scroll", onScroll);
  // 必要时先执行一次
  // onScroll();
}
```
