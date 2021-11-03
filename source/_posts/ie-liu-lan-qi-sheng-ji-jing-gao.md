---
title: 'ie浏览器升级警告'
date: 2021-04-02 08:43:04
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## ie10及以下识别
```js
// ie10及更旧版提示
<script>/*@cc_on alert('警告：你正在使用IE浏览器，请升级浏览器或者更换其他高速浏览器；点击确定继续。') @*/</script> 
```
## ie9及以下识别
```js 
// ie9及更旧版提示
<!--[if lte IE 9]> <script> 脚本 </script>  <![endif]-->
```
## ie浏览器（包括ie11）
```js 
if(!!window.ActiveXObject || "ActiveXObject" in window){
      alert('警告：你正在使用IE浏览器，请升级浏览器或者更换其他高速浏览器；点击确定继续。')
}
```
##其他
```js
        /* IE条件编译检测浏览器是否是IE并且取得IE版本号
         * 不使用navigator.userAgent获取IE版本号避免误判 
        */
        var IEVersion = 0;
        /*@cc_on@*/
        /*@
                IEVersion = @_jscript_version;
        @*/
        if(IEVersion > 0){
                if(IEVersion < 11){
                        alert('IE 11已经发布多年，不要再用祖传的IE' + IEVersion + '了！');
                }
        }else{
                alert('当前浏览器不是IE内核浏览器。');
        }
```