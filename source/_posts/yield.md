---
title: 'yield'
date: 2021-07-27 22:06:11
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
function* search(node){ 
    if(!node){
         return 
         };  
         yield node; 
         yield* search(node.firstChild); 
         yield* search(node.nextSibling); 
}
for (let node of search(document)){ 
    if(node.localName === 'title')
    { console.log(node.textContent());
    break; 
    } 
}
```