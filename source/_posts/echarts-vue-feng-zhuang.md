---
title: 'echarts vue封装'
date: 2020-07-31 15:58:45
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
<template>
  <div class="echarts"></div>
</template>
<script>
export default {
  mounted() {
    this.chart = echarts.init(this.$el)
    // 请求数据，赋值数据 等等一系列操作...
    // 监听窗口发生变化，resize组件
    window.addEventListener('resize', this.$_handleResizeChart)
  },
  updated() {
    // 干了一堆活
  },
  created() {
    // 干了一堆活
  },
  beforeDestroy() {
    // 组件销毁时，销毁监听事件
    window.removeEventListener('resize', this.$_handleResizeChart)
  },
  methods: {
    $_handleResizeChart() {
      this.chart.resize()
    },
    // 其他一堆方法
  }
}
</script>
```
## 优化
```js
export default {
  mounted() {
    this.chart = echarts.init(this.$el)
    // 请求数据，赋值数据 等等一系列操作...
    
    // 监听窗口发生变化，resize组件
    window.addEventListener('resize', this.$_handleResizeChart)
    // 通过hook监听组件销毁钩子函数，并取消监听事件
    this.$once('hook:beforeDestroy', () => {
      window.removeEventListener('resize', this.$_handleResizeChart)
    })
  },
  updated() {},
  created() {},
  methods: {
    $_handleResizeChart() {
      // this.chart.resize()
    }
  }
}
```