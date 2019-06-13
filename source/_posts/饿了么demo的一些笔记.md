---
title: 饿了么demo的一些笔记
date: 2019-03-12 15:16:28
categories:
tags: vue JavaScript
---
# 饿了么demo的一些笔记
  1.取得对象key相同的value和 例：
  ```js
    var arr = [
      { id: 'a', num: 2 },
      { id: 'a', num: 2 },
      { id: 'a', num: 2 },
      { id: 'b', num: 8 }
    ]
    var newarr = {a:6, b:8}
    // 代码实现
    let obj = {};
    for (const item of arr) {
      let [ id, num ] = [ item.id, item.num];
      /* 
        hasOwnProperty() 判断对象是否拥有某属性
      */
      if(obj.hasOwnProperty(id)){
        obj[id] += num;
      }else{
        obj[id] = num;
      }
    }
    console.log(obj)

  ```
  2. 把对象存进数组，如果存在相同id则数量加1（购物车）
  ```js
    let shopcar = [];
    let flag = false;
    shopcar.some(item => {
        if (item.id === val.id) {
            item.quantity += 1
            flag = true
            return true
        }
    })
    if (!flag) {
        state.shopcar.push(val)
    }

  ```
  3. 