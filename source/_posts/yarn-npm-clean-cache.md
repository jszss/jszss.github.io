---
title: 'npm 常用命令行'
date: 2021-03-15 09:41:36
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 清理缓存
```bat
:: 查看缓存地址
:: yarn cache dir
:: 清理缓存
yarn cache clean
:: 设置缓存地址
:: yarn config set cache-folder E:\cache\yarn_cache

:: 查看缓存地址
@REM npm config get cache
:: 清理缓存
@REM npm cache clean --force
:: 设置缓存地址
@REM npm config set cache "E:\cache\npm_cache"
:: 验证清理的有效性
@REM npm cache verify
```
## 查看全局包
```bat
npm list -g --depth 0
```