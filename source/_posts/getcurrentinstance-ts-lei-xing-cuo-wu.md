---
title: 'getCurrentInstance ts类型错误'
date: 2021-05-31 10:34:00
tags: []
published: true
hideInList: false
feature: 
isTop: false
---

```js
import {
  ComponentInternalInstance,
  defineComponent,
  getCurrentInstance,
} from '@vue/composition-api';
export default defineComponent({
  setup(){
    // 类型断言
    const { proxy: _this } = getCurrentInstance() as ComponentInternalInstance
  }
})
```