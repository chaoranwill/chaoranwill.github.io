---
layout:     post
title:      "To create an HTTP service"
subtitle:   "the simplest tutorial of http"
date:       2018-07-29 22:00:00
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

#### 1. 最简单的 http 服务器
```js
// server.js

var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);

//  node server.js
// 打开http://localhost:8888/，你会看到一个写着“Hello World”的网页~
```
就这么简单，本文 完~

> oh，no
you too young, too simple

#### 2. 肢解代码
* `var http = require("http")`
  - 请求（require）Node.js自带的 http 模块，并且把它赋值给 http 变量

* `createServer `
  - listen 方法-数值参数指定该 HTTP 服务器监听的端口号

* `createServer` 的参数
  - 基于事件驱动的回调
    - 无论何时我们的服务器收到一个请求，这个函数就会被调用

* 请求处理

   onRequest() 函数被触发的时候，有两个参数对象
  - request
  - response
    ```js
    // 发送一个HTTP状态200和HTTP头的内容类型
    response.writeHead(200, {"Content-Type": "text/plain"});
    // 添加HTTP主体内容
    response.write("Hello World");
    // 完成响应
    response.end();
    ```

#### 3. 模块封装
> 这一步我们把server.js变成一个真正的Node.js模块

1. 函数封装
  将我们的脚本封装到一个函数里面，然后导出该封装函数
    ```js
    var http = require("http");

    function start() {
      function onRequest(request, response) {
        console.log("Request received.");
        response.writeHead(200, {"Content-Type": "text/plain"});
        response.write("Hello World");
        response.end();
      }

      http.createServer(onRequest).listen(8888);
      console.log("Server has started.");
    }

    exports.start = start;
    ```

2. 模块引用
    ```js
    // 如主文件名为index.js，写入
    var server = require("./server");

    server.start();
    ```
    执行 `node index.js`

#### 4. 路由
所有请求数据都在 request对象中，数据解析，还需要 url， querystring模块

来，我们试一试找出浏览器的请求路径~
##### 4.1 获取路由
```js
var http = require("http");
var url = require('url')

function start(){
  function onRequest(req, res){
    var url = url.parse(req.url)
    // 打印 url 信息
    console.log('server start url', url)
    res.writeHead(200, {"content-type": "text/plain"})
    res.end()
  }
  http.createServer(onRequest).listen(8888)
}

exports.start = start
```

request.url参数打印：
![request](/img/in-post/post-node-7/request.png)

##### 4.2 有路可寻
> 引入路由处理

* 创建route.js，处理路由信息，在index页面引入该模块，并作为 server 中start 函数的参数执行，
* 解析每一个request，获取其url 路径进行处理

```js
// server.js
var http = require("http");
var url = require('url')

function start(route){
  function onRequest(req, res){
    var pathname = url.parse(req.url).pathname
    route(pathname)
    res.writeHead(200, {"content-type": "text/plain"})
    res.end()
  }
  http.createServer(onRequest).listen(8888)
}

exports.start = start
```
```js

// route.js
function route(pathname){
  console.log('route', pathname)
}

exports.route = route

// index.js  引入route
var server = require('./server')
var router = require('./route')
server.start(router.route)
```
以上代码我们实现了有路可寻



为了避免多重的 if..else..，我们通过对象传递一系列请求 
* 首先创建一个 requestManager 模块，导出多个处理函数
* 创建 managers 对象：映射不同路由的处理方法
* 将路由与函数的映射关系作为参数传递给 server
* server 中调用 route 的处理结果

  ```js
  // requestManager.js
  function start(){
    console.log('route-----start')
    return 'hello start'
  }
  function next(){
    console.log('route-----next')
    return 'hello next'
  }
  exports.start = start
  exports.next = next
  ```
  ```js
  // index.js
  var server = require('./readfile')
  var router = require('./route')
  var requestManager = require('./requestManager')

  var managers = []
  managers['/'] = requestManager.start
  managers['/start'] = requestManager.start
  managers['/next'] = requestManager.next

  server.start(router.route, managers)

  // http://localhost:8888/start, 浏览器会输出“hello start”
  // http://localhost:8888/next 会输出“hello next”
  // http://localhost:8888/chaoran 会输出“404”。
  ```

* manager ：每一个路由提供对应的处理函数
  ```js
  // server.js
  var http = require("http");
  var url = require('url')

  function start(route, manager){
    function onRequest(req, res){
      var pathname = url.parse(req.url).pathname
      console.log('server request for', pathname)
      var content = route(pathname, manager)
      res.writeHead(200, {"content-type": "text/plain"})
      res.write(content)
      res.end()
    }
    http.createServer(onRequest).listen(8888)
  }

  exports.start = start
  ```

* 取出managers 中的路由事件进行处理
  ```js
  // route.js
  function route(pathname, managers){
    console.log('rrr', pathname)
    if(typeof managers[pathname] == 'function'){
      return managers[pathname]()

    }else {
      console.log('managers no found')
      return ''
    }
  }

  exports.route = route
  ```


好啦，用是能用的，就是偶尔会挂 ( ﹁ ﹁ ) ~→

#### 5. 非阻塞
之前的实现中，页面渲染同步，如果中间不小心堵一下，有点小尴尬。*比如，在start中添加一个定时器，会阻塞next的*执行

刚才的实现逻辑： 请求处理程序 -> 请求路由 -> 服务器
##### 5.1. node 中的并行
**据说：在node中除了代码，所有一切都是并行执行的**
> Node.js可以在不新增额外线程的情况下，依然可以对任务进行并行处理 —— Node.js是单线程的
* 通过事件轮询（event loop）来实现并行操作
  - 对此，我们应该要充分利用这一点 —— 尽可能的避免阻塞操作
* 取而代之，多使用非阻塞操作——回调

##### 5.2. 实现非阻塞
此处我们使用一个新模块，child_process ——实现一个简单的非阻塞

```js
// server.js
var http = require("http");
var url = require('url')

function start(route, manager){
  function onRequest(req, res){
    var pathname = url.parse(req.url).pathname
    console.log('server request for', pathname)
    route(pathname, manager, res)
  }
  http.createServer(onRequest).listen(8888)
}

exports.start = start
```
```js
// requestManager.js
var exec = require('child_process').exec

function start(res){
  console.log('route-----start')

  exec("find /", {timeout: 10000,maxBuffer: 20000*1024}, function(error, stdout, stderr){
    res.writeHead(200, {"content-type": "text/plain"})
    res.write(stdout)
    res.end()
  })
}
function next(res){
  console.log('route-----next')
  res.writeHead(200, {"content-type": "text/plain"})
  res.write('hello next')
  res.end()
}
exports.start = start
exports.next = next
```
```js
// route.js
function route(pathname, managers, res){
  console.log('rrr', pathname)
  if(typeof managers[pathname] == 'function'){
    managers[pathname](res)

  }else {
    console.log('managers no found')
    console.log('404')
  }
}

exports.route = route
```
```js
// index.js
var server = require('./server')
var router = require('./route')
var requestManager = require('./requestManager')

var managers = []
managers['/'] = requestManager.start
managers['/start'] = requestManager.start
managers['/next'] = requestManager.next

server.start(router.route, managers)
```
这时：当我们打开http://localhost:8888/start时，会花10秒钟的时间才载入，而当请求http://localhost:8888/next 的时候，会立即响应，纵然这个时候/start响应还在处理中。