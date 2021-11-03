---
title: 'getTargetObject'
date: 2019-09-19 18:16:00
tags: [js utils]
published: true
hideInList: false
feature: 
---
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