---
title: '表格合并'
date: 2021-06-16 17:26:54
tags: [表格合并]
published: true
hideInList: false
feature: 
isTop: false
---
```js
<template>
  <div class="tableBox">
    <div class="buttons">
      <a-button @click="onFilter">取消过滤</a-button>
      <a-button
        v-for="item in filterArr"
        :key="item.value"
        @click="onFilter(item)"
        >{{ item.value }}</a-button
      >
    </div>
    <a-table
      :rowKey="(record, idx) => idx"
      :columns="columns"
      :data-source="tableData"
      :pagination="false"
      bordered
    >
    </a-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      columns: [
        {
          title: '',
          dataIndex: 'title',
          width: 120,
          customRender: (text, row) => {
            return {
              children: `${text}`,
              attrs: {
                rowSpan: row.titleRowSpan
              }
            };
          }
        },
        {
          title: '部门',
          dataIndex: 'department',
          width: 120,
          customRender: (text, row, index) => {
            return {
              children: `${text}`,
              attrs: {
                rowSpan: row.departmentRowSpan
              }
            };
          }
        },
        {
          title: '代码类型',
          dataIndex: 'codeType',
          width: 120
        },
        {
          title: '总数',
          dataIndex: 'totalCount',
          width: 120
        },
        {
          title: '修复',
          dataIndex: 'fixCount',
          width: 120
        },
        {
          title: '未修复',
          dataIndex: 'notFixedCount',
          width: 120
        },
        {
          title: '今日新增',
          dataIndex: 'todayAdd',
          width: 120
        },
        {
          title: 'Bug类型',
          dataIndex: 'bugType',
          width: 120,
          customRender: (text, row, index) => {
            return {
              children: `${text}`,
              attrs: {
                rowSpan: row.bugTypeRowSpan
              }
            };
          }
        }
      ],
      tableData: [
        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: 'ui展示问题',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: 'ui展示问题',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          bugType: 'ui展示问题',
          codeType: 'ui展示问题总计',
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '功能性bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '功能性bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          bugType: '功能性bug',
          codeType: '功能性bug总计',
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '前端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '前端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 3,
          bugType: '前端bug',
          codeType: '前端bug总计',
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '后端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '后端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 2,
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 5,
          bugType: '后端bug',
          codeType: '后端bug总计',
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '非bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '非bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发一部'
        },

        {
          fixCount: 1,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 5,
          bugType: '非bug',
          codeType: '非bug总计',
          title: 'bug总览',
          department: '开发一部'
        },
        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: 'ui展示问题',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: 'ui展示问题',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          bugType: 'ui展示问题',
          codeType: 'ui展示问题总计',
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '功能性bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '功能性bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          bugType: '功能性bug',
          codeType: '功能性bug总计',
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '前端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '前端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 3,
          bugType: '前端bug',
          codeType: '前端bug总计',
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '后端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '后端bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 2,
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 5,
          bugType: '后端bug',
          codeType: '后端bug总计',
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 0,
          id: 0,
          codeType: '新代码',
          bugType: '非bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },
        {
          fixCount: 0,
          id: 1,
          codeType: '老代码',
          bugType: '非bug',
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 0,
          title: 'bug总览',
          department: '开发二部'
        },

        {
          fixCount: 1,
          notFixedCount: 0,
          todayAdd: 0,
          totalCount: 5,
          bugType: '非bug',
          codeType: '非bug总计',
          title: 'bug总览',
          department: '开发二部'
        }
      ]
    };
  },
  methods: {
    //  合并单元格
    combineRow(key) {
      const tableData = this.tableData;
      for (var i = 0; i < tableData.length; i++) {
        const item = tableData[i];
        let count = 1;
        for (let j = i + 1; j < tableData.length; j++) {
          // 如果是同一个值，往后递增
          if (item[key] === tableData[j][key]) {
            count++;
            // 往后相同的值都设为空单元格
            tableData[j][`${key}RowSpan`] = 0;
            // 只有同值第一个才设置合并的单元格数
            item[`${key}RowSpan`] = count;
            // 所有都是为同一个值的情况
            // 如果到了尾部，
            if (j === tableData.length - 1) {
              return;
            }
          } else {
            // 指针跳转到下一个，从下一排开始
            i = j - 1;
            count = 1;
            tableData[j][`${key}RowSpan`] = 0;
            break;
          }
        }
        console.log(i);
      }
      this.tableData = tableData;
    },
    // 过滤组
    filterGroup(targets) {
      const res = this.tableData.reduce((obj, cur) => {
        for (let i of targets) {
          const item = { key: i, value: cur[i] };
          if (!obj[item.value]) {
            obj[item.value] = item;
          }
        }
        return obj;
      }, {});
      return Object.values(res);
    },
    onFilter(params) {
      this.tableData = JSON.parse(JSON.stringify(this.originTableData));
      if (!params) {
        return;
      }
      const { key, value } = params;
      this.tableData = this.tableData.filter((item) => item[key] === value);
      this.initCombineRow();
    },
    initCombineRow() {
      this.combineRow('title');
      this.combineRow('department');
      this.combineRow('bugType');
    }
  },
  created() {
    this.initCombineRow();
    this.originTableData = JSON.parse(JSON.stringify(this.tableData));
    this.filterArr = this.filterGroup(['department', 'bugType']);
  }
};
</script>

<style lang="less" scoped>
.tableBox {
  width: 80vw;
  margin: 0 auto;
  .buttons {
    margin: 10px 0;
  }
}
/deep/.ant-table-bordered .ant-table-thead > tr > th,
/deep/.ant-table-bordered .ant-table-tbody > tr > td {
  padding: 2px;
  text-align: center;
}
</style>
```