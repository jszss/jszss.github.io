---
title: 'fileReader 图片预览'
date: 2020-04-20 14:43:06
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
File API使得我们在浏览器端可以访问文件的数据,比如预览文件,获取文件信息(比如文件名,文件内容,文件大小等), 并且可以在前端实现文件下载(可以借助canvas和 window.URL.revokeObjectURL的一些能力).当然我们还可以实现拖拽上传文件这样高用户体验的操作.接下来我们来看看几个实际例子.

```js
function previewFiles(files, previewBox) {
    for (var i = 0; i < files.length; i++) {
      var file = files[i];
      var imageType = /^image\//;
      
      if (!imageType.test(file.type)) {
        continue;
      }
      
      var img = document.createElement("img");
      previewBox.appendChild(img); // 假设"preview"就是用来显示内容的div
      
      var reader = new FileReader();
      reader.onload = (function(imgEl) { 
        return function(e) { imgEl.src = e.target.result; }; 
      })(img);
      reader.readAsDataURL(file);
    }
  }

```