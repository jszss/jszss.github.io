---
title: js 获取某月的天数
author: zss
date: 2021-11-06 16:56:25
tags:
---

> 一三五七八十腊，31 天永不差，四六九十一，每月 30 天，惟有二月二十八，闰年要把日加一
> 四年一闰，百年不闰，四百年再闰。可以被 4 整除，但是不能被 100 整除，除非可以被 400 整除。

<!-- more -->

## 借助 Date API 处理日期溢出特性（退位方案）

```js
function getMonthCountDay(year, month) {
  return new Date(year, month, 0).getDate();
}
```

## 借助 Date API 处理日期溢出特性（进位）

```js
function getMonthCountDay(year, month) {
  return 32 - new Date(year, month - 1, 32).getDate();
}
```

## 普通版

```js
function getMonthCountDay(year, month) {
  switch (month) {
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
      return 31;
    case 4:
    case 6:
    case 9:
    case 11:
      return 30;
    case 2:
      return year % 400 == 0 ? 29 : year % 4 != 0 || year % 100 == 0 ? 28 : 29;
  }
}
```

## 延申

```js
// 获取月末是周几
new Date(2021, 11, 0).getDay();
```
