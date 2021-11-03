---
title: 'prerender-spa-plugin'
date: 2020-04-10 11:59:50
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## prerender-spa-plugin
### webpack配置
```js
        new PrerenderSPAPlugin({
            staticDir: path.join(__dirname, '../dist'),
            //需要进行渲染的的页面路由
            routes: ['/', '/aaa'],
            renderer: new Renderer({
                // 触发渲染的时间，用于获取数据后再保存渲染结果
                renderAfterTime: 10000,
                // 是否打开浏览器，false 是打开。可用于 debug 检查渲染结果
                headless: false,
                // 在项目的main.js入口中使用 `document.dispatchEvent(new Event('render-event'))` 
                renderAfterDocumentEvent: 'render-event', // render-event: 声明的方法名 
            })
        })
        })

```
### main.js配置
```js
new Vue({
    el: '#app',
    router,
    components: { App },
    template: '<App/>',
    render: h => h(App),
    mounted() {
        document.dispatchEvent(new Event('render-event'))
    },
})

```
https://juejin.im/post/5e8bedb9f265da47a741253f