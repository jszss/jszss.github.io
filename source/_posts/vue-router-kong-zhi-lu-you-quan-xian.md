---
title: 'vue-router 控制路由权限'
date: 2020-09-24 10:19:02
tags: [递归,vue-router]
published: true
hideInList: false
feature: 
isTop: false
---
```js
// src/utils/index.js
const { pathToRegexp } = require('path-to-regexp');

export function getAuthRouters(authMenu) {
    let authRouters = [];
    (authMenu || []).forEach((item) => {
        const { resourceUrl, childMenu } = item;
        resourceUrl && authRouters.push(resourceUrl);
        if (childMenu && childMenu.length > 0) {
            // 合并子级菜单
            authRouters = [...authRouters, ...getAuthRouters(childMenu)];
        }
    });
    return authRouters;
}
/**
 *
 * @param { Array } authRouters
 */
export function createAuthRouters(authRouters) {
    const isAuthUrl = (url) => {
        return (authRouters || []).some((cUrl) => {
            return pathToRegexp(url).toString() === pathToRegexp(cUrl).toString();
        });
    };
    return function createRouters(routers, upperPath) {
        let nRouters = [];
        (routers || []).forEach((item) => {
            const { children, path, name } = item;
            let isMatched = false,
                nItem = { ...item },
                fullPath = `${upperPath || ''}/${path}`.replace(/\/{2,}/, '/'),
                nChildren = null;
            children && (nChildren = createRouters(children, fullPath));
            // 1.当前路由匹配
            if (isAuthUrl(fullPath)) {
                isMatched = true;
            }
            // 2.存在子路由匹配
            if (nChildren && nChildren.length > 0) {
                nItem.children = nChildren;
                isMatched = true;
            }
            // 特殊处理
            if(name === "home"){
                isMatched = true;
            }
            // nItem
            isMatched && nRouters.push(nItem);
        });
        return nRouters;
    };
}

// src/router.js

import Vue from 'vue';
import Store from '@/store';
import Router from 'vue-router';
import Cookie from 'js-cookie';

const openRouters = [];
const authRouters = [{
    path : "order/list",
    // ...
    meta : {
        // 是否身份验证(至于默认定义false还是true由开发者自定义)
        isAuth : true
    }
}];

/* 动态注册路由 */
async function AddRoutes() {
    // 获取用户路由权限
    let res = await POST(API.AUTH_RESOURCE_LISTSIDEMENU);
    try {
        const { code, data } = res || {};
        if (code === '000') {
            let newAuthRoutes = createAuthRouters(getAuthRouters(data))(authRouters, routes.options.base);
            // 注册路由
            routes.addRoutes([].concat(newAuthRoutes, openRouters));
            // 设置已注册
            Store.commit('UPDATE_IS_ADD_ROUTERS', true);
            // 保存菜单信息
            Store.commit('UPDATE_MENU_INFO', data);
        }
    } catch (error) {
        console.error('>>> AddRoutes() - error:', error);
    }
}


/* 路由前置 */
let { origin } = window.location || {};
routes.beforeEach((to, from, next) => {
    const { meta, matched, path } = to;
    let isMatched = matched && matched.length > 0; // 是否匹配
    let isAuth = (meta || {}).isAuth; // 是否授权访问
    let { isAddRoutes } = Store.state; // 注册路由
    let isLogin = Cookie.get('token') || null; // 是否登录
    if ((isMatched && !isAuth) || (isMatched && isAuth && isLogin)) {
        // next()
        // 1.匹配路由 && 未登录访问
        // 2.匹配路由 && 登录访问 && 登录
        next();
    } else if ((isMatched && isAuth && !isLogin) || (!isMatched && !isLogin)) {
        // 登录
        // 1.匹配路由 && 登录访问 && 未登录
        // 2.未匹配路由 && 未登录
        next(`/login?r=${origin}/e-lottery${path}`);
    } else if (!isMatched && isLogin && isAddRoutes) {
        // 404
        // 1.未匹配路由 && 登录 && 动态注册路由
        next('/404');
    } else if (!isMatched && isLogin && !isAddRoutes) {
        // 注册路由
        // 1.未匹配路由 && 登录 && 未动态注册路由
        AddRoutes();
        next();
    }
});

```