---
title: 'treeNest'
date: 2020-05-07 11:16:25
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 方法1
https://blog.csdn.net/Mr_JavaScript/article/details/82817177
```js
     let source = [
          {id:1,parentId:0,name:"一级菜单A",rank:1},
          {id:2,parentId:0,name:"一级菜单B",rank:1},
          {id:3,parentId:0,name:"一级菜单C",rank:1},
          {id:4,parentId:1,name:"二级菜单A-A",rank:2},
          {id:5,parentId:1,name:"二级菜单A-B",rank:2},
          {id:6,parentId:2,name:"二级菜单B-A",rank:2},
          {id:7,parentId:4,name:"三级菜单A-A-A",rank:3},
          {id:8,parentId:7,name:"四级菜单A-A-A-A",rank:4},
          {id:9,parentId:8,name:"五级菜单A-A-A-A-A",rank:5},
          {id:10,parentId:9,name:"六级菜单A-A-A-A-A-A",rank:6},
          {id:11,parentId:10,name:"七级菜单A-A-A-A-A-A-A",rank:7},
          {id:12,parentId:11,name:"八级菜单A-A-A-A-A-A-A-A",rank:8},
          {id:13,parentId:12,name:"九级菜单A-A-A-A-A-A-A-A-A",rank:9},
          {id:14,parentId:13,name:"十级菜单A-A-A-A-A-A-A-A-A-A",rank:10},
      ];

function setTreeData(source) {
    let cloneData = JSON.parse(JSON.stringify(source))
    // 对源数据深度克隆
    return cloneData.filter(father=>{
        // 循环所有项，并添加children属性
        let branchArr = cloneData.filter(child=>father.id == child.parentId);
        // 返回每一项的子级数组
        branchArr.length > 0 ? father.children = branchArr : ''
        //给父级添加一个children属性，并赋值
        return father.parentId == 0;
        //返回第一层
    }
    );
}
console.log(setTreeData(source), 1111111)
// 树形数据

/* 封装函数 */
/* 字段名以字符串的形式传入 */
function treeData(source, id, parentId, children) {
    let cloneData = JSON.parse(JSON.stringify(source))
    return cloneData.filter(father=>{
        let branchArr = cloneData.filter(child=>father[id] == child[parentId]);
        branchArr.length > 0 ? father[children] = branchArr : ''
        return father[parentId] == 0
    }
    )
}
// 调用2
console.table(treeData(source, 'id', 'parentId', 'children'), 22222222222)

let nest = (items,id=null,link='parent_id')=>items.filter(item=>item[link] === id).map(item=>({
    ...item,
    children: nest(items, item.id)
}));

// 调用 3
console.log(nest(source, 0, 'parentId'), 33333)

```
## 方法2
```js
var models = [
 {id: 1, title: 'hello-0', parent: 0},
 {id: 3, title: 'hello-1', parent: 1},
 {id: 4, title: 'hello-3', parent: 3},
 {id: 5, title: 'hello-4', parent: 4},
 {id: 2, title: 'hello-0', parent: 0},
 {id: 6, title: 'hello-4', parent: 4},
 {id: 7, title: 'hello-2', parent: 2},
 {id: 8, title: 'hello-10', parent: 10}
];
var nestedStructure = getNestedChildren(models, 0);
console.log(nestedStructure);

function getNestedChildren(arr, parent) {
    var out = []
    for (let i = 0; i < arr.length; i++) {
        if (arr[i].parent == parent) {
            var children = getNestedChildren(arr, arr[i].id)
            if (children.length) {
                arr[i].children = children
            }
            out.push(arr[i])
        }
    }
    return out
}

```