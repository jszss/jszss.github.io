---
title: '提高Vue渲染性能，了解一下Object.freeze'
date: 2020-07-21 09:42:29
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
当一个 Vue 实例被创建时，它将 data 对象中的所有的 property 加入到 Vue 的响应式系统中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。但是这个过程实际上是比较消耗性能的，所以对于一些有大量数据但只是展示的界面来说，并不需要将property加入到响应式系统中，这样可以提高渲染性能，怎么做呢，你需要了解一下Object.freeze。
在Vue官网中，有这样一段话：这里唯一的例外是使用 Object.freeze()，这会阻止修改现有的 property，也意味着响应系统无法再追踪变化。这段话的意思是，如果我们的数据使用了Object.freeze，就可以让数据脱离响应式系统，那么该如何做呢?
比如下面这个表格，因为只是渲染数据，这时候我们就可以通过Object.freeze来优化性能

```js
<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="date" label="日期" width="180" />
    <el-table-column prop="name" label="姓名" width="180" />
    <el-table-column prop="address" label="地址" />
  </el-table>
</template>
<script>
export default {
  data() {
    const data = Array(1000)
      .fill(1)
      .map((item, index) => {
        return {
          date: '2020-07-11',
          name: `子君${index}`,
          address: '大西安'
        }
      })
    return {
      // 在这里我们用了Object.freeze
      tableData: Object.freeze(data)
    }
  }
}
</script>

```
有的同学可能会有疑问，如果我这个表格的数据是滚动加载的，你这样写我不就没法再给tableData添加数据了吗？是，确实没办法去添加数据了，但还是有办法解决的，比如像下面这样
```js
export default {
  data() {
    return {
      tableData: []
    }
  },
  created() {
    setInterval(() => {
      const data = Array(1000)
        .fill(1)
        .map((item, index) => {
          // 虽然不能冻结整个数组，但是可以冻结每一项数据
          return Object.freeze({
            date: '2020-07-11',
            name: `子君${index}`,
            address: '大西安'
          })
        })
      this.tableData = this.tableData.concat(data)
    }, 2000)
  }
}

```
合理的使用Object.freeze，是可以节省不少渲染性能，特别对于IE浏览器，效果还是很明显的，赶快去试试吧。