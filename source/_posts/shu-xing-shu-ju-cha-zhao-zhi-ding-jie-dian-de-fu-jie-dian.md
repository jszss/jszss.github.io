---
title: '树形数据 查找指定节点的父节点'
date: 2021-06-09 10:19:23
tags: [tree-data]
published: true
hideInList: false
feature: 
isTop: false
---
```js
const data = [
  {
    id: 1,
    label: '一级 1',
    children: [{
      id: 4,
      label: '二级 1-1',
      children: [{
        id: 9,
        label: '三级 1-1-1'
      }, {
        id: 10,
        label: '三级 1-1-2'
      }]
    }]
  },
  {
    id: 2,
    label: '一级 2',
    children: [{
      id: 5,
      label: '二级 2-1'
    }, {
      id: 6,
      label: '二级 2-2'
    }]
  },
  {
    id: 3,
    label: '一级 3',
    children: [{
      id: 7,
      label: '二级 3-1'
    }, {
      id: 8,
      label: '二级 3-2'
    }]
  }];
```
```js
function findParentNode(arr, id, parent) {
    for (let item of arr) {
      if (item.id === id) {
        return parent || arr;
      }
      if (item.children) {
        let node = findParentNode(item.children, id, item)
        if(node){
            return node
        }
      }
    }
    return null;
}
findParentNode(data,9) // { id:4, label: "二级 1-1", children:[] }
```