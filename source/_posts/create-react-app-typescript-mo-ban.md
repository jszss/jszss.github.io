---
title: 'create-react-app typescript模板'
date: 2021-04-23 10:10:29
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 解决别名配置问题
```json
// tsconfig.json
{
    ...
    "extends": "./paths.json"
}
```
```json
// paths.json
{
    "compilerOptions": {
        "baseUrl": "src",
        "paths": {
            "@/*": ["*"]
        }
    }
}
```