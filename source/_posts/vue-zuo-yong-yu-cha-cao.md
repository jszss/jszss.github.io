---
title: 'Vue 作用域插槽'
date: 2019-09-16 10:38:35
tags: []
published: true
hideInList: false
feature: 
---
## 作用域插槽
```html
<template>
  <div>
    <slot v-if="loading" name="loading">
        <div>Loading ...</div>
    </slot>
    <slot v-else :data='data' :loading='loading'> 
    <!-- 简写 -->
    <!-- <slot v-else v-bind={data, loading}> -->
    </slot>
  </div>
</template>

<script>
export default {
  props: ["url"],
  data: () => ({
    loading: true,
    data: null
  }),
  async created() {
    this.data = await fetch(this.url);
    this.loading = false;
  }
};
</script>
```
**用法**
```html
<lazy-loading url="https://www.baidu.com">
  <template #default="{ data,loading }">
    <div>{{ data }}</div>
    <div>{{ loading }}</div>
  </template>
</lazy-loading>

```