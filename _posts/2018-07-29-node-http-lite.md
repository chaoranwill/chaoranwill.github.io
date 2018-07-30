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

#### 最简单的 http 服务器
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

#### 肢解代码
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

#### 模块封装
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

#### 路由
所有请求数据都在 request对象中，数据解析，还需要 url， querystring模块

来，我们试一试找出浏览器的请求路径~
##### 获取路由
```js
var http = require("http");
var url = require('url')

function start(){
  function onRequest(req, res){
    var pathname = url.parse(req.url).pathname
    console.log('server request for', pathname)
    res.writeHead(200, {"content-type": "text/plain"})
    res.end()
  }
  http.createServer(onRequest).listen(8888)
}

exports.start = start
```

request.url参数打印：
![request](/img/in-post/post-node-7/request.png)

##### 有路可寻
> 引入路由处理

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

为了避免多重的 if..else..，我们通过对象传递一系列请求 
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

好啦，用是能用的，就是偶尔会挂 ( ﹁ ﹁ ) ~→

#### 实现非阻塞
之前的实现中，页面渲染同步，如果中间不小心堵一下，有点小尴尬

刚才的实现逻辑： 请求处理程序 -> 请求路由 -> 服务器

