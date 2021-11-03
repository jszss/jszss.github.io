---
title: 'vscode 代码格式化 eslint+prettier+vetur'
date: 2021-02-18 09:04:36
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 安装插件
eslint vetur prettier - code formatter
### 配置 vscode settings.json
```
{
  ...
  
    // 保存的时候格式化
    "editor.formatOnSave": true,
    
    // 启用 eslint 格式化
    "eslint.format.enable": true,
  
    // 采用 eslint 格式化
    "[vue]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
    },
    "[javascript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
    },
    "[typescript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
    }
}
```
### 配置 .prettierrc
```
{
  "spaceBeforeFunctionParen": true,
  "tabWidth": 2,
  "useTabs": false,
  "trailingComma": "none",
  "eslintIntegration": true,
  "singleQuote": true,
  "semi": false,
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "arrowParens": "avoid"
}
```
