---
title: Vue.js学习笔记
copyright: true
date: 2019-03-21 20:28:43
tags:
---

# 想法

# 经验

## 0. 选择困难症

前端三大框架, 各有优劣, 网上各种测评看了好久, 最终决定先拿 vue 下手
然后问题又来了, 用什么 UI 框架呢?

- vux
- element-ui
- mint-ui
- bootstrap-vue
- ......

最终选择了星星数最多的 vux, 虽然这个框架是个人开发维护的, 也存在很多问题.

## 1. vue-cli3 与 vux 的融合

vux 官方暂时还没有适配 vue-cli3
[vue-cli3](https://cli.vuejs.org/zh/) 可以用 [vue-cli-plugin-vux](https://www.npmjs.com/package/vue-cli-plugin-vux) 一键安装 [vux](https://vux.li/) UI 框架, 不需要手动适配 vue-loader

```console
npm i vue-cli-plugin-vux
vue add vux
```

## 2. 初始化项目的注意事项

可以通过命令行输入`vue ui`打开图形化界面
也可以`` vue create `project-name` ``直接在命令行创建
两种方式的效果是一样的, 看你习惯用哪种

```
   Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
 (*) Babel //转码器, 将ES6+转换成ES5以适配更多浏览器
 ( ) TypeScript //根据情况自选
 ( ) Progressive Web App (PWA) Support //根据情况自选
 (*) Router //前端路由, 选上
 (*) Vuex //全局状态管理, 选上
 (*) CSS Pre-processors //CSS预处理器, 选上
 ( ) Linter / Formatter //如果已经在编辑器里安装了ESLint, Prettier等插件的话就不用选, 会冲突
 ( ) Unit Testing //单元测试, 暂时没用上
 ( ) E2E Testing //暂时没用上
```

回车之后就进入了进一步的配置.
`Use history mode for router?`默认 Y, 链接里就不会出现/#/
一路回车即可.

## 3. VSCode 对 Webpack Alias 路径的支持('@/'), 只需在项目根目录中添加 jsconfig.json 文件, 内容如下:

```json
//jsconfig.json

{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["./src/**/*"],
  "exclude": ["node_modules"]
}
```

## 4. Vue.js + Node.js(koa2)集成开发

开发全栈项目, 登录组件拼凑完成以后, 前端开发告一段落, 是时候写一点后端接口了. 目前没有找到比修改 proxy 更优雅的解决方案.

另一种方法参考:
[【新手向】Vue.js + Node.js(koa) 合体指南](https://juejin.im/post/5c2cc80bf265da6169175962)

# 点子

https://github.com/wangdahoo/vonic
http://ghbtns.com/#star

<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=star&count=true&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
