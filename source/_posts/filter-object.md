---
title: 'filter Object'
date: 2019-09-19 18:16:00
tags: [js utils]
published: true
hideInList: false
feature: 
---
# 过滤目标对象 / 过滤掉两个对象相等的值
## 过滤目标对象 getTargetObject
/**
 *
 * @param {Object} targetObject
 * @param {Array} propsArray
 */
export function getTargetObject(targetObject, propsArray) {
  if (typeof (targetObject) !== 'object' || !Array.isArray(propsArray)) {
    throw new Error('参数格式不正确')
  }
  const result = {}
  Object.keys(targetObject).filter(key => propsArray.includes(key)).forEach(key => {
    result[key] = targetObject[key]
  })
  return result
}
## 过滤掉两个对象相等的值
```
/**
 * 比较两个对象是否相等
 * 相等返回obj2
 * 不等 返回不相同的值 和 reserveArray数组保留的值
 *
 * @export
 * @param {*} obj1
 * @param {*} obj2
 * @param {*} reserveArray
 * @returns
 */
export function getObjectDifferent(obj1, obj2, reserveArray) {
  var data = {}
  var isEqually = true
  for (var key in obj1) {
    if (obj1.hasOwnProperty(key) && obj1[key] !== obj2[key]) {
      data[key] = obj2[key]
      isEqually = false
    }
  }

  if (isEqually) {
    data = obj2
  } else {
    for (var i = 0; i < reserveArray.length; i++) {
      var item = reserveArray[i]
      data[item] = obj2[item]
    }
  }
  // reserveArray.forEach(item => {
  //   data[item] = obj2[item];
  // })
  return {
    isEqually: isEqually,
    data: data
  }
}
```