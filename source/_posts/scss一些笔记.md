---
title: scss一些笔记
date: 2019-10-14 15:07:25
categories: scss
tags: scss
---

<meta name="referrer" content="never">



# scss for循环

```scss
$color-list: #5e83fb, #f7da47, #58ca9a, #ee706d, #ffa502, #808e9b;

@for $i from 1 to 7 {
  .grid-#{$i} {
    background-color: nth($color-list, $i);
  }
}
```
