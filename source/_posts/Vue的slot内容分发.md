---
title: Vue的slot内容分发
date: 2019-02-04 15:59:01
categories: Vue
tags: vue
---

## 单个 slot

在 children 这个标签里放 Dom，Vue 不会显示，类似于 React

```JavaScript
  //父
  <children>
  <span>12345</span>//这边不会显示
  </children>

  //子
  components: {
  children: {
      template: "<button>为了明确作用范围，所以使用button标签</button>"
    }
  }
```
 <!-- more -->

你需要写成这个样子

```JavaScript
children: {
  template: "<button><slot></slot>为了明确作用范围，所以使用button标签<button>"
}
```

可以给 slot 添加属性

```JavaScript
  //父
<children>
  <span slot="name1">12345</span>
</children>

//子
components: {
  children: {
    template: "<button>
            <slot name="name1"></slot>
            button标签
          </button>"
  }
}
```
