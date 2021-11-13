---
title: "使用transform描绘1px边框"
date: 2019-10-10 17:11:13
tags: [scss]
published: true
hideInList: false
feature:
---

分辨率比较低的屏幕下显示 1px 的边框会显得模糊，通过::before 或::after 和 transform 模拟细腻的 1px 边框

```scss
.onepx-border {
  margin-top: 10px;
  width: 200px;
  height: 80px;
  cursor: pointer;
  line-height: 80px;
  text-align: center;
  font-weight: bold;
  font-size: 50px;
  color: $red;
  &:first-child {
    margin-top: 0;
  }
}
.normal {
  border: 1px solid $red;
}
.thin {
  position: relative;
  &::after {
    position: absolute;
    left: 0;
    top: 0;
    width: 200%;
    height: 200%;
    border: 1px solid $red;
    content: "";
    transform: scale(0.5);
    transform-origin: left top;
  }
}
```
