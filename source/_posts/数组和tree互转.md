---
title: 数组和tree互转
author: zss
date: 2021-10-28 21:25:26
tags: [tree]
---

数组和 tree 互转

<!-- more -->

```js
let arr = [
  { id: 1, name: "1", pid: 0 },
  { id: 2, name: "2", pid: 1 },
  { id: 3, name: "3", pid: 1 },
  { id: 4, name: "4", pid: 3 },
  { id: 5, name: "5", pid: 3 },
];
```

## tree 扁平化

### 1. 递归实现

遍历 tree，每一项加进结果集，如果有 children 且长度不为 0，则递归遍历。

```js
function treeToArray(tree) {
  let res = [];
  for (const item of tree) {
    const { children, ...i } = item;
    if (children && children.length) {
      res = res.concat(treeToArray(children));
    }
    res.push(i);
  }
  return res;
}
```

### 2. reduce 实现

```js
function treeToArray(tree) {
  return tree.reduce((res, item) => {
    const { children, ...i } = item;
    return res.concat(
      i,
      children && children.length ? treeToArray(children) : []
    );
  }, []);
}
```

## 扁平化数组转 tree

### 1. 递归实现

最常用到的就是递归实现，思路也比较简单，实现一个方法，该方法传入 tree 父节点和父 id，循环遍历数组，无脑查询，找到对应的子节点，push 到父节点中，再递归查找子节点的子节点。

```js
function arrayToTree(items) {
  let res = [];
  let getChildren = (res, pid) => {
    for (const i of items) {
      if (i.pid === pid) {
        const newItem = { ...i, children: [] };
        res.push(newItem);
        getChildren(newItem.children, newItem.id);
      }
    }
  };
  getChildren(res, 0);
  return res;
}
```

该算法的时间复杂度为 O(2^n)。性能消耗很大。

### 2. map 对象实现

#### 先转 map 再找对应关系

思路：先把数据转成 Map 去存储，然后再遍历的同时借助对象的引用，直接从 Map 找对应的数据做存储。

> Object.prototype.hasOwnProperty: 方法会返回一个布尔值，指示对象自身属性中是否具有指定的属性，会忽略掉那些从原型链上继承到的属性。

```js
function arrayToTree(items) {
  let res = []; // 存放结果集
  let map = {};

  // 先转成map存储
  for (const i of items) {
    map[i.id] = { ...i, children: [] };
  }

  for (const i of items) {
    const newItem = map[i.id];
    if (i.pid === 0) {
      res.push(newItem);
    } else {
      if (Object.prototype.hasOwnProperty.call(map, i.pid)) {
        map[i.pid].children.push(newItem);
      }
    }
  }
  return res;
}
```

有两次循环，时间复杂度为 O(2n)，需要一个 Map 把数据存储起来，空间复杂度 O(n)

当然，我们也可以边做 map 存储，边找对应关系，一次循环搞定。

#### 边做 map 存储，边找对应关系

思路：循环将该项的 id 为键，存储到 map 中，如果已经有该键值对了，则不用存储了，同时找该项的 pid 在不在 map 的键中，在直接对应父子关系，不在就在 map 中生成一个键值对，键为该 pid，然后再对应父子关系。

```js
function arrayToTree(items) {
  let res = []; // 存放结果集
  let map = {};
  // 判断对象是否有某个属性
  let getHasOwnProperty = (obj, property) =>
    Object.prototype.hasOwnProperty.call(obj, property);

  // 边做map存储，边找对应关系
  for (const i of items) {
    map[i.id] = {
      ...i,
      children: getHasOwnProperty(map, i.id) ? map[i.id].children : [],
    };
    const newItem = map[i.id];
    if (i.pid === 0) {
      res.push(newItem);
    } else {
      if (!getHasOwnProperty(map, i.pid)) {
        map[i.pid] = {
          children: [],
        };
      }
      map[i.pid].children.push(newItem);
    }
  }
  return res;
}
```

一次循环就搞定了，性能也很好。时间复杂度为 O(n)，需要一个 Map 把数据存储起来，空间复杂度 O(n)

https://juejin.cn/post/6987224048564437029
