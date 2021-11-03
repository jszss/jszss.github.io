---
title: '权限组件 authority'
date: 2020-10-09 10:52:53
tags: [权限组件]
published: true
hideInList: false
feature: 
isTop: false
---
这里将使用渲染函数实现上面介绍过的的权限按钮。使用方式如下，把需要控制权限的按钮包在权限组件 authority 里面，如果有该权限就显示，没有就不显示。
```js
<authority :auth="['admin']">
    <button>提交</button>
</authority>
```
然后我们用渲染函数去实现一个 authority 组件：
```js
<script>
const AUTH_LIST = ['admin', 'user', 'org']

function checkAuth(auths) {
    return AUTH_LIST.some(item => auths.includes(item))
}
export default {
    functional: true,
    props: {
        auth: {
            type: Array,
            required: true
        }
    },
    render(h, context) {
        const { props,  scopedSlots} = context
        return checkAuth(props.auth) ? scopedSlots.default() : null
    }
}
</script>
```
全局注册这个组件：
```js
// main.js
import Authority from './components/authority'
Vue.component('authority', Authority)
```