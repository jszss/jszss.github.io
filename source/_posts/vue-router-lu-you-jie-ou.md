---
title: 'Vue-router 路由解耦'
date: 2020-01-08 14:15:45
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
在组件中使用 route 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。
简单滴说，就是解耦后你便可以在任何地方使用该组件，使得该组件更易于重用和测试，而不再依赖于this.$route来获取参数。[点击了解](https://router.vuejs.org/zh/guide/essentials/passing-props.html)
```json
// router.js
  {
    path: '/lesson/:id',
    props: true,    // 解耦
    component: () => import ('@/views/Lesson.vue') 
  },
```
```
<!-- Lesson.vue -->
<p> 解耦前id: {{ $route.params.id }} </p>
<p> 解耦后id: {{ id }} </p>
```
```js
export default {
  // 解耦必须加props
  props: ['id']  // 接收
}
```