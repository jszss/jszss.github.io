---
title: 'vuex createLogger'
date: 2021-06-30 14:02:26
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
import Vuex, { createLogger } from 'vuex'
const debug = process.env.NODE_ENV !== 'production'
export default new Vuex.Store({
    // ...
    plugins: debug ? [createLogger()] : []
})
```