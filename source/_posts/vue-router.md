---
title: 'vue-router'
date: 2019-10-31 10:35:20
tags: [vue-router]
published: true
hideInList: false
feature: 
---
## 将"激活时的CSS类名"应用在外层元素

有时候我们要让 "激活时的CSS类名" 应用在外层元素，而不是 `<a>` 标签本身，那么可以用 `<router-link> `渲染外层元素，包裹着内层的原生`<a>` 标签：
```
<router-link tag="li" to="/foo"> 
  <a>/foo</a>
</router-link>
```
在这种情况下，`<a> `将作为真实的链接（它会获得正确的 href 的），而 "激活时的CSS类名" 则设置到外层的 `<li>`。 

原文链接：https://blog.csdn.net/qq_35624642/article/details/78910194