---
title: Vue中跳转页面返回原页面回到记忆位置
date: 2019-02-26 10:36:12
categories: Vue
tags: vue
---
# Vue中跳转页面返回原页面回到记忆位置
1. 修改 router-view
```js
    <transition name="router-fade" mode="out-in">
        // 在这里显示被缓存的页面
        <keep-alive>
            <router-view v-if="$route.meta.keepAlive"></router-view>
        </keep-alive>
    </transition>
    <transition name="router-fade" mode="out-in">
        // 在这里显示不需要被缓存的页面
        <router-view v-if="!$route.meta.keepAlive"></router-view>
    </transition>
```
2. 修改vueRouter的配置文件index.js
```js
    // 
    {
        path: '/home',
        name: 'home',
        component: home,
        meta: {
            title: 'home',
            keepAlive: true // 需要被缓存
        }
    },
    // mode: 'history',     // vueRouter默认为hash模式
    scrollBehavior (to, from, savedPosition) {
        if (savedPosition) {
            return savedPosition
        } else {
            if (from.meta.keepAlive) {
                from.meta.savedPosition = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
            }
            return { x: 0, y: to.meta.savedPosition ||0}
        }
    }
```