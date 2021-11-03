---
title: 'CSS单行文字居中，多行文字居左的实现方式'
date: 2019-12-25 15:42:11
tags: []
published: true
hideInList: false
feature: 
---
## CSS单行文字居中，多行文字居左的实现方式
### 1.父级`text-align:center`，子级`inline-block+text-align:left`

```css
.content{
    text-align: center;
}
.text{
    display: inline-block;
    text-align: left;
}
```
### 2.`width:fit-content` + `margin:auto`
块级block元素可以在设置宽度后直接通过margin:0 auto来实现居中，但是必须指明宽度，不然就水平填充了，这两者的关系很微妙，有没有什么办法能够让块级block元素的宽度像inline-block元素跟随内部元素呢？
>width:fit-content可以实现元素收缩效果的同时，保持原本的block水平状态，于是，就可以直接使用margin:auto实现元素向内自适应同时的居中效果了。
```html
<p class="text">这段文字能不能这样判断一下，当文字不足一行时，让它居中显示，当文字超过一行就让它居左</p>
```
```css
.text{
    width: fit-content;
    width: -moz-fit-content;//火狐需要-moz-前缀
    margin: 0 auto;
}
```