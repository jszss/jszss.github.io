---
title: 'Vue 函数式组件'
date: 2019-06-03 10:35:06
tags: [Vue]
published: true
hideInList: false
feature: 
---
` tip 函数式组件, 无状态，无法实例化，内部没有任何生命周期处理方法，非常轻量，因而渲染性能高，特别适合用来只依赖外部数据传递而变化的组件。`

> 在template标签里面标明functional
> 只接受props值
> 不需要script标签

```html
<!-- App.vue -->
<template>
  <div>
    <UserList :users="users" :click-handler="clickHandler.bind(this)"></UserList>
  </div>
</template>
 
<script>
import UserList from "./UserList";
 
export default {
  name: "App",
  data: () => {
    users: ['james', 'ian']
  }
  components: { UserList },
  methods: {
    clickHandler(name){
      console.log(`clicked: ${name}`);
    }    
  }
};
</script>
```
```
// UserList.vue
<template functional>
  <div>
    <p v-for="(name, idx) in props.users" @click="props.clickHandler(name)" :key="idx">
      {{ name }}
    </p>
  </div>
</template>

```