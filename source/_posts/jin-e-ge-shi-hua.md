---
title: '金额格式化'
date: 2020-07-17 09:39:17
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Static Template</title>
  </head>
  <body>
    <h1>金额格式化</h1>
    <h2></h2>
    <script>
      function formatNum(val) {
        // 金额格式化
        var rt = null;

        if (val <= 999) {
          rt = { val: val.toString().substr(0, 3), unit: "" };
          substrNum(rt);
        } else if (val < 9999999) {
          val = Math.round(val / 1000) / 10;
          console.log(val);
          rt = { val: val, unit: "万" };
          substrNum(rt);
        } else if (val < 99999999) {
          val = Math.round(val / 1000000) / 10;
          rt = { val: val, unit: "千万" };
          substrNum(rt);
        } else if (val < 99999999999) {
          val = Math.round(val / 10000000) / 10;
          rt = { val: val, unit: "亿" };
          substrNum(rt);
        } else {
          val = Math.round(val / 10000000) / 10;
          rt = { val: val, unit: "亿" };
        }
        return rt;
      }

      function substrNum(rt) {
        rt.val = rt.val.toString().substr(0, 3);
        console.log(rt.val);
        console.log(rt.val.charAt(rt.val.length - 1));
        if (rt.val.charAt(rt.val.length - 1) == ".") {
          //判断末尾是否 "."
          rt.val = rt.val.substr(0, 2);
        }
      }
      var result = formatNum(51696991);
      console.log(result);
      document.querySelector("h2").innerHTML = result.val + result.unit;
    </script>
  </body>
</html>

```