---
title: 'CSS实现六边形图片展示效果'
date: 2019-02-04 11:57:21
tags: [CSS3]
published: true
hideInList: false
feature: 
---
``` html
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>CSS3 实现六边形图片展示效果</title>
    <style type="text/css">
        body,
        div,
        img,
        ul,
        li {
            margin: 0;
            padding: 0;
        }

        body {
            font-size: 12px;
            background-color: #DDD;
            min-width: 1200px;
        }

        ul,
        ul li {
            list-style: none;
        }

        .boxF,
        .boxS,
        .boxT,
        .overlay {
            width: 200px;
            height: 250px;
            overflow: hidden;
        }

        .boxF,
        .boxS {
            visibility: hidden;
        }

        .boxF {
            transform: rotate(120deg);
            float: left;
            margin-left: 10px;
            -ms-transform: rotate(120deg);
            -moz-transform: rotate(120deg);
            -webkit-transform: rotate(120deg);
        }

        .boxS {
            transform: rotate(-60deg);
            -ms-transform: rotate(-60deg);
            -moz-transform: rotate(-60deg);
            -webkit-transform: rotate(-60deg);
        }

        .boxT {
            transform: rotate(-60deg);
            background: no-repeat 50% center;
            background-size: 125% auto;
            -ms-transform: rotate(-60deg);
            -moz-transform: rotate(-60deg);
            -webkit-transform: rotate(-60deg);
            visibility: visible;
        }
    </style>
</head>

<body>
    <div class="boxF">
        <div class="boxS">
            <div class="boxT" style="background-image: url(./images/pic.jpg);"></div>
        </div>
    </div>
</body>

</html>
```