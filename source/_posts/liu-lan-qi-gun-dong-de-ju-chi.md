---
title: '浏览器滚动的距离'
date: 2020-07-31 09:37:28
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
浏览器内的内容即然可以滚动，那么我们就可以获取到浏览器滚动的距离思考一个问题？浏览器真的滚动了吗？其实我们的浏览器是没有滚动的，是一直在那里滚动的是什么？是我们的页面所以说，其实浏览器没有动，只不过是页面向上走了所以，这个已经不能单纯的算是浏览器的内容了，而是我们页面的内容所以不是在用 window 对象了，而是使用 document 对象

```js
window.onscroll = function () {
 console.log(document.body.scrollTop)
 console.log(document.documentElement.scrollTop)
  console.log(window.pageYOffset)
}
```
两个都是获取页面向上滚动的距离区别：IE 浏览器没有 DOCTYPE 声明的时候，用这两个都行有 DOCTYPE 声明的时候，只能用 document.documentElement.scrollTop Chrome 和 FireFox没有 DOCTYPE 声明的时候，用 document.body.scrollTop有 DOCTYPE 声明的时候，用 document.documentElement.scrollTop Safari两个都不用，使用一个单独的方法 window.pageYOffset
