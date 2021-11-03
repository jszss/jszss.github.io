---
title: 'resetRouter'
date: 2020-10-15 17:56:01
tags: [vue-router]
published: true
hideInList: false
feature: 
isTop: false
---
```js
//写一个重置路由的方法，切换用户后，或者退出时清除动态加载的路由
export function resetRouter() {
    const newRouter = createRouter()
    router.matcher = newRouter.matcher // 新路由实例matcer，赋值给旧路由实例的matcher，（相当于replaceRouter）
}
```
```
import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)
const createRouter = () => new Router({
 mode: 'history',
 routes: []
})
const router = createRouter()
export function resetRouter () {
 const newRouter = createRouter()
 router.matcher = newRouter.matcher
}
export default router
```
```js
Router.prototype.resetRouter=function resetRouter(routes) {
let newRouter = new Router({
routes: routes
})
this.matcher = newRouter.matcher ;
}

//把自己定义的方法挂载在 router下。 通过传参 给路由赋值。

this.$router.resetRouter(routes);
```
```js
const createRouter = () => new VueRouter({
    linkActiveClass: 'active',
    mode: 'hash',
    base: './',
    routes: constantRouterMap
});
const router = createRouter()
 
 
//在addRoutes之前重置matcher
router.matcher = createRouter().matcher;
router.addRoutes(store.getters.addRouters);
```