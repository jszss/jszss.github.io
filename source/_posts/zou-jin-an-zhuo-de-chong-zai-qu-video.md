---
title: '走进安卓的重灾区----video'
date: 2019-09-17 12:01:42
tags: []
published: true
hideInList: false
feature: 
---
[走进安卓的重灾区----video]([走进安卓的重灾区----video](https://juejin.im/post/5d8046345188253849631aa6))
>在ios上会自动全屏播放，需要在video标签上设置一个属性 webkit-playsinline，ios10及以上版本属性名改成 playsinline。安卓上，无法自动播放，必须手动触发视频的播放。调用任何方法都没用，据说这个为了帮用户省流量而设定的。但是安卓在首次触发之后，再次触发可以通过调用 .play 来触发播放视频。因此做兼容的时候可以设一个判断是否首次播放的标志来处理。 