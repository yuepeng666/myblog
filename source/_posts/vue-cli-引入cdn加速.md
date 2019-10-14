---
title: vue cli 引入cdn加速
date: 2019-10-14 14:51:58
categories: vue webpack vue-cli
tags: vue webpack vue-cli
---

<meta name="referrer" content="never">

# vue.config.js 示例

```js
const path = require('path');
const TerserPlugin = require('terser-webpack-plugin');

const vueV = require('vue/package.json').version;
const routerV = require('vue-router/package.json').version;
const vuexV = require('vuex/package.json').version;
const axiosV = require('axios/package.json').version;
const elementV = require('element-ui/package.json').version;
const cookieV = require('js-cookie/package.json').version;
const nprogressV = require('nprogress/package.json').version;
const echartsV = require('echarts/package.json').version;

const isProduction = process.env.NODE_ENV === 'production';
const isCdn = true; // 是否开启cdn模式

const logTxt =
  process.env.NODE_ENV === 'development'
    ? '编译开发'
    : process.env.VUE_APP_FLAG === 'test'
    ? '打包测试'
    : '打包线上';

console.log(logTxt);
```

<!-- more -->

```js
function resolve(dir) {
  return path.join(__dirname, dir);
}
// 需要忽略打包的 npm包
const Externals = {
  vue: 'Vue',
  vuex: 'Vuex',
  'vue-router': 'VueRouter',
  axios: 'axios',
  'element-ui': 'ELEMENT',
  'js-cookie': 'Cookies',
  nprogress: 'NProgress',
  echarts: 'echarts'
};
// cdn地址
const CDN = {
  css: [
    // `https://cdn.jsdelivr.net/npm/element-ui@${elementV}/lib/theme-chalk/index.min.css`,
    `https://cdn.bootcss.com/element-ui/${elementV}/theme-chalk/index.css`,
    `https://cdn.bootcss.com/nprogress/${nprogressV}/nprogress.min.css`
  ],
  js: [
    // `https://cdn.jsdelivr.net/npm/vue@${vueV}/dist/vue.min.js`,
    // `https://cdn.jsdelivr.net/npm/vuex@${vuexV}/dist/vuex.min.js`,
    // `https://cdn.jsdelivr.net/npm/vue-router@${routerV}/dist/vue-router.min.js`,
    `https://cdn.bootcss.com/vue/${vueV}/vue.min.js`,
    `https://cdn.bootcss.com/vuex/${vuexV}/vuex.min.js`,
    `https://cdn.bootcss.com/vue-router/${routerV}/vue-router.min.js`,
    //  从jsdeliver 引入完整element-ui
    // `https://cdn.jsdelivr.net/npm/element-ui@/${elementV}/lib/index.min.js`,
    // 从bootcdn
    `https://cdn.bootcss.com/element-ui/${elementV}/index.js`,
    `https://cdn.bootcss.com/echarts/${echartsV}/echarts.min.js`,
    `https://cdn.bootcss.com/axios/${axiosV}/axios.min.js`,
    `https://cdn.bootcss.com/js-cookie/${cookieV}/js.cookie.min.js`,
    `https://cdn.bootcss.com/nprogress/${nprogressV}/nprogress.min.js`
  ]
};

module.exports = {
  publicPath: '/', // 公共路径
  outputDir: process.env.VUE_APP_FLAG === 'test' ? 'test-dist' : 'dist', // 不同的环境打不同包名
  lintOnSave: false, // 关闭eslint
  productionSourceMap: false, // 如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建
  parallel: require('os').cpus().length > 1, // 构建时开启多进程处理babel编译
  // 这里写loader
  chainWebpack: config => {
    // production打包才使用CDN
    if (isProduction && isCdn) {
      config.plugin('html').tap(args => {
        args[0].cdn = CDN;
        return args;
      });
    }

    // config.resolve.alias
    //   .set('assets', resolve('src/assets'))
    //   .set('pages', resolve('src/pages'))
    //   .set('components', resolve('src/components'))
    //   .set('utils', resolve('src/utils'))
  },

  // 这里回覆盖webpack默认配置
  configureWebpack: config => {
    // production模式
    if (isProduction && isCdn) {
      // 忽略的包
      config.externals = Externals;
      // 打包生产.gz包
      // config.plugins.push(new CompressionWebpackPlugin({
      //   algorithm: 'gzip',
      //   test: new RegExp('\\.(' + productionGzipExtensions.join('|') + ')$'),
      //   threshold: 10240,
      //   minRatio: 0.8
      // }))
      // 添加自定义代码压缩配置
      config.plugins.push(
        new TerserPlugin({
          // 是否开启多线程
          parallel: true,
          terserOptions: {
            // 去除打印
            compress: {
              warnings: false,
              drop_console: true,
              drop_debugger: true,
              pure_funcs: ['console.log']
            },
            // 去除注释，当设置为true时，会保留注释
            // 当然这个默认是false
            output: {
              comments: false
            }
          }
        })
      );
    }
  }
};
```

  <!-- more -->
