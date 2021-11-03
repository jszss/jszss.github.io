---
title: 'Vue 自定义组件全局引用'
date: 2019-09-29 10:03:40
tags: [Vue cli 配置]
published: true
hideInList: false
feature: 
---
## 局部组件引用方式
```js
import A from '@/component/A'
export default {
    data () {},
    components: { A }
}
```
## 全局组件引用方式1
```js
// index.js 文件
import A from '@/component/A'
A.install = function (Vue) {
  Vue.component(A.name, A)
}
export {
    A
}
// main.js 文件
import { A } from './components/index'
Vue.use(A)

```
## 全局组件引用方式2(推荐?)
```js
// index.js 文件
import A from '@/component/global/A'
A.install = function (Vue) {
  Vue.component(A.name, A)
}
function InstallAll(Vue) {
    Vue.use(A)
}
export {
    A,
    InstallAll
}
// main.js 文件
import { InstallAll } from './components/index'
InstallAll(Vue)
```
## 全局组件引用方式3(webpack?)
[【官方】基础组件的自动化全局注册](https://cn.vuejs.org/v2/guide/components-registration.html#%E5%9F%BA%E7%A1%80%E7%BB%84%E4%BB%B6%E7%9A%84%E8%87%AA%E5%8A%A8%E5%8C%96%E5%85%A8%E5%B1%80%E6%B3%A8%E5%86%8C)
[官方例子](https://github.com/chrisvfritz/vue-enterprise-boilerplate/blob/master/src/components/_globals.js)
> require.context('.', false, /\.vue$/)加载当前目录所有.vue结尾的文件自动遍历注册，再引入到main.JS