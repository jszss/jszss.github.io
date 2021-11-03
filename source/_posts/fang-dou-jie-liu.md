---
title: '防抖-节流'
date: 2020-11-17 19:02:33
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
#  防抖
### 在当前点击完成后，我们等wait这么长的时间，看是否还会触发第二次，如果没有触发第二次，属于非频繁操作，我们直接执行想要执行的函数func：如果触发了第二次，则以前的不算了，从当前这次再开始等待...
```js
/*
      防抖:
        @params:
          func[function]:最后要触发执行的函数
          wait[number]:频繁设定的界限
          immediate[boolean]:默认多次操作，我们识别的是最后一次，但是immediate=true，让其识别第一次
        @return
          可以被调用执行的函数
 */
function debounce(func,wait = 300,immediate = false){
      let timer = null;
      return function anonymous(...params){
        let now = immediate && !timer;

        //每次点击都把之前设置的定时器清除掉
        clearInterval(timer)
        //重新设置一个新的定时器监听wait事件内是否触发第二次
        timer = setTimeout(() => {
          timer = null;//垃圾回收机制
          //wait这么久的等待中，没有触发第二次
          !immediate ? func.call(this,...params) : null;
        }, wait);

        //如果是立即执行
        now ? func.call(this,...params) : null;
      }
}
```
## 节流
### 函数节流：在一段频繁操作中，可以触发多次，但是触发的频率由自己指定
```js
/*
      @params:
          func[function]:最后要触发执行的函数
          wait[number]:触发的频率
        @return
          可以被调用执行的函数
*/
function throttle(func,wait = 300){
      let timer = null,
          previous = 0;//记录上一次操作时间
      return function anonymouse(...params){
        let now = new Date(),//记录当前时间
            remaining = wait - (now - previous);//记录还差多久达到我们一次触发的频率
        if(remaining <= 0){
          //两次操作的间隔时间已经超过wait了
          window.clearInterval(timer);
          timer = null;
          previous = now;
          func.call(this,...params);
        }else if(!timer){
          //两次操作的间隔时间还不符合触发的频率
          timer = setTimeout(() => {
            timer = null;
            previous = new Date();
            func.call(this,...params);
          }, remaining);
        }
      }
}

```