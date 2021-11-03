---
title: 'node cors 跨域设置'
date: 2020-08-04 11:01:05
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
// 设置跨域
app.use(cors({
    origin: function (ctx) {
        if (ctx.url.indexOf(config.API_VERSION_PATH) > -1) {
          return isDev ? 'http://192.xxx.1.3:8000' : 'http://qutanqianduan.cn'; // 允许来自指定域名请求, 如果设置为*，前端将获取不到错误的响应头
        }
    },
    exposeHeaders: ['WWW-Authenticate', 'Server-Authorization', 'x-show-msg'],
    maxAge: 5,  //  该字段可选，用来指定本次预检请求的有效期，单位为秒
    credentials: true,  // 允许携带用户凭证
    allowMethods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'], // 允许的请求方法
    allowHeaders: ['Content-Type', 'Authorization', 'Accept', 'X-Requested-With'] // 允许接收的头部字段
}))

```