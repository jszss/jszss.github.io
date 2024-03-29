---
title: "元素水平垂直居 -- 使用表格居中"
date: 2019-09-27 17:49:40
tags: []
published: true
hideInList: false
feature:
---

## 使用 display：table（作为 flexbox 的替代）使子元素在其父元素中水平垂直居。

```html
<div class="container">
  <div class="center"><span>Centered content</span></div>
</div>
```

```css
.container {
  border: 1px solid #333;
  height: 250px;
  width: 250px;
}
.center {
  display: table;
  height: 100%;
  width: 100%;
}
.center > span {
  display: table-cell;
  text-align: center;
  vertical-align: middle;
}
```

### [例子](https://codepen.io/bigerfe-com/pen/JjPYqYg)

> display：table 使.center 元素的行为类似于 HTML 元素。
> 设置.center 的宽高为 100%，使其填满父元素。
> display：table-cell, 设置'.center > span'的 table-cell 允许元素表现得像 HTML 元素。
> text-align: center 使子元素水平居中。
> vertical-align: middle 使子元素垂直居中。

### 外部父级必须有固定的宽高。
