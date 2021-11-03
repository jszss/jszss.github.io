---
title: '数组forEach不能中途退出？教你封装可中途退出的函数'
date: 2021-05-17 08:49:16
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
    Array.prototype.nextEach = function (callback) {
      let _this = this;

      !function fn(i) {
        new Promise(res => {
          callback(_this[i], i, res);
        }).then(() => {
          i + 1 < _this.length && fn(i + 1);
        })
      }(0)
    }

    let arr = [{ count: 2 }, { count: 3 }, { count: 4 }, { count: 5 }, { count: 6 }];

    //demo: 只遍历到 count < 4
    arr.nextEach((item, i, next) => {
      console.log(item, i);
      // 执行next，才会遍历下一个
      item.count < 4 && next();
    })
```
https://www.toutiao.com/i6962823796386726404