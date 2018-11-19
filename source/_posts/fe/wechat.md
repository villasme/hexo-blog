---
title: 微信服务系列
categories: FE
tags: 
- 微信小程序
- 微信公众号
---

## 搭建微信公众号 (详情看文档)   https://github.com/node-webot

* koa与co-wechat 来构建微信公众号自动回复功能

```js
const Koa = require('koa');
const wechat = require('co-wechat');
```

* 微信公共平台node库api  ---->>>>  http://doxmate.cool/node-webot/co-wechat-api/api.html#api_js_exports_registerTicketHandle

```js 
var WechatAPI = require('co-wechat-api');
```