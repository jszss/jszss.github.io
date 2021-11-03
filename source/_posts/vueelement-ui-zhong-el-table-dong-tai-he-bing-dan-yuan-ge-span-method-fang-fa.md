---
title: 'Vue+Element-UI 中 el-table 动态合并单元格 :span-method 方法'
date: 2021-01-18 17:26:02
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
<template>
          <el-table
            border
            size="mini"
            height="100%"
            :span-method="cellMerge"
            :data="tableData"
          >
            <el-table-column
              label="设备"
              align="center"
              prop="a"
            />
            <el-table-column
              label="参数"
              align="center"
              prop="b"
            />
            <el-table-column
              label="数值"
              align="num"
              prop="c"
            />
          </el-table>
</template>
<script>
export default {
  data () {
    return {
      tableData: [
        { a: '2222', b: '1', c: '2' },
        { a: '111', b: '1', c: '2' },
        { a: '111', b: '2', c: '3' },
        { a: '111', b: '2', c: '3' },
        { a: '111', b: '2', c: '3' },
        { a: '2222', b: '1', c: '2' },
        { a: '2222', b: '1', c: '2' },
        { a: '111', b: '2222', c: '3333' },
        { a: '111', b: '2222', c: '3333' }
      ],
      spanArr: []
    }
  },
  methods: {
    // groupBy 数组
    groupBy (data, params) {
      const groups = {}
      data.forEach(v => {
        const group = JSON.stringify(v[params])
        groups[group] = groups[group] || []
        groups[group].push(v)
      })
      return Object.values(groups)
    },
    // 计算 数据合并 索引
    getSpanArr (data, params) {
      // 接收重构数组
      let arr = []

      // 设置索引
      let pos = 0

      // 控制合并的数组
      this.spanArr = []

      // arr 处理
      this.groupBy(data, params).map(v => (arr = arr.concat(v)))
      
      // this.tableData = arr
      arr.map(res => {
        data.shift()
        data.push(res)
      })

      // spanArr 处理
      const redata = arr.map(v => v[params])
      redata.reduce((old, cur, i) => {
        if (i === 0) {
          this.spanArr.push(1)
          pos = 0
        } else {
          if (cur === old) {
            this.spanArr[pos] += 1
            this.spanArr.push(0)
          } else {
            this.spanArr.push(1)
            pos = i
          }
        }
        return cur
      }, {})
    },

    // 合并 tableData 数据
    cellMerge ({ row, column, rowIndex, columnIndex }) {
      if (columnIndex === 0) {
        const _row = this.spanArr[rowIndex]
        const _col = _row > 0 ? 1 : 0
        return {
          rowspan: _row,
          colspan: _col
        }
      }
    }
  },
  created () {
    this.getSpanArr(this.tableData, 'a')
  }
}
</script>

```