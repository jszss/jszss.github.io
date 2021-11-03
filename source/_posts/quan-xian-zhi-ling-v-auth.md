---
title: '权限指令 v-auth'
date: 2020-10-09 10:54:31
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
除了 Vue 内置的一些指令比如 v-model、v-if 等，Vue 还允许我们自定义指令。在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。比如我们可以通过自定义一个指令来控制按钮的权限。我们期望设计一个如下形式的指令来控制按钮权限：

```js
<button v-auth="['user']">提交</button>
```
通过在按钮的指令里传入一组权限，如果该按钮只有 admin 权限才可以提交，而我们传入一个别的权限，比如 user，那这个按钮就不应该显示了。接下来我们去注册一个全局的指令：
```js
// auth.js
const AUTH_LIST = ['admin']

function checkAuth(auths) {
    return AUTH_LIST.some(item => auths.includes(item))
}

function install(Vue, options = {}) {
    Vue.directive('auth', {
        inserted(el, binding) {
            if (!checkAuth(binding.value)) {
                el.parentNode && el.parentNode.removeChild(el)
            }
        }
    })
}

export default { install }
```
然后我们需要在 main.js 里通过安装插件的方式来启用这个指令：
```js
import Auth from './utils/auth'
Vue.use(Auth)
```