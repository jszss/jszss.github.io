---
title: '移动端触摸事件'
date: 2020-10-16 09:04:59
tags: []
published: false
hideInList: false
feature: 
isTop: false
---
①touchstart：当手指触碰到屏幕的时候触发
②touchmove：当手指在屏幕上滑动的时候触发
③touchend：当手指离开屏幕的时候时候触发
④touchcancel事件：当系统停止跟踪触摸的时候触发(这个事件很少会用，一般不做深入研究)。 电话接入或者弹出信息等其他事件切入
event：

touches：表示当前跟踪的触摸操作的touch对象的数组。
targetTouches：特定于事件目标的Touch对象的数组。
changeTouches：表示自上次触摸以来发生了什么改变的Touch对象的数组。

每个touch对象包含的属性

clientX：触摸目标在视口中的x坐标。
clientY：触摸目标在视口中的y坐标。
identifier：标识触摸的唯一ID。
pageX：触摸目标在页面中的x坐标。
pageY：触摸目标在页面中的y坐标。
screenX：触摸目标在屏幕中的x坐标。
screenY：触摸目标在屏幕中的y坐标。
target：触目的DOM节点目标。

作者：信心
链接：https://juejin.im/post/6844903673009553416
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。