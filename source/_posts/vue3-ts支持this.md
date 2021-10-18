---
title: vue3-ts支持this.
author: zss
date: 2021-10-18 17:16:34
tags:
---

```ts
// main.ts
app.config.globalProperties.$axios = axios;
```
```ts
// global.d.ts

import { ComponentCustomProperties } from 'vue'

// axios的实例类型
import { AxiosInstance } from 'axios'

// 声明要扩充@vue/runtime-core包的声明.
// 这里扩充"ComponentCustomProperties"接口, 因为他是vue3中实例的属性的类型.
declare module '@vue/runtime-core' {
  
  // 给`this.$http`提供类型
  interface ComponentCustomProperties {
    $axios: AxiosInstance;
  }
}
```