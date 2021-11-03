---
title: '给Canvas录制一个视频'
date: 2019-09-19 10:31:11
tags: [canvas]
published: true
hideInList: false
feature: 
---
[给Canvas录制一个视频](https://juejin.im/post/5d81f689f265da039b24cf56)
### Step 1：初始化录屏实例
```
const chunks = new Set()
function createRecord () {
  const mediaStream = $canvas.captureStream(10) // 设置帧频率(FPS)
  mediaRecord = new MediaRecorder(mediaStream, {
      videoBitsPerSecond: 8500000
  })
  mediaRecord.ondataavailable = (e) => { // 接收数据
      chunks.add(e.data)
  }
}
```
### Step 2：控制录屏
```
mediaRecord.start()  // 开始录屏
this.mediaRecord.stop() // 结束录屏
```
### Step 3：下载录屏
```
const videoBlob = new Blob(chunks, { 'type' : 'video/mp4' })
videoUrl = window.URL.createObjectURL(videoBlob)
```
chunks是元素为Blob类型的列表，可能只有一个元素，可能是多个元素，取决于start()中是否设置了timeslice，将这些片段blob重新封装为一个完整的blob数据，并且可以指定数据类型。然后根据blob数据生成一条blob URL。关于blob和createObjectURL的介绍可以移步[这里](https://juejin.im/post/5d2d9fbff265da1bb67a4c1f#heading-14)。