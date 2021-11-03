---
title: '$options.data 重置data'
date: 2021-06-22 09:44:42
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
      console.log('🚀  this', this)
      Object.assign(this.$data, this.$options.data.call(this))
      console.log('🚀  this', this)
```