---
title: '自定义指令directive'
date: 2020-05-12 20:21:32
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
https://juejin.im/post/5eb7fc626fb9a0436a7c6af1
```js
import Vue from 'vue'

const preventReClick = Vue.directive('preventReClick', {
  inserted: function(el, binding) {
    el.addEventListener('click', () => {
      if (!el.disabled) {
        el.disabled = true
        setTimeout(() => {
          el.disabled = false
        }, binding.value || 3000) // 传入绑定值就使用，默认3000毫秒内不可重复触发
      }
    })
  }
})

export { preventReClick }

```
```js
import preventReClick from './plugins/directives.js' //防多次点击，重复提交
```
```js
// 指定延迟1000ms
<el-button  size="small" type="primary" @click="handleSave()" v-preventReClick="1000">保 存</el-button>

// 默认延迟时间3000
<el-button  size="small" type="primary" @click="handleSave()" v-preventReClick>保 存</el-button>

```