---
layout:     post
title:      "SMASHING Node.js: Javascript Everywhere"
subtitle:   "note"
date:       2019-09-30 22:00:00
author:     "Chaoran"
header-img: "img/post-bg-php-basic.jpg"
noToc:      true
tags:
    - 前端开发
    - node
---

> “To be a better girl ”

* 目录
{:toc #toc}

本文仅用于大致了解node 所涉及的技术
本博客的示例代码：[github 地址](https://github.com/chaoranwill/amazing-nodejs)

## V8
> v8 做了一件很酷的事情：始终坚定不移的实现最新版本的 ECMA 标准。node 核心团队也是如此，只要安装了最新版本的 node， 总能使用到最新版本的 V8.

## 阻塞与非阻塞 IO
> 为什么选择 node，其性能好在哪里，非阻塞的调试和错误处理有什么不同

node 为js 引入了一个复杂概念：共享状态的并发
```js
// example js

var books = ['math', 'chinese', 'english']

function showBooks () {
    var html = '<b>' + books.join('</b><br><b>') + '</b>'

    // magic
    books = []
    return html
}
```

```php
// example php

$books = array('math', 'chinese', 'english') 

function showBooks () {
    $html = '<b>' .join('</b><br><b>') . '</b>'

    // magic
    $books = array()
    return $html
}
```

结果
* node - 完整返回第一个请求，第二次请求时返回空
* php - 每次都完整返回

原因
* node - 是采用一个长期运行的进程，每次调用同一个 showBooks 函数，作用域不变
* apache - 每次请求一个进程，每次更新状态
![apache-vs-node](/img/in-post/post-amazing-node/apache-vs-node.jpg)

#### 阻塞
思考下面两端代码的执行结果
```php
// php
print('hello')

sleep(5)

print('world')
```
```js
// js
console.log('hello')
setTimeout(function(){
   console('chaoran')
}, 5000)

console.log('world')
// 分别打印 hello world chaoran
``` 
结果：
* php
    - 5s 后打印world 
    - sleep 阻塞了线程，阻塞时不执行任何操作，同步

* node
    - 先注册事件
    - 轮询是否分发，分发时执行回调，异步
    - 此过程无阻塞

**node 的并发实现也采用了事件轮询，所有像http，net io部分都是，当事件完成时，触发一个和[文件描述符](https://www.cnblogs.com/DengGao/p/file_symbol.html)（对打开的文件、socket、管道等的引用）相关的通知**

如果客户端向服务端发送数据，node 就会收到该文件描述符上的通知，然后触发js 回调

#### 调用堆栈
> v8 首次调用一个函数时，会创建一个 调用堆栈/执行堆栈

```js
function a() {
    b()
}
function b() {}

// 调用堆栈 a > b
// node 的并发量为 1？？
```
yes node 不提供并行操作

当堆栈调用非常快的时候，也无需并发处理请求，因此，最佳拍档是：
* v8 + 非阻塞 IO
    - v8 执行js 非常快
    - 非阻塞io 确保线程执行时，不会因为io 操作被挂起

#### 错误处理
```js
var http = require('http')

http.createServer(function () {
    throw new Error('错误不会被捕获')
}).listen(3000)

// 捕获方法
process.on('uncaughtException', function(err) {
    console.log(err)
    process.exit(1) // 手动退出
})
```

#### 堆栈追踪
```js
function c() {
    b()
}
function b() {
    a()
}
function a() {
    setTimeout(function(e) {
        throw new Error('hello')
    }, 0)
}

c()
```

**无法捕捉未来才执行的函数抛出的错误，如果加 try catch 则永远不会执行**
因此，在node 中每步都要进行错误捕捉，不然很难追踪，山下文会丢失

## node 中的 js
全局对象
* global
    - 和 window 性值一样，被全局访问
* process
    - 所有全局执行山下文的内容，唯一性
    - 如 浏览器中窗口名字 window.name ， node中进程名字 process.title
* 实用性的全局对象
    - setImmediate -- 与 process.nextTick 相当
    - console
    - ...

语言标准中没有的js常用API
* 定时器
* 事件
* 模块

#### 模块系统
> require、module、exports

* 绝对和相对模块
    - 绝对：node 通过在其内部node_modules 查找的模块，或内置模块（如js），可直接require(name)
    - 相对：相对目录

* 暴露 API
    > 默认每个模块都暴露一个空对象，要在其添加属性，可以简单使用exports

    - exports  对module.exports 的引用，如无法满足需求，可重写 module.exports
    
#### 事件
> 无论浏览器还是node 大量代码依赖于所监听或分发的事件

##### 浏览器中
处理事件相关的 DOM API (也用在一系列从window到XMLHTTPRequest 等对象)
* addEventListener
* removeEventListener
* dispatchEvent

##### node 中
node 暴露了 [Event EmitterAPI](https://www.runoob.com/nodejs/nodejs-event.html) ：定义了 on、emit、remove Listener 方法，以process.EventEmitter 形式暴露

```js
var EventEmitter = require('events').EventEmitter,
    a = new EventEmitter;

a.on('event', function() {
    console.log('event called')
})
a.emit('event')
```

**node 通常不会直接返回数据，而采用分发事件来传递数据**

```js
// example
http.Server(function(req, res) {
    var buf = '';
    req.on('data', function(data) {
        buf += data;
    });

    req.on('end', function() {
        console.log('数据接收完毕');
    });

    // 缓冲请求数据（data 事件）
    // 待数据接收完毕（end）
})
```
node中，事件分发 --> 通知尚未发生但即将要发生的事情

#### buffer
> buffer : 弥补了该语言对二进制数据处理的不足

* 固定内存分配的全局对象
    - 要放到缓冲区中的字节数需要预定
* 作用
    - 对数据进行编码转换

* base64
    - 仅由 ASCII 字符书写二进制数据的方式（用字符表示图片等复杂信息，但占用更多硬盘空间）

```js
var mybuffer = new Buffer('==ii1j2i3h1i23h', 'base64')
console.log(mybuffer)
require('fs').writeFile('logo.png', mybuffer)
```

## Node 重要的API
fs 模块是唯一一个同时提供同步和异步API的模块

#### 常用参数
* process.argv 包含了所有node 程序运行时的参数值
* 工作目录
    - `__dirname` 获取执行文件时该文件在文件系统中所在的目录
    - `process.cwd` 当前的工作目录
    - `process.chdir` 可灵活的修改工作目录
        - `process.chdir('/')`

* 环境变量 process.env
* 退出应用
    - `process.exit()`
    - 调用并提供一个退出代码
* 信号
    - node 通过在 process 对象上以事件分发形式发送信号
```js
process.on('SKILL', function() {
    // 信号已收到
})
```

#### 流
console.log 输出过程：
* 在指定字符串后加上\n（换行）字符
* 将其写到 stdout 流中

process 包含三个流对象
* `stdin` 标准输入 -- 可读流
    - 默认状态 paused
    - 恢复该流时，node 观察对应文件描述符（UNIX下为0），同时保持不退出，除非有IO ，否则总会退出
* `stdout` 标准输出 -- 可写流
* `stderr` 标准错误 -- 可写流

node 中的流：TCP ,HTTP 请求等，涉及到持续不断的数据读写时，流就产生了

stream
* 每次读取大小可变的内容块，并且每次读取后出发回调函数
应用
* watchFile
    - 监听文件的改动
* watch
    - 监听整个目录

## TCP

> 传输层协议：保证计算机间数据传输的可靠性和顺序

* node HTTP 服务器构建与 node TCP 服务器之上
* 编程角度：http.server 继承 net.server(net 是TCP 模块)
* 其他如邮件客户端（SMTP/IMAP/POP)、聊天程序（IRC/XMPP)、shell（SSH）等都基于 TCP 协议

#### 特性
* 面向连接
    - TCP 将客户端服务端看作一个连接/数据流，易理解和抽象（所基于的 IP 是面向无连接的）
    - IP 基于数据报的传输，送达无序
    - TCP 如何保证有序
        - 发送的 IP 数据报+标识连接、数据流顺序的信息
    - 用node 写TCP 服务器，就不需要考虑这些，，只需要连接和写数据就行 
* 面向字节
    - TCP 对字符编码无感知（不同编码--传输字节不同）
* 可靠性
    - 由于底层不可靠，+ 确认和超时 = 一系列机制达到可靠
* [流控制](https://www.cnblogs.com/iou123lg/p/9017044.html)
    - 通过流控制确保通信的计算机间传输数据的平衡
* 阻塞控制
    - 控制数据包的延迟率和丢包率

```js
// 创建一个tcp连接
var net = require('net');

var server = net.createServer(function (conn) {
  // handle connection
  console.log(' new connection !')
  conn.on('data', function(data) {

  });
  conn.on('close', function(data){

  })
});

server.listen(3000, function () {
  console.log('server listening on 3000')
})
``` 
#### HTTP
> 目的：进行文档交换，通过头信息（header）描述不同消息内容

* content-type 类型
* connection  keep-alive 默认
* Transfer-Encoding chunked 默认，node 异步的特性
* 。。。。

与 TCP 服务的差异性
* 回调函数中对象的类型
    - net connection
    - request， response
* 原因
    - http 服务器是更高层的api，提供了控制和http 协议相关功能
    - 可能同时打开多个连接，导致不容易区分是connection 还是 请求，node 为我们提供了请求、响应的抽象