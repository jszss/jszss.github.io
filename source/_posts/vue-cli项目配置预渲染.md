---
title: vue-cli项目配置预渲染
author: zss
date: 2021-10-28 20:16:43
tags: [ssr, 预渲染]
---

## vue-cli2.0 版本

### webpack.prod.conf.js 增加

> router.js 中设置路由模式 `mode: "history"`

```js
// npm install prerender-spa-plugin --save

const path = require("path");
const PrerenderSPAPlugin = require("prerender-spa-plugin"); // 引入插件
const Renderer = PrerenderSPAPlugin.PuppeteerRenderer;

plugins: [
  // 配置PrerenderSPAPlugin
  new PrerenderSPAPlugin({
    // 生成文件的路径，也可以与webpakc打包的一致。
    staticDir: path.join(__dirname, "../dist"),

    // 对应自己的路由文件，比如index有参数，就需要写成 /index/param1。
    routes: ["/", "/report", "/genius", "/index/param1"],
    // 一定要写，如果没有配置这段，也不会进行预编译
    renderer: new Renderer({
      inject: {
        foo: "bar",
      },
      headless: false,
      // 在 main.js 中 document.dispatchEvent(new Event('render-event'))，两者的事件名称要对应上。
      renderAfterDocumentEvent: "render-event",
    }),
  }),
];
```

### 在 main.js 中添加

```js
new Vue({
  el: "#pingce",
  router,
  store,
  components: { App },
  template: "<App/>",
  // 添加mounted，不然不会执行预编译
  mounted() {
    document.dispatchEvent(new Event("render-event"));
  },
});
```

## vue-cli3.0 版本

### vue-config.js 中增加

> router.js 中设置路由模式 `mode: "history"`

```js
// npm install prerender-spa-plugin --save

const PrerenderSPAPlugin = require("prerender-spa-plugin"); // 引入插件
const Renderer = PrerenderSPAPlugin.PuppeteerRenderer;
const path = require("path");
module.exports = {
  configureWebpack: (config) => {
    if (process.env.NODE_ENV !== "production") return;
    return {
      plugins: [
        new PrerenderSPAPlugin({
          // 生成文件的路径，也可以与webpakc打包的一致。
          // 这个目录只能有一级，如果目录层次大于一级，在生成的时候不会有任何错误提示，在预渲染的时候只会卡着不动。
          staticDir: path.join(__dirname, "dist"),
          // 对应自己的路由文件，比如about有参数，就需要写成 /about/param1。
          routes: ["/", "/product", "/about"],
          // 必须配置不然不会进行预编译
          renderer: new Renderer({
            inject: {
              foo: "bar",
            },
            headless: false,
            // 在 main.js 中 document.dispatchEvent(new Event('render-event'))，两者的事件名称要对应上。
            renderAfterDocumentEvent: "render-event",
          }),
        }),
      ],
    };
  },
};
```

### 在 main.js 中添加

```js
new Vue({
  router,
  store,
  render: (h) => h(App),
  // 与 vue-config.js的renderAfterDocumentEvent: 'render-event'名字一定要对应上
  mounted() {
    document.dispatchEvent(new Event("render-event"));
  },
}).$mount("#app");
```

## 总结

1. 路由的模式最好使用 history 模式，不使用也可以运行生成文件，但是查看每个 index.html 文件内容师一样的。
2. 在 3.0 中和 2.0 中的设置大致是一样的但是极个别的地方一定有注意
   在 2.0 中，设置 `staticDir: path.join(__dirname,'../dist')`
   在 3.0 中，设置 `staticDir: path.join(__dirname,'dist')`
   如果这两个设置错了，运行 npm run build 都会报错。
3. 如果你想设置每个页面三元素; title 和 meta 信息推荐使用 [vue-meta-info]
