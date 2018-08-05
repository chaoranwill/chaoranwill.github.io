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
之前的实现中，页面渲染同步，如果中间不小心堵一下，有点小尴尬。

* 比如，在start中添加一个定时器，会阻塞next的执行
* 若服务器接收请求时需要做大量的数值计算，也可能导致无法响应其他的请求

刚才的实现逻辑： 请求处理程序 -> 请求路由 -> 服务器
##### 5.1. node 中的并行
**据说：在node中除了代码，所有一切都是并行执行的**
> Node.js可以在不新增额外线程的情况下，依然可以对任务进行并行处理 —— Node.js是单线程的
* 通过事件轮询（event loop）来实现并行操作
  - 对此，我们应该要充分利用这一点 —— 尽可能的避免阻塞操作
* 多使用非阻塞操作——回调
* 创建一个子进程执行密集的cpu计算任务

##### 5.2. 实现非阻塞
此处我们使用一个新模块，child_process ——实现一个简单的非阻塞

[Node.js中的child_process模块详解](https://www.jb51.net/article/141698.htm)

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

此时，我们做到了路由处理，请求内容渲染，及非阻塞，下面尝试一下交互~

#### 操刀实践
> 场景： 用户上传文件，页面进行显示

##### 页面跳转响应
> 简单实现提交后页面跳转

* index 逻辑
  ```js
  // index.js
  var server = require('./server')
  var router = require('./route')
  var requestManager = require('./requestManager')

  var managers = []
  managers['/'] = requestManager.start
  managers['/start'] = requestManager.start
  managers['/upload'] = requestManager.upload

  server.start(router.route, managers)
  ```

* 执行 server 中的函数——监听各个请求，传入 managers 处理对象
  ```js
  // server.js
  var http = require("http");
  var url = require('url')

  function start(route, managers){
    function onRequest(req, res){
      var pathname = url.parse(req.url).pathname
      console.log('server request for', pathname)
      route(pathname, managers, res)
    }
    http.createServer(onRequest).listen(8888)
  }


  exports.start = start
  ```
  下面是 requestManager 中封装的我们对应各个处理函数
  ```js
  // requestManager.js
  function start(res){
    console.log('start')
    var body = '<html>' +
              '<head>' +
              '<meta http-equiv="Content-Type" content="text/html" charset="UTF-8"/>' +
              '</head>' +
              '<body>' +
              '<form action="/upload" method="post">' +
              '<textarea name="text" rows="20" cols="60"></textarea>' +
              '<input type="submit" value="上传"/>' +
              '</form>' +
              '</body>' +
              '</html>'

    res.writeHead(200, {'content-type':"text/html"})
    res.write(body)
    res.end()
  }

  function upload(res){
    console.log('upload')
    res.writeHead(200, {"content-type": "text/html"})
    var content = '<html><head><meta charset="UTF-8" /></head><body>上传啦</body></html>'
    res.write(content)
    res.end()
  }

  exports.start = start
  exports.upload = upload
  ```

* 在 router.js 中通过 manager 对象中的对应关系进行路由分发

  ```js
  // router.js
  function route(pathname, managers, res){
    console.log('rrr', pathname)
    if(typeof managers[pathname] == 'function'){
      console.log('yoyoyo:', pathname)
      managers[pathname](res)
    }else {
      console.log('managers no found')
      console.log('404')
    }
  }

  exports.route = route
  ```

好了，我们现在实现了一个简单的页面跳转与显示，下面我们尝试一下用之前学习的非阻塞方式处理

##### 非阻塞处理 post 请求
> 如果 post 时需要传输大量数据，node 会将post 的数据进行拆分，当触发特定的事件时，通过事件监听传输每次的数据

目前我们只是在 router.js 中操作了 respose 对象，所有的处理放在了HTTP服务器处理请求的过程中
对服务器中的 onRequest 中的 request 对象的 data 和 end 事件进行数据监听，
```js
request.addListener('data', function(chunk){
  // 收到新的 chunk 时触发
  console.log('receive', chunk)
})

request.addListener('end', functhon(){
  // 传输结束时触发
  console.log('end')
})
```

* 创建服务器后，监听请求中的 request 对象
  - 设置接收数据的编码格式为UTF-8
  - 注册“data”事件的监听器
  - end 事件中触发

  ```js
  // server.js

  var http = require("http");
  var url = require('url')

  function start(route, managers){
    function onRequest(req, res){
      var pathname = url.parse(req.url).pathname
      req.setEncoding('utf8')
      var chunkData = ''
      // 注册 data事件的监听器 接收 data 
      req.addListener('data', function(chunk){
        chunkData += chunk
        console.log('此刻接收到了：', chunk)
      })

      // request 信息传输结束，保证只触发一次
      req.addListener('end', function(){
        route(pathname, managers, res, chunkData)
      })
    }

    http.createServer(onRequest).listen(8888)
    console.log('start server')
  }


  exports.start = start
  ```

* 在路由处理 requestManager 中将数据呈现在路由 upload 中
  ```js
  function start(res, data){
    console.log('start')
    var body = '<html>' +
              '<head>' +
              '<meta http-equiv="Content-Type" content="text/html" charset="UTF-8"/>' +
              '</head>' +
              '<body>' +
              '<form action="/upload" method="post">' +
              '<textarea name="text" rows="20" cols="60"></textarea>' +
              '<input type="submit" value="上传"/>' +
              '</form>' +
              '</body>' +
              '</html>'

    res.writeHead(200, {'content-type':"text/html"})
    res.write(body)
    res.end()
  }

  function upload(res, data){
    console.log('upload')
    res.writeHead(200, {"content-type": "text/html"})
    var content = '<html><head><meta http-equiv="Content-Type" content="text/html" charset="UTF-8"/></head><body>received----'+ data + '</body></html>'
    res.write(content)
    res.end()
  }

  exports.start = start
  exports.upload = upload
  ```

现在我们可以获取到提交的内容，但如何对表单里的数据进行筛选或处理呢
querystring 模块
> 一般是对 http 请求所带的数据进行解析：
 `querystring.parse, querystring.stringify, querystring.escape, querystring.unescape`

为了分离出form 中的参数对象，我们试一下 parse 方法

```js
// 引入 querystring 模块
const querystring = require('querystring')

function upload(res, data){
  console.log('upload')
  // 将 data 序列化为一个对象
  data = querystring.parse(data)
  res.writeHead(200, {"content-type": "text/html"})
  var content = '<html><head><meta http-equiv="Content-Type" content="text/html" charset="UTF-8"/></head><body>received----'+ data.text + '</body></html>'
  res.write(content)
  res.end()
}
```

上述过程就是如何处理 post 数据