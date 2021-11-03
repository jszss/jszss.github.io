---
title: '🌈彩虹 Loading'
date: 2019-10-09 11:51:08
tags: []
published: true
hideInList: false
feature: 
---
# [codepen](https://codepen.io/krischan77/pen/OJJVbxJ)
> https://cdpn.io/boomboom/v2/index.html?key=iFrameKey-5647e640-e7d1-ee18-99d4-c8d3837275bd
## HTML
```html
<h1><i>斯人若彩虹，遇上方知有</i></h1>
<div class="rainbow-box">
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
	<div class="rainbow-arc">
		<div class="rainbow-arc-main"></div>
	</div>
</div>
```
## CSS
```css
html,
body,
div {
	margin: 0;
	padding: 0;
}
html,
body {
	background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
	width: 100%;
	height: 100%;
}
h1 {
	text-align: center;
	line-height: 3;
	font-weight: 700;
	-webkit-text-fill-color: transparent;
	background-color: hsla(0, 100%, 60%, .8);
	-webkit-background-clip: text;
	animation: textColorRotate 5s linear infinite;
	letter-spacing:2px
}
.rainbow-box {
	position: absolute;
	top: 100px;
	right: 0;
	left: 0;
	margin: auto;
	width: 200px;
	height: 200px;
}
.rainbow-arc {
	position: absolute;
	left: 0;
	top: 0;
	width: 200px;
	height: 100px;
	box-sizing: border-box;
	overflow: hidden;
	transform-origin: 50% 100%;
/* 	animation: rainbowMove 3s cubic-bezier(.58,-0.57,.5,1.66) infinite; */
}
.rainbow-arc-main {
	border: 4px solid transparent;
	border-radius: 100%;
	box-sizing: border-box;
	height: 150px;
	left: 0;
	margin: 0 auto;
	position: absolute;
	right: 0;
	top: 0;
	width: 150px;
}
.rainbow-arc:nth-child(1) { 
	animation-delay: -50ms;
}
.rainbow-arc:nth-child(2) {
	animation-delay: -100ms;
}
.rainbow-arc:nth-child(3) {
	animation-delay: -150ms;
}
.rainbow-arc:nth-child(4) {
	animation-delay: -200ms;
}
.rainbow-arc:nth-child(5) {
	animation-delay: -250ms;
}
.rainbow-arc:nth-child(6) {
	animation-delay: -300ms;
}
.rainbow-arc:nth-child(7) {
	animation-delay: -350ms;
}

.rainbow-arc:nth-child(1) .rainbow-arc-main {
	border-color: hsla(0, 100%, 60%, .8);
	height: 200px;
	width: 200px;
	top: 10px;
}
.rainbow-arc:nth-child(2) .rainbow-arc-main {
	border-color: hsla(30, 100%, 60%, .8);
	height: 180px;
	width: 180px;
	top: 20px;
}
.rainbow-arc:nth-child(3) .rainbow-arc-main {
	border-color: hsla(60, 100%, 60%, .8);
	height: 160px;
	width: 160px;
	top: 30px;
}
.rainbow-arc:nth-child(4) .rainbow-arc-main {
	border-color: hsla(90, 100%, 60%, .8);
	height: 140px;
	width: 140px;
	top: 40px;
}
.rainbow-arc:nth-child(5) .rainbow-arc-main {
	border-color: hsla(120, 100%, 60%, .8);
	height: 120px;
	width: 120px;
	top: 50px;
}
.rainbow-arc:nth-child(6) .rainbow-arc-main {
	border-color: hsla(150, 100%, 60%, .8);
	height: 100px;
	width: 100px;
	top: 60px;
}
.rainbow-arc:nth-child(7) .rainbow-arc-main {
	border-color: hsla(180, 100%, 60%, .8);
	height: 80px;
	width: 80px;
	top: 70px;
}

@keyframes textColorRotate {
	from {
		filter: hue-rotate(0deg);
	}
	to {
		filter: hue-rotate(360deg);
	}
}
@keyframes rainbowMove {
	0%, 15% {
		transform: rotate(0);
	}
	100% {
		transform: rotate(360deg);
	}
}
```