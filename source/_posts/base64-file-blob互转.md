---
title: "base64,file,blob互转"
author: zss
date: 2021-10-29 21:08:51
tags:
---

> base64ToFile
> base64ToBlob
> fileToBase64

<!--  -->

## base64 转 file

```js
/**
 *  @param { base64 } base64
 *  @param { string } filename 转换后的文件名
 */
export const base64ToFile = (base64, filename) => {
  let arr = base64.split(",");
  let mime = arr[0].match(/:(.*?);/)[1];
  let suffix = mime.split("/")[1]; // 图片后缀
  let bstr = atob(arr[1]);
  let n = bstr.length;
  let u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new File([u8arr], `${filename}.${suffix}`, { type: mime });
};
```

## 复制代码 base64 转 blob

```js
/**
 *  @param { base64 } base64
 */
export const base64ToBlob = (base64) => {
  let arr = base64.split(","),
    mime = arr[0].match(/:(.*?);/)[1],
    bstr = atob(arr[1]),
    n = bstr.length,
    u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new Blob([u8arr], { type: mime });
};
```

## 复制代码 blob 转 file

```js
/**
 *  @param { blob } blob
 *  @param { string } fileName
 */
export const blobToFile = (blob, fileName) => {
  blob.lastModifiedDate = new Date();
  blob.name = fileName;
  return blob;
};
```

## 复制代码 file 转 base64

```js
/**
 * @param { * } file 图片文件
 */
export const fileToBase64 = (file) => {
  let reader = new FileReader();
  reader.readAsDataURL(file);
  reader.onload = function (e) {
    return e.target.result;
  };
};
```
