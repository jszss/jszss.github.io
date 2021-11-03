---
title: '格式化日期'
date: 2020-12-28 14:48:49
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
/**
 * 格式化日期
 * @param {string | number | Date} value 指定日期
 * @param {string} format 格式化的规则
 * @example
 * ```js
 * formatDate();
 * formatDate(1603264465956);
 * formatDate(1603264465956, "h:m:s");
 * formatDate(1603264465956, "Y年M月D日");
 * ```
 */
function formatDate(value = Date.now(), format = "Y-M-D h:m:s") {
    const formatNumber = n => `0${n}`.slice(-2);
    const date = new Date(value);
    const formatList = ["Y", "M", "D", "h", "m", "s"];
    const resultList = [];
    resultList.push(date.getFullYear().toString());
    resultList.push(formatNumber(date.getMonth() + 1));
    resultList.push(formatNumber(date.getDate()));
    resultList.push(formatNumber(date.getHours()));
    resultList.push(formatNumber(date.getMinutes()));
    resultList.push(formatNumber(date.getSeconds()));
    for (let i = 0; i < resultList.length; i++) {
        format = format.replace(formatList[i], resultList[i]);
    }
    return format;
}


/**
 * 获取指定日期时间戳
 * @param {number} time 毫秒数
 */
export function getDateFormat (time = Date.now()) {
  if (!time) return ''
  const date = new Date(time)
  return `${date.toLocaleDateString()} ${date.toTimeString().slice(0, 8)}`
}
```