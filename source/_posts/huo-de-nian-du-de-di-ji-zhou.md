---
title: '获得年度的第几周'
date: 2019-10-09 15:12:42
tags: []
published: true
hideInList: false
feature: 
---
```js
var getMonthWeek = function(a, b, c) {
    var date = new Date(a,parseInt(b) - 1,c)
      , w = date.getDay()
      , d = date.getDate();
    return Math.ceil((d + 6 - w) / 7);
};

var getYearWeek = function(a, b, c) {
    var date1 = new Date(a,parseInt(b) - 1,c)
      , date2 = new Date(a,0,1)
      , d = Math.round((date1.valueOf() - date2.valueOf()) / 86400000);
    return Math.ceil((d + ((date2.getDay() + 1) - 1)) / 7);
};

var today = new Date();
//获取当前时间
var y = today.getFullYear();
var m = today.getMonth() + 1;
var d = today.getDate();
document.write("<p>今天是：", y, "-", m, "-", d, "</p>");
document.write("<p>今天是", y, "年的第", getYearWeek(y, m, d), "周</p>");
document.write("<p>今天是", m, "月的第 ", getMonthWeek(y, m, d), " 周</p>");
var quarter = "";
var result = getYearWeek(y, m, d);
if (m < 4) {
    quarter = 1;
    week = result;
} else if (m < 7) {
    quarter = 2;
    week = result - getYearWeek(y, 4, 1);
    var day = new Date(y,4,1);
    if (day.getDay() > 1) {
        week += 1;
    }
} else if (m < 10) {
    quarter = 3;
    week = result - getYearWeek(y, 7, 1);
    var day = new Date(y,7,1);
    if (day.getDay() > 1) {
        week += 1;
    }
} else {
    quarter = 4;
    week = result - getYearWeek(y, 10, 1);
    var day = new Date(y,10,1);
    if (day.getDay() > 1) {
        week += 1;
    }
}
document.write("<p>今天是第", quarter, "季度的第 ", week, " 周</p>");

```