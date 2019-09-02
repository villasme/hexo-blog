---
title: vue碰到的问题
date: 2019-09-02 15:50:08
categories: FE
tags: Vue
---

## vue调试工具Devtools不出现的解决方式

```js
// main.js中
import Vue from 'vue'
if (process.env.NODE_ENV !== 'production') {
    Vue.config.devtools = true
}
```