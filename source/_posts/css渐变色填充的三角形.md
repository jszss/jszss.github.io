---
title: css渐变色填充的三角形
author: zss
date: 2022-01-09 17:54:42
tags:
---

```html
<div class="triangle"></div>
```

```css
.triangle {
  position: relative;
  display: inline-block;
  width: 30px;
  height: 16px;
  background-image: linear-gradient(#FFFFFF, #CE070A80);
}

.triangle:before {
  position: absolute;
  content: "";
  width: 0;
  height: 0;
  border-right: 15px solid transparent;
  border-bottom: 16px solid #FFFFFF;
}

.triangle:after {
  position: absolute;
  content: "";
  /* 使绘制的三角形位于矩形右侧 */
  right: 0; 
  width: 0;
  height: 0;
  border-left: 15px solid transparent;
  border-bottom: 16px solid #FFFFFF;
}
```