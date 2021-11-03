---
title: 'Vue -- inheritAttrs'
date: 2019-12-10 16:01:11
tags: []
published: true
hideInList: false
feature: 
---
## 子组件替换/合并已有的特性
在Vue中对于绝大多数特性来说，从外部提供给组件的值会替换掉组件内部设置好的值。所以如果传入type="text"就会替换掉 type="date"并把它破坏！庆幸的是，class和 style特性会稍微智能一些，即两边的值会被合并起来，从而得到最终的值，举个例子：

```html
<div id="app">
  <base-input type="text" class="out"></base-input>
</div>
```
```js
Vue.component('base-input', {
  template: `<input type="date" placeholder="replace" class="default">`
})
new Vue({
  el: '#app',
})
```
在上例中input的type值为date，class为deafault，在使用子组件时，向`子组件`中传入`type="text" class="out"`，此时input的type值会被替换为text，class值会被合并为"default out"，那么如果想要禁用属性继承怎么办呢？可以在组件的选项中设置`inheritAttrs: false`，举个例子：

```js
Vue.component('base-input', {
  inheritAttrs: false,
  template: `<input type="date" placeholder="replace" class="default">`
})
```
但是`inheritAttrs: false`选项不会影响style和class的绑定，因此style和class还是会合并