---
title: '前端实现批量导出图片并打包压缩功能'
date: 2020-10-15 13:32:32
tags: [jszip,file-saver]
published: true
hideInList: false
feature: 
isTop: false
---
```js
import axios from 'axios'
import JSZip from 'jszip'
import FileSaver from 'file-saver'
const getFile = (url) => {
      return new Promise((resolve, reject) => {
        axios({
          method: 'get',
          url,
          responseType: 'arraybuffer'
        }).then(data => {
          resolve(data.data)
        }).catch(error => {
          reject(error.toString())
        })
      })
    };
// 批量下载
const handleBatchDownload = async (selectImgList) => {
      const data = selectImgList;
      const zip = new JSZip()
      const cache = {}
      const promises = []
      await data.forEach(item => {
          const promise =  getFile(item).then(data => { // 下载文件, 并存成ArrayBuffer对象
          const arr_name = item.split("/");
          let file_name = arr_name[arr_name.length - 1] // 获取文件名
          // if (file_name.indexOf('.png') == -1) {
         //    file_name = file_name + '.png'
         // }
          zip.file(file_name, data, {
            binary: true
          }) // 逐个添加文件
          cache[file_name] = data
        })
        promises.push(promise)
      })
      Promise.all(promises).then(() => {
        zip.generateAsync({
          type: "blob"
        }).then(content => { // 生成二进制流
          FileSaver.saveAs(content, "photo.zip") // 利用file-saver保存文件
        })
      })
    
};

const listPic = [
  "http://127.0.0.1:5500/img/1.png",
  "http://127.0.0.1:5500/img/2.png",
]

handleBatchDownload(listPic)
```
