---
title: 'vue组件 props、data 初始化的执行顺序'
date: 2020-11-16 13:33:17
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
beforeCreate  ->inject -> Props ->  Methods ->  Data -> Computed -> Watch ->provide-> created
```
```js
      console.log('🚀  this', this)
      Object.assign(this.$data, this.$options.data.call(this))
      console.log('🚀  this', this)
```