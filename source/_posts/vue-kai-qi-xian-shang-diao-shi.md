---
title: 'Vue 开启线上调试 '
date: 2021-06-30 11:20:56
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
var Vue = $0.__vue__.$root.constructor
while(Vue.super) {Vue = Vue.super}
Vue.config.devtools = true
window.__VUE_DEVTOOLS_GLOBAL_HOOK__.Vue = Vue
```
## $vm
```
重新开启console
```
## 线上线下 查看 vuex数据
```js
$0.__vue__.$store._vm._data
```
## react $r
```
// $0.__react
$r.props.store.getState()
```