---
title: 'vue3 ts 类型扩展'
date: 2021-05-31 10:37:51
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
declare module '@vue/runtime-core' {
  interface ComponentCustomProperties {
    $test: number
  }
}
```