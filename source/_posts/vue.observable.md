---
title: 'Vue.observable'
date: 2019-09-16 10:27:50
tags: [Vue]
published: true
hideInList: false
feature: 
---
## 不使用Vuex创建Store(Vue.observable)
`Vue.observable({})`返回的对象可以直接用于渲染函数和计算属性内，并且会在发生改变时触发相应的更新。也可以作为最小化的跨组件状态存储器，用于简单的场景：
```
const state = Vue.observable({ count: 0 })

const Demo = {
  render(h) {
    return h('button', {
      on: { click: () => { state.count++ }}
    }, `count is: ${state.count}`)
  }
}
```
我们可以利用这个API来应对一些简单的跨组件数据状态共享的情况.
```
// miniStore.js

import Vue from "vue";
 
export const miniStore = Vue.observable({ count: 0 });
 
export const actions = {
  setCount(count) {
    miniStore.count = count;
  }
}

export const getters = {
  count: () => miniStore.count
}
```
```
// Demo.vue
<template>
  <div>
    <p>count:{{count}}</p>
    <button @click="add"> +1 </button>
    <button @click="sub"> -1 </button>
  </div>
</template>
 
<script>
import { actions, getters } from "./store";
export default {
  name: "App",
  computed: {
    count() {
      return getters.count;
    }
  },
  methods: {
    add: actions.setCount(this.count+1),
    sub: actions.setCount(this.count-1)
  }
};
</script>
```