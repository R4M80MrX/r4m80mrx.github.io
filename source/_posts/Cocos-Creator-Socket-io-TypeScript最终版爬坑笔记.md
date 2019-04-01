---
title: Cocos Creator + Socket.io + TypeScript最终版爬坑笔记
copyright: true
date: 2019-03-22 16:24:08
tags:
---

&emsp;&emsp;在做 Cocos Creator H5 联机小游戏的时候, 想用 Socket.io 来进行实时通信, 一阵搜索发现相关资料甚少, 总有人评论让自己封装 Web Socket. 既然有现成的完善的带有心跳和重连机制的 Socket.io, 为什么要自己造前后端的轮子而不把精力放在实现所需功能上呢, 所以写一篇文章来记录一下.

# 环境

开发环境:

- 操作系统: Win10
- Creator 版本: v2.0.9
- NodeJS 版本: v10.0.6
- Socket.io 版本: v2.2.0
- 开发语言: TypeScript
  _其他环境请自行尝试_

# 准备工作

目录结构:

```
sio
 └─ sio-client
 │
 └─ sio-server
```

1. 新建文件夹 `sio` 作为项目根目录
2. 启动 Cocos Creator, 在项目根目录新建 Hello TypeScript 项目, 命名为 `sio-client` , 打开工程并初始化 TS 项目. 具体步骤不再赘述, 详见

- Cocos Creator 新手入门: [官方文档](https://docs.cocos.com/creator/manual/zh/getting-started/)
- TypeScript 项目入门教程: [TS 教程](https://forum.cocos.com/t/cocos-creator-typescript/56306)

3. 在项目根目录新建文件夹, 命名为 `sio-server` 并在该文件夹初始化 npm 项目, 安装相关模块. 我的`package.json`如下, 具体过程不再赘述.

```json
{
  "name": "sio-server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "koa": "^2.7.0",
    "socket.io": "^2.2.0"
  },
  "devDependencies": {
    "debug": "^4.1.1"
  }
}
```

4. 进入`sio-server\node_modules\socket.io-client\dist` 目录, 找到 `socket.io.js` 文件, 把它放入你的 Cocos Creator 工程中. 我这里把它放在了 `assets\Script\lib` 中

至此, 准备工作完成, 开始写代码

# 代码

## 服务端

我们这里使用 Node.JS 搭建服务端.
进入 `sio-server` 文件夹, 新建 `index.js` , 写一个基于 Koa2 和 Socket.io 的简易 Web Socket 服务端.

```js
// index.js

var Koa = require('koa');
var app = new Koa();
const server = require('http').createServer(app.callback());
const io = require('socket.io')(server);

io.on('connection', socket => {
  // 当用户建立Socket连接时
  console.log('user connected');

  // 接收消息
  socket.on('msg', data => {
    console.log(data);
  });

  // 当用户断开连接时
  socket.on('disconnect', () => {
    console.log('user disconnected');
  });
});

// 监听本地3000端口
server.listen(3000, () => {
  console.log('listening on *:3000');
});
```

然后在服务端根目录执行 `node index`

```console
❯ node index
listening on *:3000
```

则服务器搭建成功

## Creator 项目

我创建的是 TS 项目, 准备阶段已经将 `socket.io.js` 放进了 Hello TypeScript 项目中, 需要将 Socket.io-client TS 声明(https://raw.githubusercontent.com/DefinitelyTyped/DefinitelyTyped/master/types/socket.io-client/index.d.ts)下载至 `socket.io.js` 所在文件夹并重命名为 `socket.io.d.ts` , 接下来小小地修改一下 `HelloWorld.ts` 来引用它.

```js
const { ccclass, property } = cc._decorator;
import { connect } from './lib/socket.io';

@ccclass
export default class Helloworld extends cc.Component {
  @property(cc.Label)
  label: cc.Label = null;

  start() {
    let self = this;
    var socket = null;

    socket = connect('http://localhost:3000');
    socket.on('connected', () => {
      console.log('Socket connected');
    });
  }
}
```

# 运行结果

NodeJS 控制台输出

```
user connected
```

Web Mobile 输出

```
Socket connected
```
