---
title: 'event.currentTarget与event.target的区别'
date: 2019-09-10 11:55:21
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## target、currentTarget的区别？
currentTarget当前所绑定事件的元素

target当前被点击的元素
### 
>event.currentTarget 获取到的是发起事件的标签元素 event.target 获取的是触发事件的标签元素
### event对象的常用属性和方法：
* event.preventDefault();//阻止默认事件
* event.isDefaultPrevented();//检测 event.preventDefault() 是否被调用过
* event.currentTarget;//发起事件的标签
* event.target;//触发事件的标签
* event.type//事件的类型
* event.pageX;event.pageY //相对于文件的左侧和顶部边缘的位置
* event.which;//针对键盘和鼠标事件，确定底按的是哪个键或按钮 常用在keydown事件中
* event.timeStamp;//事件触发时与事件创建之间的时间间隔
* event.stopPropagation(); //阻止事件的冒泡