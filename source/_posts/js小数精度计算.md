---
title: js小数精度计算
author: zss
date: 2021-11-12 15:14:56
tags:
---

## JavaScript 小数精度计算

````js
/**
 * 数字运算（主要用于小数点精度问题）
 * @param {number} a 前面的值
 * @param {"+"|"-"|"*"|"/"} type 计算方式
 * @param {number} b 后面的值
 * @example
 * ```js
 * // 可链式调用
 * const res = computeNumber(1.3, "-", 1.2).next("+", 1.5).next("*", 2.3).next("/", 0.2).result;
 * console.log(res);
 * ```
 */
function computeNumber(a, type, b) {
  /**
   * 获取数字小数点的长度
   * @param {number} n 数字
   */
  function getDecimalLength(n) {
    const decimal = n.toString().split(".")[1];
    return decimal ? decimal.length : 0;
  }
  /**
   * 修正小数点
   * @description 防止出现 `33.33333*100000 = 3333332.9999999995` && `33.33*10 = 333.29999999999995` 这类情况做的处理
   * @param {number} n
   */
  const amend = (n, precision = 15) =>
    parseFloat(Number(n).toPrecision(precision));
  const power = Math.pow(
    10,
    Math.max(getDecimalLength(a), getDecimalLength(b))
  );
  let result = 0;

  a = amend(a * power);
  b = amend(b * power);

  switch (type) {
    case "+":
      result = (a + b) / power;
      break;
    case "-":
      result = (a - b) / power;
      break;
    case "*":
      result = (a * b) / (power * power);
      break;
    case "/":
      result = a / b;
      break;
  }

  result = amend(result);

  return {
    /** 计算结果 */
    result,
    /**
     * 继续计算
     * @param {"+"|"-"|"*"|"/"} nextType 继续计算方式
     * @param {number} nextValue 继续计算的值
     */
    next(nextType, nextValue) {
      return computeNumber(result, nextType, nextValue);
    },
  };
}
````
