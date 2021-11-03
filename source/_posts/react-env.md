---
title: 'React .env '
date: 2021-06-30 09:34:29
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
https://github.com/toddbluhm/env-cmd
```json
"scripts": {
    "start": "react-scripts start",
    "start:staging": "env-cmd -f .env.staging react-scripts start",
    "start:prod": "env-cmd -f .env.production react-scripts start",
    "build": "react-scripts build",
    "build:staging": "env-cmd -f .env.staging react-scripts build",
    "build:prod": "env-cmd -f .env.production react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
}
```
https://zhuanlan.zhihu.com/p/362418612 