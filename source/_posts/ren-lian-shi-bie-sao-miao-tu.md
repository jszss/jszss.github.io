---
title: '🙅人脸识别 -- 扫描图'
date: 2019-09-12 12:30:59
tags: [css 特效]
published: true
hideInList: false
feature: 
---
```html
<img src='https://secure.gravatar.com/avatar/9a7560a750923bc17df191f8f5f511da?d=identicon' />
<div></div>
```
```css
*{ margin:0 }
div{
	width: 200px;
  position: absolute;
  left:0;
  top:0;
  z-index:2;
	height: 200px;
	background: linear-gradient(#03A9F4,#03A9F4), 
 linear-gradient(90deg, #ffffff33 1px,transparent 0,transparent 19px),
 linear-gradient(#ffffff33 1px,transparent 0,transparent 19px),
 linear-gradient(transparent, #2196f387);
	background-size:100% 1.5%, 10% 100%,100% 10%, 100% 100%;
	background-repeat: no-repeat,repeat,repeat,no-repeat;
	background-position: 0 0,0 0, 0 0, 0 0;
	clip-path: polygon(0% 0%, 100% 0%, 100% 1.5%, 0% 1.5%);
	animation: move 2s infinite linear;
}

img{
  width: 200px;
	 height: 200px;
}
@keyframes move{
	to{
		background-position: 0 100%,0 0, 0 0, 0 0;
		clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
	}
```

[参考](https://codepen.io/laoyao/pen/MWgGzWb)
![](http://zssjs.coding.me/post-images/1568262853871.gif)