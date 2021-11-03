---
title: 'vue jsx directives 指令'
date: 2020-12-22 14:20:13
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## v-action:edit
```js
           customRender: (text, record) => {
             const directives = [{ name: 'action', value: null, arg: 'edit' }]
             return (
               <router-link {...{ directives }} to={{ name: 'operation_news_edit', params: { id: record.id } }}>
                 {text}
               </router-link>
             )
           }
```
```js
const directives = [
  { name: 'my-directive', value: 123, modifiers: { stop: true },arg: 'edit' }
]
return <div {...{ directives }}/>
```