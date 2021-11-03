---
title: 'Axios 接口响应拦截处理'
date: 2020-04-13 15:53:09
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
接口响应的拦截主要是对接口返回的数据进行提取、封装使用，以及对请求异常进行统一配置处理。
```js
request.interceptors.response.use(
  response => {
    const data = response.data || {};
    return data;
  },
  error => {
    const code = error.response.status;
    if (code) {
      let msg = '';
      switch (code) {
        case 400:
          msg = '请求错误';
          break;
        case 401:
          msg = '未授权，请登录';
          break;
        case 403:
          msg = '拒绝访问';
          break;
        case 404:
          msg = `请求${error.response.config.url}出现404错误`;
          break;
        case 408:
          msg = '请求超时';
          break;
        case 500:
          msg = '服务器内部错误';
          break;
        case 501:
          msg = '服务未实现';
          break;
        case 502:
          msg = '网关错误';
          break;
        case 503:
          msg = '服务不可用';
          break;
        case 504:
          msg = '网关超时';
          break;
        case 505:
          msg = 'HTTP版本不受支持';
          break;
      }
      Message.error(msg);
    }
    return Promise.reject(error);
  }
)

```
#### API方法封装
单独封装接口请求方法， GET方法的参数为params，POST方法的参数为data。
```js
// api.js
import request from '@/utils/request';

export function APIPostMethod(data) { // 自定义接口方法
  return request({
    url: '/url1',
    method: 'post',
    data
  });
}
export function APIGetMethod(params) { // 自定义接口方法
  return request({
    url: '/url2',
    method: 'get',
    params
  });
}

```
在业务中调用API方法
```js
import { APIGetMethod, APIPostMethod } from '@/utils/request';
const params = {}
APIGetMethod(params).then(res => {
//...
//对数据处理
})

```