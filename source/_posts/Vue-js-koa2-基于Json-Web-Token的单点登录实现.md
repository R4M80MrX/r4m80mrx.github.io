---
title: Vue.js + koa2 基于Json Web Token的单点登录实现
copyright: true
date: 2019-03-22 16:14:10
tags:
---

# 概述

## [SSO(Single Sign On)单点登录](https://baike.baidu.com/item/SSO/3451380)

SSO 是在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统。它包括可以将这次主要的登录映射到其他应用中用于同一个用户的登录的机制。它是目前比较流行的企业业务整合的解决方案之一。

## [JWT(Json Web Token)](https://jwt.io/introduction/)

一种跨域认证解决方案, 用它来实现 SSO

## [koa2](https://koa.bootcss.com/)

基于 Node.JS 的 Web 开发框架, 由 Express 原班人马基于 ES7 打造, 相比 Express 代码更清晰明了, 性能强劲

# 准备工作

## 配置

之前的文章讲到 Vue+NodeJS 的全栈开发, 最后采用了在根目录 vue.config.js 里添加如下内容

```javascript
// vue.config.js

// ...some other configs

module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        pathRewrite: { '^/api': '' }
    }
  }
}
```

实现将前端 axios 发送到/api/\*的内容转发到开在本地 3000 端口的 NodeJS 服务器.

##
