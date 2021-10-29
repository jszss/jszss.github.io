---
title: tree 追溯父节点
author: zss
date: 2021-10-29 21:05:46
tags: [tree]
---

<!-- more -->
## 追溯父节点

```js
export function traceParentNode(
  pid,
  data,
  rootPid,
  pidName = "parentId",
  idName = "id",
  childrenName = "children"
) {
  let arr = [];
  foreachTree(data, childrenName, (node) => {
    if (node[idName] == pid) {
      arr.push(node);
      if (node[pidName] != rootPid) {
        arr = arr.concat(
          traceParentNode(node[pidName], data, rootPid, pidName, idName)
        );
      }
    }
  });
  return arr;
}
```

## 寻找所有子节点

```js
export function traceChildNode(
  id,
  data,
  pidName = "parentId",
  idName = "id",
  childrenName = "children"
) {
  let arr = [];
  foreachTree(data, childrenName, (node) => {
    if (node[pidName] == id) {
      arr.push(node);
      arr = arr.concat(
        traceChildNode(node[idName], data, pidName, idName, childrenName)
      );
    }
  });
  return arr;
}
```

## 遍历树节点

```js
export function foreachTree(data, childrenName = "children", callback) {
  for (let i = 0; i < data.length; i++) {
    callback(data[i]);
    if (data[i][childrenName] && data[i][childrenName].length > 0) {
      foreachTree(data[i][childrenName], childrenName, callback);
    }
  }
}
```
