---
title: 'JavaScript：如何获取某一天所在的星期'
date: 2019-09-17 08:28:34
tags: [ECMAScript,Date]
published: true
hideInList: false
feature: 
---
[如何获取某一天所在的星期](https://segmentfault.com/a/1190000020342937)
```js
function getWeekStartAndEnd(timestamp) {
    const oneDayTime = 1000 * 60 * 60 * 24; // 一天里一共的毫秒数
    const today = timestamp ? new Date(timestamp) : new Date();
    const todayDay = today.getDay() || 7; // 若那一天是周末时，则强制赋值为7
    const startDate = new Date(
        today.getTime() - oneDayTime * (todayDay - 1)
    );
    const endDate = new Date(today.getTime() + oneDayTime * (7 - todayDay));

    return { startDate, endDate };
}
```