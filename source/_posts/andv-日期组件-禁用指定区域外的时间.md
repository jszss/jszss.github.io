---
title: andv 日期组件 禁用指定区域外的时间
author: zss
date: 2021-11-25 21:32:12
tags: [andv]
---

ant design vue `DatePicker` 组件禁用指定区域外的时间

<!-- more -->

## andv 日期组件 禁用指定区域外的时间

```html
<template>
  <div>
    <a-date-picker
      v-model="startValue"
      :disabled-date="disabledStartDate"
      show-time
      format="YYYY-MM-DD HH:mm:ss"
      placeholder="Start"
      @openChange="handleStartOpenChange"
    />
    <a-date-picker
      v-model="endValue"
      :disabled-date="disabledEndDate"
      show-time
      format="YYYY-MM-DD HH:mm:ss"
      placeholder="End"
      :open="endOpen"
      @openChange="handleEndOpenChange"
    />
  </div>
</template>
<script>
  import moment from "moment";
  export default {
    data() {
      return {
        startValue: null,
        endValue: null,
        endOpen: false,
      };
    },
    watch: {
      startValue(val) {
        console.log("startValue", val);
      },
      endValue(val) {
        console.log("endValue", val);
      },
    },
    methods: {
      disabledStartDate(startValue) {
        const endValue = this.endValue;
        if (!startValue || !endValue) {
          return false;
        }
        return startValue.valueOf() > endValue.valueOf();
      },
      disabledEndDate(endValue) {
        const startValue = this.startValue;
        if (!endValue || !startValue) {
          return false;
        }
        // return startValue.valueOf() >= endValue.valueOf();
        /**
         * endValue：面板显示的每个日期
         * startValue < endValue < 年末
         * 取反：不属于此范围的日期禁用，返回true
         */
        const lastYearDay = moment().endOf("year");
        console.log("=================");
        console.log("lastYearDay", lastYearDay.format());
        console.log("startValue", startValue.format());
        console.log("endValue", endValue.format());
        console.log("startValue > endValue", startValue > endValue);
        console.log("endValue > lastYearDay", endValue > lastYearDay);
        console.log("=================");
        return startValue > endValue || endValue > lastYearDay;
      },
      handleStartOpenChange(open) {
        if (!open) {
          this.endOpen = true;
        }
      },
      handleEndOpenChange(open) {
        this.endOpen = open;
      },
    },
  };
</script>
```
