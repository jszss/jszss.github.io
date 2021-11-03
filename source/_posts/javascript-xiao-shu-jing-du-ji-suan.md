---
title: 'JavaScript小数精度计算'
date: 2020-12-28 14:47:32
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
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
    /** 倍率 */
    const power = Math.pow(10, Math.max(getDecimalLength(a), getDecimalLength(b)));
    let result = 0;
    
    // 防止出现 `33.33333*100000 = 3333332.9999999995` && `33.33*10 = 333.29999999999995` 这类情况做的暴力处理
    a = Math.round(a * power);
    b = Math.round(b * power);

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
            result = a  / b ;
            break;
    }
    
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
        }
    };
}

```