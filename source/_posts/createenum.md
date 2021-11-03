---
title: 'createEnum'
date: 2021-07-02 11:46:15
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
/**
 * 业务常量的使用方式扩展
 * @param {Array} source 
    [
      { value: 1,label: '空间站',name: 'SPACE' },
      { value: 2, label: '实践任务', name: 'PRACTICE' },
      { value: 3, label: '其他系统', name: 'OTHERS' }
    ]
  @returns {Function} fn
    fn() ===> source
    fn(value) ===> label
    fn(name) ===> value
 */
export default function createEnum(source) {
  const sourceMap = new Map()
  source.map(item => {
    sourceMap.set(item.name, item.value)
    sourceMap.set(item.value, item.label)
  })

  return function(key) {
    if (key) {
      return sourceMap.get(key)
    } else {
      return source
    }
  }
}
```
## 使用
```js
export const fieldType = createEnum([
  { value: 1, label: '文本', name: 'TEXT' },
  { value: 2, label: '数字', name: 'NUMBER' },
  { value: 3, label: '视频', name: 'VIDEO' }
])

fieldType()  // list

fieldType(1)  // '文本'
fieldType(1, 2, 3)  // '文本、数组、视频'  代码未实现

fieldType('TEXT')  // 1

```