---
title: 异步创建加载script
date: 2019-10-14 15:12:14
categories: js 
tags: js
---

<meta name="referrer" content="never">



# 异步创建加载script
```js
/**
 * @param {*} url 需要引用的script标签的地址

 * @param {*} callback 创建完成script元素回调

 * @returns

 */

function createScript(url, callback) {

  const scriptEl = document.createElement('script');

  scriptEl.charset = 'utf-8'

  scriptEl.src = url;

  // document.body.appendChild(scriptEl);

  // 添加到head

  const head = document.head || document.getElementsByTagName('head')[0];

  head.appendChild(scriptEl);
```
<!-- more -->
```js  

  const promise = new Promise((resolve, reject) => {

    // 不支持ie8及以下

    scriptEl.addEventListener(

      'load',

      e => {

        if (!callback) {

          resolve(e);

        } else {

          callback()

          resolve(e);

        }

      },

      false

    );

    scriptEl.addEventListener(

      'error',

      e => {

        removeScript(scriptEl)

        reject(e);

      },

      false

    );

  });

  return promise;

}

/**

 * 移除script标签

 * @param scriptEl script dom

 */

function removeScript(scriptEl) {

  document.body.removeChild(scriptEl);

}

export default createScript;

```

