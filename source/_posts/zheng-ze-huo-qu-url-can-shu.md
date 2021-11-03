---
title: '正则获取url参数'
date: 2019-09-10 11:46:00
tags: []
published: true
hideInList: false
feature: 
---
``` javascript
function query(url){
  let reg=/([^=?&]+)=([^=?&]+)/g,
  obj={};
  url.replace(reg,function(){
    obj[arguments[1]]=arguments[2]
  })
  return obj
}

query(location.href)
```