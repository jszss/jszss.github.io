---
title: "⏳CountDown 倒计时"
date: 2019-09-17 11:43:16
tags: []
published: true
hideInList: false
feature:
---

[CountDown](https://github.com/any86/useful-utils/blob/master/docs/CountDown.md)

## 倒计时小例子

```html
<div id="box"></div>
<script>
  //new Date()获取客户端本地当前时间（不能拿它做重要依据，因为用户可以随意修改）
  /*
   * 倒计时抢购需要从服务器获取当前时间  AJAX
   *    问题：时间差（从服务器把时间给客户端，到客户端获取到这个信息，中间经历的时间就是时间差，而时间差是不可避免的，我们应尽可能减少这个误差）
   *    - 从响应头获取时间（AJAX异步）
   *    - 基于HEAD请求（只获取响应头信息）
   */
  let target = new Date("2019/09/14 13:27:00"),
    now = null,
    timer = null;

  //=>从服务器获取时间：获取到时间后再做其他的事情
  function func(callback) {
    let xhr = new XMLHttpRequest();
    xhr.open("HEAD", "json/data.json", true);
    xhr.onreadystatechange = function () {
      if (!/^(2|3)\d{2}$/.test(xhr.status)) return;
      if (xhr.readyState === 2) {
        now = new Date(xhr.getResponseHeader("Date"));
        callback && callback();
      }
    };
    xhr.send(null);
  }

  //=>开启倒计时模式
  function computed() {
    let spanTime = target - now;
    if (spanTime <= 0) {
      //=>到抢购时间：结束定时器
      clearInterval(timer);
      timer = null;
      box.innerHTML = "开抢~~";
      return;
    }
    let hours = Math.floor(spanTime / (60 * 60 * 1000));
    spanTime -= hours * 60 * 60 * 1000;
    let minutes = Math.floor(spanTime / (60 * 1000));
    spanTime -= minutes * 60 * 1000;
    let seconds = Math.floor(spanTime / 1000);
    box.innerHTML = `距离抢购还剩 ${hours < 10 ? "0" + hours : hours}:${
      minutes < 10 ? "0" + minutes : minutes
    }:${seconds < 10 ? "0" + seconds : seconds}`;

    //=>每一次计算完，我们需要让NOW在原来的基础上加上一秒（第一次从服务器获取到时间，后期直接基于这个时间自己加即可，不要每隔一秒重新从服务器拿）
    now = new Date(now.getTime() + 1000);
  }
  func(() => {
    //=>已经从服务器获取时间了
    computed();
    timer = setInterval(computed, 1000);
  });
</script>
```
