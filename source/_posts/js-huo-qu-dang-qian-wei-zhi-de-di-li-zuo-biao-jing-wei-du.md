---
title: '✈JS 获取当前位置的地理坐标（经纬度）'
date: 2019-09-10 12:03:19
tags: []
published: true
hideInList: false
feature: 
---
使用getCurrentPosition方法实时获取当前Geolocation信息
<!-- more -->

``` javascript
navigator.geolocation.getCurrentPosition(
        function (position) {
            //获取地理位置成功时所做的处理
    },
        function (error) {
            //获取地理位置信息失败时所做的处理
    }, //以下是可选属性
        {
            enableHighAccuracy: true,//是否要求高精度的地理位置信息
            timeout: 1000,//对地理位置信息的获取操作做超时限制，如果再该事件内未获取到地理位置信息，将返回错误
            maximumAge:60*1000//设置缓存有效时间，在该时间段内，获取的地理位置信息还是设置此时间段之前的那次获得的信息，超过这段时间缓存的位置信息会被废弃
        })
```
[https://www.cnblogs.com/qikeyishu/p/7708116.html](https://www.cnblogs.com/qikeyishu/p/7708116.html)
```html
<!Doctype html>
<html>
<head>
    <title></title>
    <meta charset="utf-8" />
    <meta name="keywords" content="关键词"/>
    <meta name="description" content="描述"/>
    <meta name="author" content="奇客艺术"/>
</head>
<body>
<p id="GeoDisplay"></p>
<script>
    Geolocation();//执行Geolocation()函数
    setInterval(Geolocation,100);//设置定时器，100ms执行一次Geolocation();实现实时获取
    function getElem(id) {
        return typeof id === 'string' ? document.getElementById(id):id;//typeof表示变量id的类型为字符串类型
    }
    var GetID = getElem("GeoDisplay");
    function showMap(lat,lon) {//自定义了一个在浏览器上显示地理信息的函数
    var str = "您当前位置的维度："+lat+"，经度："+lon;
        GetID.innerHTML = str;
    }
    function Geolocation() {
        if(navigator.geolocation){
            navigator.geolocation.getCurrentPosition(
                function (position) {//传入了对象position
                    showMap(position.coords.latitude,position.coords.longitude);
                },
                function (err) {//传入了error对象
                    GetID.innerHTML = err.code + '\n'+err.message;//Firefox3.6以上不支持error对象的message属性
                    //error对象的code属性有如下属性值:
                    //PERMISSION_DENIED(1):(permission_denied):用户单机信息条上的“不共享”按钮或直接拒绝被获取位置信息
                    //POSITION_UNAVAILABLE(2):(position_unavailable):(position_unavailable)网络不可用或者无法连接到获取位置信息的卫星
                    //TIMEOUT(3):(timeout)网络可用但在计算机用户的位置上花费过长时间
                    //UNKNOWN_ERROR(0):(unknown_error)发生其他未知错误
                })
            }else {
                GetID.innerHTML = "您当前使用的浏览器不支持地理定位服务";
        }
    }
</script>
</body>
</html>
```