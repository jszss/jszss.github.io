---
title: flex布局 justify-content:space-between 最后一行左对齐
date: 2021-10-14 10:22:00
tags:
---

## [在线地址](demo/flex-last-line.html)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>flex布局最后一行列表左对齐</title>
  </head>
  <body>
    <br />
    <h2 class="tac">flex布局最后一行列表左对齐</h2>
    <br />
    <h3 class="tac">(可点列表击删除最后一个选项)</h3>
    <br />
    <h4 class="tac">一行3列的情况</h4>
    <ul class="list list1">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
    <h4 class="tac">一行4列的情况</h4>
    <ul class="list list2">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <!-- <li></li> -->
    </ul>
    <h4 class="tac">一行5列的情况</h4>
    <ul class="list list3">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
    <h4 class="tac">一行列数不固定的情况</h4>
    <ul class="list list4">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </body>
</html>
<script>
  [].slice.call(document.querySelectorAll("li")).forEach(function (list) {
    list.onclick = function () {
      this.parentNode.removeChild(this);
    };
  });
</script>
<style>
  * {
    margin: 0;
    padding: 0;
  }
  :root {
    --width1: 30%;
    --width2: 24%;
    --width3: 18%;
    --width4: 80px;
  }
  .tac {
    text-align: center;
  }
  .list {
    padding: 10px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .list li {
    height: 80px;
    list-style: none;
    background: deepskyblue;
    margin-bottom: 10px;
  }

  .list1 li {
    width: var(--width1);
  }
  .list1 li:last-child:nth-child(3n + 2) {
    background: hotpink;
    margin-right: calc((100% - var(--width1)) / 2);
  }

  .list2 li {
    width: var(--width2);
  }
  .list2 li:last-child:nth-child(4n + 2) {
    background: hotpink;
    margin-right: calc((100% - var(--width2)) / 3 * 2);
  }
  .list2 li:last-child:nth-child(4n + 3) {
    background: burlywood;
    margin-right: calc((100% - var(--width2)) / 3 * 1);
  }

  .list3 li {
    width: var(--width3);
  }
  .list3 li:last-child:nth-child(5n + 2) {
    background: hotpink;
    margin-right: calc((100% - var(--width3)) / 4 * 3);
  }
  .list3 li:last-child:nth-child(5n + 3) {
    background: burlywood;
    margin-right: calc((100% - var(--width3)) / 4 * 2);
  }
  .list3 li:last-child:nth-child(5n + 4) {
    background: mediumseagreen;
    margin-right: calc((100% - var(--width3)) / 4 * 1);
  }

  .list4 {
    display: grid;
    grid-template-columns: repeat(auto-fill, var(--width4));
    grid-gap: 10px;
  }
  .list4 li {
    width: var(--width4);
  }
</style>
```
https://www.jb51.net/css/708614.html
https://blog.csdn.net/lbchenxy/article/details/100654731