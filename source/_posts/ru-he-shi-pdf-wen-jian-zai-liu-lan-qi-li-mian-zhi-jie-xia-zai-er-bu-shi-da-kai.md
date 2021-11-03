---
title: '如何使 pdf 文件在浏览器里面直接下载而不是打开'
date: 2021-01-20 09:14:46
tags: [pdf]
published: true
hideInList: false
feature: 
isTop: false
---
```js
window.open('url')
```
```js
<a href='url' download='文件名'>点击下载PDF</a>
```
### 额外
这种需求的解决方式就是将PDF文件的 MIME type 改为 `application/octet-stream` 并加入 `Content-Disposition:attachment header`，原本的 pdf 文件 MIME type 为 `application/pdf`，浏览器识别到这个 type 之后会自动在浏览器打开，所以说我们在这里修改 type 即可。

修改的方法有两种，一种是在后端进行修改，上传文件或者返回文件的时候进行操作，但是绝大多数情况下文件都是存储到 cdn 服务器中的，后端也不方便对其进行操作，这个时候就需要前端来修改了。
```js
/**
 * @deprecated 下载文件
 * @param {string} url 
 * @param {string} filename
 */
handleFileDownload = (url, filename) => {
  // 创建 a 标签
  let a = document.createElement('a');
  a.href = url;
  a.download = filename;
  a.click();
}

/**
 * @deprecated 处理 pdf url，使其不在浏览器打开
 * @param {string} url
 */
handlePdfLink = (url, filename) => {
  fetch(url, {
    method: 'get',
    responseType: 'arraybuffer',
  })
    .then(function (res) {
      if (res.status !== 200) {
        return res.json()
      }
      return res.arrayBuffer()
    })
    .then((blobRes) => {
    	// 生成 Blob 对象，设置 type 等信息
      const e = new Blob([blobRes], {
        type: 'application/octet-stream',
        'Content-Disposition':'attachment'
      })
      // 将 Blob 对象转为 url
      const link = window.URL.createObjectURL(e)
      handleFileDownload(link, filename)
    }).catch(err => {
      console.error(err)
    })
}
```
网友解决方案
```js
我的做法是直接在nginx里面配置，拦截掉所有.pdf后缀的路径
proxy_hide_header 'Content-Type';
add_header Content-Type application/octet-stream;
这样子 无需任何代码改动
```
https://www.cnblogs.com/Jacob98/p/directly-download-pdf.html