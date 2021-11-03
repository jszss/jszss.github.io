---
title: 'js将list转化为tree格式的 4 种写法'
date: 2020-11-27 10:18:11
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
const list = [{ "menuId" : "5f50c5fb8f0d74536bbfb7a4", "menuName" : "菜单管理", "parentMenuId" : null },
{ "menuId" : "5f524416ff216c2cbc554907", "menuName" : "频道管理", "parentMenuId" : "5f50c5fb8f0d74536bbfb7a4" },
{ "menuId" : "5f576677d9588f3d78fbdb74", "menuName" : "分类管理", "parentMenuId" : "5f524416ff216c2cbc554907" },
{ "menuId" : "5f588b22499cd2538411b98a", "menuName" : "发布管理", "parentMenuId" : "5f50c5fb8f0d74536bbfb7a4" },
{ "menuId" : "5f588b85499cd2538411b98b", "menuName" : "权限管理", "parentMenuId" : "5f50c5fb8f0d74536bbfb7a4" },
{ "menuId" : "5f588f8358bc0d3e647403a1", "menuName" : "菜单管理", "parentMenuId" : "5f588b85499cd2538411b98b" }
...
]
```
## list2tree1
递归遍历children
```js
const list = [...]
// 递归 161202 次 5ms左右时间
const list2tree1 = (list, parentMenuId) => {
    return list.filter(item => {
        if (item.parentMenuId === parentMenuId) {
            item.children = list2tree1(list, item.menuId)
            return true
        }
        return false
    })
}
list2tree1(list, null)
```
## list2tree2
因为方法1是查询的children，所以每次必须全部遍历。
我们换个思路，查询每个节点的parent，查到paret之后，内部循环就可以截止了。（使用find方法）
```js
const list = [...]
// 68976 次 3.6ms左右
const list2tree2 = (list, parentMenuId) => {
    return list.filter(item => {
        if (item.parentMenuId !== parentMenuId) {
            let parent = list.find(parent => parent.menuId === item.parentMenuId)
            if (!parent.children) parent.children = []
            parent.children.push(item)
            return false
        }
        return true
    })
}
list2tree2(list, null)
```

## list2tree3
在方法2的基础上，将每次find的parentNode缓存起来，减少相同parent的查询次数

```js
const list = [...]
// 15337 次 1.8ms左右 cache parent
const list2tree3 = (list, parentMenuId) => {
    let parentObj = {}
    return list.filter(item => {
        if (item.parentMenuId !== parentMenuId) {
            if (!parentObj[item.parentMenuId]) {
                parentObj[item.parentMenuId] = list.find(parent => parent.menuId === item.parentMenuId)
                parentObj[item.parentMenuId].children = []
            }
            parentObj[item.parentMenuId].children.push(item)
            return false
        }
        return true
    })
}
list2tree3(list, null)
```
##list2tree4
遍历tree之前，先遍历一遍数组，将数据缓存到object中。

二次遍历，直接使用object中的缓存
```js
const list = [...]
// 802 次 0.2ms左右
const list2tree4 = (list, parentMenuId) => {
    let menuObj = {}
    list.forEach(item => {
        item.children = []
        menuObj[item.menuId] = item
    })
    return list.filter(item => {
        if (item.parentMenuId !== parentMenuId) {
            menuObj[item.parentMenuId].children.push(item)
            return false
        }
        return true
    })
}
```