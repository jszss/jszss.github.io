---
title: websocket心跳检测机制
author: zss
date: 2021-10-28 21:34:52
tags: [websocket]
---

<!-- more -->

```js
var ws;
var tt;
var lockReconnnet=false;
var wxUrl='https://api/v1/1';
function createWebSocket(url){
  try{
  ws=new WebSocket(url);
  init();
  }catch(){
  reconnect(url);
  }
}
function init(){
  ws.onclose=function(){
    console.log("websocket关闭了");
    reconnect(url);
  }
  ws.onopen=function(){
    console.log("websocket打开了");
    heartCheck(url);
  }
  ws.onerror=function(){
    console.log("websocket报错了");
    reconnect(url);
  }
  ws.onmessage=function(){
    //能收到消息说明链接正常
    heartCheck(url);
  }
}
function reconnect(url){
//如果连接被锁定了，就说明当前的链接是正常的
  if(lockReconnnet){
    return;
  }
  lockReconnnet=true;
  //清除定时器
  tt&&clearTimeOut(tt);
  tt=setTimeOut(()=>{
   createWebSocket(url);
   lockReconnnet=false;
  },4000)
}
var heartCheck={
   timeout:3000,
   timeOutObj:null,
   serverTimeOutObj:null,
   start:function(){
     var self=this;
     this.timeOutObj&&clearTimeOut(this.timeOutObj);
     this.serverTimeOutObj&&clearTimeOut(this.serverTimeOutObj)
     this.timeOutObj=setTimeOut(()=>{
        ws.send("发送数据");
        self.serverTimeOutObj=setTimeOut(()=>{
          ws.onclose();
        },self.timeout)
     },self.timeout)
   }
}
createWebSocket(wsUrl);

```
