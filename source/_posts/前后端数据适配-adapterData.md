---
title: 前后端数据适配-adapterData()
author: zss
date: 2021-10-22 17:39:29
tags:
---

```js
/**
 * 前后端数据对象 key 适配
 * @example
 * const backendData = { id: 1, stu_name: "姓名", stu_age: 20, stu_classId: 3 };
  const frontend = adapterData(backendData, [ "id", "stu_name:stuName", "stu_age:stuAge"]);
  // 返回数据
  // { "id": 1, "stuName": "姓名", "stuAge": 20, "stu_classId": 3 }
 * @param {object} sourceObj - 源数据
 * @param {string[]} filter - 条件
 * @returns {object} 适配数据
 */
function adapterData(sourceObj, filter) {
  // console.log(fn);
  return new Function(
    "sourceObj",
    "filter",
    `
    let {${filter.join(",")}, ...other} = sourceObj;
    let tempObj = {${filter.map((i) => i.split(":")[1] || i).join(",")}};
    return {...tempObj, ...other}
  `
  )(sourceObj, filter);
}
```