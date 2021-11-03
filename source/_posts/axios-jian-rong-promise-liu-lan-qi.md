---
title: 'axios 兼容 promise 浏览器'
date: 2019-09-29 10:00:27
tags: [axios,Vue cli 配置]
published: true
hideInList: false
feature: 
---
## 引入 babel-polyfill
```
npm install --save babel-polyfill
```
```js
// vue.config.js
module.exports = {
    configureWebpack: config => {
        return {
            entry: {
                app:['babel-polyfill', './src/main.js']
            }
        }
    }
} 
```