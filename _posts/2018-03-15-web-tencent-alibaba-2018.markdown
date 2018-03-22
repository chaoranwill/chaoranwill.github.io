---
layout:     post
title:      "The interview summary"
subtitle:   "From Tencent and Alibaba"
date:       2018-03-09 19:55:00
author:     "Chaoran"
header-img: "img/post-bg-interview.jpg"
noToc:      true
tags:
    - 前端开发
---

> “To be is to be perceived. ”

* 目录
{:toc #toc}


#### 聊之前
最近暑期实习招聘已经开始，个人目前参加了腾讯和阿里的内推，在此总结一下
一是备忘、总结提升，二是希望给大家一些参考
其他面试及基础相关可以参考其他博文：
* [Questions of FE](https://chaoranwill.github.io/2018/03/01/web-questions-of-interview-2018/)
* [Web basis summary](https://chaoranwill.github.io/2018/02/27/web-basis-2018/)
* [FE knowledge fragment](https://chaoranwill.github.io/2018/02/27/FE-knowledge-fragment-2018/)

阿里和腾讯每位面试官的面试时间基本都在 30-60 分钟

**腾讯**

首先腾讯分为三面，都为技术面：
* 初试一个面试官
* 复试两个面试官，包括电话远程 online coding
（我也不知道为什么几天内三个面试官面我，只算两个面试过程 ヾ(´A｀)ノﾟ）
* 终面一位面试官

    这位应该是大 boss ，他说并不是前端开发的，面试的问题也不会很深入，主要看个人对这个领域的想法以及对常见问题在前端领域的解决思路，不按套路出牌，emmm 感觉回答的不理想
    类似这种问题：
    - 说说最能体现你能力的工作
    - 网络安全的实现
        如何检测恶意脚本
        如何屏蔽
        ...

腾讯的远程 online coding 时间较长，大概一个多小时，不仅要按要求编程，也要口述思路以及关键点，过程类似压力面，面试官说完题目要求会给你思考及coding 时间，他可以远程看到面试者的 coding 状态，主要考察应变能力，思维活跃度，编码习惯，调试能力，以及测试方法，本人在此过程中没有太注意测试过程，导致对于特殊情况考虑不全面，测试样例不完善，望小伙伴们注意 ヾ(´A｀)ノﾟ，不过，在口述代码时发现也可以自己提出来需要完善的地方。coding 为一到两题，后续问题都是围绕它结合实际应用进行拓展，主要考察是否能灵活运用以及相似的思路转换，当时面试时间太长以及基础知识较差，进制转换，存储那些个基础被小学老师收回，一连串的炮轰简直爽歪歪，个人表示此过程自己的表现较差，也要重视基础基础啊老铁们  (￣_￣ )

经历了腾讯云的四个面试官，以及其他部门一个面试官的酱油面，腾讯的技术面试官普遍语速较快，思路转换很快，要跟上面试官的节奏，聊到自己比较熟悉的可以多说几句，他们也会顺着你回答的内容进行深入，也会引导面试者的回答方向，如果不太熟尽量坦白一些，不懂装懂很容易 gg

**阿里**

我投的是蚂蚁金服的前端开发，投过简历硬生生排队等了12天，还被内推人提前告知蚂蚁的前端很严格 (￣_￣ )
阿里分为在线测试，初试 ......
* 首先是在线测试
    投完简历后官网会有相关在线测试题
    阿里前端的在线测试只有一道coding 题，限时 30 分，由于初次在线答题，看着倒计时紧张的思路不通，未能准确理解题意，但实际题目并不难，考察使用原生 js 实现类似css 的层级选择器的功能，具体题目记不太清，将仅存的记忆写了下来并附上个人实现，详情见本文后部分
* 初试

总体来说，面试中有按照面试题出的，也有直接聊的，一般也会结合实际工作中会遇到的场景以及技术中的一些坑，回答时结合自己的项目经验会更好，大厂的面试官更侧重于面试者对深层原理的理解，对于实习生来说一般面基础，如果有深查原理的习惯，个人的可塑造性也会较高

以下为面试中的一些知识点以及个人的一些补充，敲黑板啦啦

## 1. Tencent
#### 1.1. js 的事件机制
**事件阶段**

一般的，事件分为三个阶段：捕获阶段、目标阶段和冒泡阶段。

* 捕获阶段（Capture Phase）
　　事件的第一个阶段是捕获阶段。事件从文档的根节点流向目标对象节点。途中经过各个层次的DOM节点，并在各节点上触发捕获事件，直到到达事件的目标节点。捕获阶段的主要任务是建立传播路径，在冒泡阶段，事件会通过这个路径回溯到文档跟节点。
　　或这样描述：
　　任何事件产生时，如点击一个按钮，将从最顶端的容器开始（一般是html的根节点）。浏览器会向下遍历DOM树直到找到触发事件的元素，一旦浏览器找到该元素，事件流就进入事件目标阶段

* 目标阶段（Target Phase）
　　当事件到达目标节点的，事件就进入了目标阶段。事件在目标节点上被触发，然后会逆向回流，直到传播至最外层的文档节点。

* 冒泡阶段（Bubble Phase）
　　事件在目标元素上触发后，并不在这个元素上终止。它会随着DOM树一层层向上冒泡，回溯到根节点。
　　冒泡过程非常有用。它将我们从对特定元素的事件监听中释放出来，如果没有事件冒泡，我们需要监听很多不同的元素来确保捕获到想要的事件

**事件处理程序**
* DOM0 级事件处理程序
    ```js
    var btn5 = document.getElementById('btn5');
    btn5.onclick=function(){
       console.log(this.id);//btn5   
    };
    ```
    - 基于DOM0的事件，对于同一个dom节点而言，只能注册一个，后边注册的 同种事件 会覆盖之前注册的。
        利用这个原理我们可以解除事件，`btn5.onclick＝null;`其中this就是绑定事件的那个元素；
    - 以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理；

* DOM2 级事件处理程序
    - DOM2支持同一dom元素注册多个同种事件，事件发生的顺序按照添加的顺序依次触发（IE是相反的）。
    - DOM2事件通过addEventListener和removeEventListener管理
        ```js
        /* addEventListener(eventName,handlers,boolean);removeEventListener()
        * 两个方法都一样接收三个参数,第一个是要处理的事件名,第二个是事件处理程序,
        * 第三个值为false时表示在事件冒泡阶段调用事件处理程序,一般建议在冒泡阶段使用,
        * 特殊情况才在捕获阶段;
        */

        // 注意：通过addEventListener()添加的事件处理程序只能用removeEventListener()来移除
        // 并且移除时传入的参数必须与添加时传入的参数一样；比如

        var btn2 = document.getElementById('btn2');
        var handlers = function () {
            console.log(this.id);
        };

        btn2.addEventListener('click',handlers,false);

        btn2.removeEventListener('click',handlers.false);
        ```

    - ie 事件处理程序
        ```js
        //IE事件处理程序(IE和Opera支持)

        /* IE用了attachEvent(),detachEvent(),接收两个参数,事件名称和事件处理程序,
         * 通过attachEvent()添加的事件处理程序都会被添加到冒泡阶段,所以平时为了兼容更多的浏览器最好将事件添加到事件冒泡阶段,IE8及以前只支持事件冒泡;
         */

        var btn3 = document.getElementById('btn3');
        var handlers2=function(){
            console.log(this===window);//true,注意attachEvent()添加的事件处理程序运行在全局作用域;
        };
        btn3.attachEvent('onclick',handlers2);
        ```

##### ---ie 与其他浏览器的区别
**总结**
DOM事件模型中的事件对象常用属性:
* type用于获取事件类型
* target获取事件目标
* stopPropagation()阻止事件冒泡
* preventDefault()阻止事件默认行为
* 判断加载状态 —— onload 事件

IE事件模型中的事件对象常用属性:
* type用于获取事件类型
* srcElement获取事件目标
* cancelBubble 阻止事件冒泡
* returnValue 阻止事件默认行为
* 通过 readystate 属性值判断何时方法下载完毕可用
    readystate共有以下几个值：
    - uninitialized： 对象存在但未初始化；
    - loading：对象正在加载；
    - loaded：对象数据加载完毕；
    - interactive：可以操作对象了，但还没加载完毕；
    - complete：加载完毕。
    注意上面5个值并不一定每个事件都全包含，并且不一定是什么顺序。

    Document.readyState 属性
    一个文档的 readyState 可以是以下之一：
    - loading / 加载
        document 仍在加载。
    - interactive / 互动
        文档已经完成加载，文档已被解析，但是诸如图像，样式表和框架之类的子资源仍在加载。
    - complete / 完成
        T文档和所有子资源已完成加载。状态表示 load 事件即将被触发。

    当这个属性的值变化时，document 对象上的readystatechange 事件将被触发。


**事件对象**
* IE
    IE中事件对象是作为全局对象 `window.event` 存在的
* Firefox
    Firefox中则是做为句柄( handler )的第一个参数传入
* 通用
    `var evt = window.event || arguments[0];`

![event](/img/in-post/post-web-interview/event.png)

**事件监听**
- Chrome、FireFox、Opera、Safari、IE9.0及其以上版本
    ```js
    addEventListener(eventName,handler,boolean);
    removeEventListener()
    /* 两个方法都一样接收三个参数,
    * 事件名
    * 事件处理程序
    * boolean false时表示在事件冒泡阶段调用事件处理程序,一般建议在冒泡阶段使用
    */
    ```

    ![eventlistener](/img/in-post/post-web-interview/addEventListener.png)

- IE8.0及其以下版本
    ```js
    element.attachEvent(type, handler); 
    element.detachEvent(type, handler); 
    /* element  要绑定事件的对象，html 节点
    * type     事件类型 +'on' 如： "onclick, onmouseover"
    * listener 事件处理程序（只写函数名，不带括号）
    */
    ```

- 早期浏览器
    `obj['on' + type] = handler`

**阻止冒泡**
* `event.stopPropagation`
* `event.cancelBubble = true //IE`  

**阻止默认事件**
* `event.preventDefault()`
* `event.returnValue = false  //IE`

##### ---通用的事件监听器
```js
// event(事件)工具集，来源：github.com/markyun
markyun.Event = {
    // 页面加载完成后
    readyEvent: function (fn) {
        if (fn == null) {
            fn = document;
        }
        var oldonload = window.onload;
        if (typeof window.onload != 'function') {
            window.onload = fn;
        } else {
            window.onload = function () {
                oldonload();
                fn();
            };
        }
    },
    // 视能力分别使用dom0||dom2||IE方式 来绑定事件
    // 参数： 操作的元素,事件名称 ,事件处理程序
    addEvent: function (element, type, handler) {
        if (element.addEventListener) {
            //事件类型、需要执行的函数、是否捕捉
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent) {
            element.attachEvent('on' + type, function () {
                handler.call(element);
            });
        } else {
            element['on' + type] = handler;
        }
    },
    // 移除事件
    removeEvent: function (element, type, handler) {
        if (element.removeEnentListener) {
            element.removeEnentListener(type, handler, false);
        } else if (element.detachEvent) {
            element.detachEvent('on' + type, handler);
        } else {
            element['on' + type] = null;
        }
    },
    // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
    stopPropagation: function (ev) {
        if (ev.stopPropagation) {
            ev.stopPropagation();
        } else {
            ev.cancelBubble = true;
        }
    },
    // 取消事件的默认行为
    preventDefault: function (event) {
        if (event.preventDefault) {
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },
    // 获取事件目标
    getTarget: function (event) {
        return event.target || event.srcElement;
    },
    // 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
    getEvent: function (e) {
        var ev = e || window.event;
        if (!ev) {
            var c = this.getEvent.caller;
            while (c) {
                ev = c.arguments[0];
                if (ev && Event == ev.constructor) {
                    break;
                }
                c = c.caller;
            }
        }
        return ev;
    }
};
```


#### 1.2. vue
##### ---Vue 生命周期
##### ---双向绑定原理 & 如何实现
##### ---vuex 原理
##### ---vue 数据更新后执行
#### 1.3. 跨域
**什么叫跨域**

**方案**
#### 1.4. 安全 && 怎样预防
#### 1.5. session & cookie
#### 1.6. 本地存储
#### 1.7. 浏览器缓存
#### 1.8. 页面从输入URL 到加载过程
#### 1.9. HTTP 
##### ---content-type
* application/x-www-form-urlencoded
    > 最常见的 POST 提交数据的方式了。浏览器的原生 form 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded方式提交数据。 

    传递的key/val会经过URL转码，所以如果传递的参数存在中文或者特殊字符需要注意。
    ```js
    //例子
    //b=曹,a=1

    POST  HTTP/1.1(CRLF)
    Host: www.example.com(CRLF)
    Content-Type: application/x-www-form-urlencoded(CRLF)
    Cache-Control: no-cache(CRLF)
    (CRLF)
    b=%E6%9B%B9&a=1(CRLF)
    //这里b参数的值"曹"因为URL转码变成其他的字符串了
    ```

* multipart/form-data
    > 常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 form 的 enctyped 等于这个值
    并且Http协议会使用boundary来分割上传的参数

* text/xml
    ```xml
    //例子
    POST http://www.example.com HTTP/1.1(CRLF) 
    Content-Type: text/xml(CRLF)
    (CRLF)
    <?xml version="1.0"?>
    <resource>
        <id>123</id>
        <params>
            <name>
                <value>homeway</value>
            </name>
            <age>
                <value>22</value>
            </age>
        </params>
    </resource>
    ```

* application/json
    > 用来告诉服务端消息主体是序列化后的 JSON 字符串

    ```js
    //例子
    //传递json

    POST  HTTP/1.1(CRLF)
    Host: www.example.com(CRLF)
    Content-Type: application/json(CRLF)
    Cache-Control: no-cache(CRLF)
    Content-Length: 24(CRLF)
    (CRLF)
    {
        "a":1,
        "b":"hello"
    }
    ```

**(CRLF)指 `\r\n`**
参考： [HTTP常见Content-Type比较](http://blog.csdn.net/jekxi/article/details/54342789)
#### 1.10. get & post
#### 1.11. TCP & UDP & 握手
##### ---TCP (Transmission Control Protocol)
两个序号和三个标志位：
* 序号：seq序号，占32位，用来标识从TCP源端向目的端发送的字节流，发起方发送数据时对此进行标记。
* 确认序号：ack序号，占32位，只有ACK标志位为1时，确认序号字段才有效，ack=seq+1。

标志位：共6个，即URG、ACK、PSH、RST、SYN、FIN等，具体含义如下：
* URG：紧急指针（urgent poin* 有效。
* **ACK**：acknowledgement 确认序号有效。
* PSH：接收方应该尽快将这个报文交给应用层。
* RST：reset 重置连接。
* **SYN**：synchronous 建立联机,发起一个新连接。
* **FIN**：finish 释放一个连接。

需要注意的是：
* 不要将确认序号ack与标志位中的ACK搞混了。
* 确认方ack=发起方req+1，两端配对。

![三次握手](/img/in-post/post-web-interview/tcp.png)
1. 第一次握手：
    Client将标志位SYN置为1，随机产生一个值 seq=J，并将该数据包发送给Server
    Client进入SYN_SENT状态，等待Server确认。
2. 第二次握手：
    Server收到数据包后由标志位SYN=1知道Client请求建立连接，Server将标志位SYN和ACK都置为1，ack=J+1，随机产生一个值seq=K，并将该数据包发送给Client以确认连接请求，Server进入SYN_RCVD状态。
3. 第三次握手：
    Client收到确认后，检查ack是否为J+1，ACK是否为1，如果正确则将标志位ACK置为1，ack=K+1，并将该数据包发送给Server，Server检查ack是否为K+1，ACK是否为1，如果正确则连接建立成功，Client和Server进入ESTABLISHED状态，完成三次握手，随后Client与Server之间可以开始传输数据了

**为什么需要确认**

![tips](/img/in-post/post-web-interview/tips.png)

##### ---四次挥手
> 由于TCP连接时全双工的，因此，每个方向都必须要单独进行关闭，这一原则是当一方完成数据发送任务后，发送一个FIN来终止这一方向的连接，收到一个FIN只是意味着这一方向上没有数据流动了，即不会再收到数据了，但是在这个TCP连接上仍然能够发送数据，直到这一方向也发送了FIN

![tcp-transport](/img/in-post/post-web-interview/tcp-transport.jpg)

![tcp-bye](/img/in-post/post-web-interview/tcp-bye.png)

首先进行关闭的一方将执行主动关闭，而另一方则执行被动关闭，上图描述的即是如此。
* 第一次挥手：
    Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。
* 第二次挥手：
    Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态。
* 第三次挥手：
    Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。
* 第四次挥手：
    Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSED状态，完成四次挥手。

**为什么TIME_WAIT状态需要经过2MSL(最大报文段生存时间)才能返回到CLOSE状态？**
* 可靠的实现 TCP 全双工连接的终止
* 允许老的重复分节在网络中消失

![time](/img/in-post/post-web-interview/tcp-timewait.png)
*MSL是Maximum Segment Lifetime英文的缩写，中文可以译为“报文最大生存时间”，他是任何报文在网络上存在的最长时间，超过这个时间报文将被丢弃，RFC 793中规定MSL为2分钟，实际应用中常用的是30秒，1分钟和2分钟等。2MSL即两倍的MSL，TCP的TIME_WAIT状态也称为2MSL等待状态*

**为什么连接的时候是三次握手，关闭的时候却是四次握手？**
* 因为当Server端收到Client端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时
* 当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到我Server端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送。故需要四步握手。

参考： [TCP三次握手详解及释放连接过程](https://www.cnblogs.com/laowz/p/6947539.html)

#### 1.12. HTTP 加密
##### ---加密对象
对于HTTP协议来说，加密的对象有以下两个：
* 对通信的加密：
    HTTP中没有加密功能，但是可以通过和SSL(Secure Socket Layer，安全套接层)组合使用，加密通信内容。使用SSL建立安全通信线路后，就可以在这条线路上进行HTTP通信了。与SSL组合使用的HTTP被称为HTTPS（HTTP Secure，超文本传输安全协议）。
* 对通信内容本身进行加密
    即对HTTP报文里所包含的内容进行加密。这样，首先客户端要先对报文进行加密，然后再发给服务器。服务器在接受到请求时，需要对报文进行解密，再处理报文。该方式不同于SSL将整个通信线路进行加密处理，所以内容仍然有被篡改的风险。
    - A、任何人都可以发起请求
        HTTP协议中，并未有确认通信方这一步骤，所以，任何人都可以发送请求，而服务器在接受到任何请求时，都会做出相应的响应。
        - 解决方案：
        **查明对手的证书**
        虽然HTTP不能确认通信方，但SSL是可以的。SSL不仅提供了加密处理，还使用了"证书"的手段，可用于确认通信方。证书是由值得信赖的第三方机构颁布，可用于确定证明服务器和客户端是实际存在的。所以，只要能确认通信方持有的证书，即可判断通信方的真实意图。
    - B、无法判断报文是否完整（报文可能已遭篡改）
        HTTP协议无法判断报文是否被篡改，在请求或者响应发出后，在对方接收之前，即使请求或者响应遭到篡改是无法得知的。
        - 防止篡改：
            常用的，确定报文完整性方法：MD5、SHA-1 等 散列值校验方法，以及用来确认文件的数字签名方法。但是，使用这些方法，也无法百分百确保结果正确，因为MD5本身被修改的话，用户是没办法意识到得。

    为了有效防止这些弊端，可以采用HTTPS。
* POST 用户安全登陆
    在关系到用户隐私的时候，要时刻遵循两个原则：
    * 任何应用程序都不能在本地存储与安全相关的用户信息
    * 任何应用程序在向服务器传递数据的时候，都不能直接传递与安全相关的用户信息。

    要想让用户信息安全，就必须对其进行加密，让别人即便是拿到了安全信息，摆在眼前的也是一串乱码，没有半点用处

    MD5是一种常用的加密方法，它是一种散列函数，利用MD5对用户信息进行加密，会增加用户信息安全性。

    网上有关于MD5的第三方框架Category

    利用这个第三方框架可以实现对密码进行MD5加密

    +随机乱码字符防止被破解

##### ---加密算法
**对称加密**
![encryption](/img/in-post/post-web-interview/encryption.JPEG)

**非对称加密**
![encryption](/img/in-post/post-web-interview/encryption2.JPEG)

##### ---HTTPS 加密原理
> HTTPS简介
HTTPS其实是有两部分组成：HTTP + SSL / TLS，也就是在HTTP上又加了一层处理加密信息的模块。服务端和客户端的信息传输都会通过TLS进行加密，所以传输的数据都是加密后的数据

![https](/img/in-post/post-web-interview/https1.png)

* 服务器 用RSA生成公钥和私钥

* 把公钥放在证书里发送给客户端，私钥自己保存

* 客户端首先向一个权威的服务器检查证书的合法性，如果证书合法，客户端产生一段随机数，这个随机数就作为通信的密钥，我们称之为对称密钥，用公钥加密这段随机数，然后发送到服务器

* 服务器用密钥解密获取对称密钥，然后，双方就已对称密钥进行加密解密通信了

HTTPS在传输数据之前需要客户端（浏览器）与服务端（网站）之间进行一次握手，在握手过程中将确立双方加密传输数据的密码信息。TLS/SSL协议不仅仅是一套加密传输的协议，更是一件经过艺术家精心设计的艺术品，TLS/SSL中使用了非对称加密，对称加密以及HASH算法。握手过程的具体描述如下：

1. 浏览器将自己支持的一套加密规则发送给网站。 
2. 网站从中选出一组加密算法与HASH算法，并将自己的身份信息以证书的形式发回给浏览器。证书里面包含了网站地址，加密公钥，以及证书的颁发机构等信息。 
3. 浏览器获得网站证书之后浏览器要做以下工作： 
a) 验证证书的合法性（颁发证书的机构是否合法，证书中包含的网站地址是否与正在访问的地址一致等），如果证书受信任，则浏览器栏里面会显示一个小锁头，否则会给出证书不受信的提示。 
b) 如果证书受信任，或者是用户接受了不受信的证书，浏览器会生成一串随机数的密码，并用证书中提供的公钥加密。 
c) 使用约定好的HASH算法计算握手消息，并使用生成的随机数对消息进行加密，最后将之前生成的所有信息发送给网站。 
4. 网站接收浏览器发来的数据之后要做以下的操作： 
a) 使用自己的私钥将信息解密取出密码，使用密码解密浏览器发来的握手消息，并验证HASH是否与浏览器发来的一致。 
b) 使用密码加密一段握手消息，发送给浏览器。 
5. 浏览器解密并计算握手消息的HASH，如果与服务端发来的HASH一致，此时握手过程结束，之后所有的通信数据将由之前浏览器生成的随机密码并利用对称加密算法进行加密。

参考：[图解HTTPS](http://www.cnblogs.com/zhuqil/archive/2012/07/23/2604572.html)

#### 如何保证 HTTP 传输安全性
* 重要的数据，要加密
    比如用户名密码（如果简单的md5，是可以暴力破解），常见的是 md5(不可逆)，aes（可逆），自由组合,还可以加一些特殊字符
    举例：username = aes(username), pwd = MD5(pwd + username)

* 非重要数据，要签名
    签名的目的是为了防止篡改，比如http://www.xxx.com/getnews?id=1，获取id为1的新闻，如果不签名那么通过id=2,就可以获取2的内容等等。怎样签名呢？
    通常使用sign，比如原链接请求的时候加一个sign参数，sign=md5(id=1)，服务器接受到请求，验证sign是否等于md5(id=1)，如果等于说明正常请求。
    这会有个弊端，假如规则被发现，那么就会被伪造，所以适当复杂一些，还是能够提高安全性的。

* 登录态怎么做
    http是无状态的，也就是服务器没法自己判断两个请求是否有联系，那么登录之后，以后的接口怎么判定是否登录呢
    简单的做法，在数据库中存一个token字段（名字随意），当用户调用登陆接口成功的时候，就将该字段设一个值，（比如aes(过期时间)），同时返回给前端，以后每次前端请求带上该值，服务器首先校验是否过期，其次校验是否正确，不通过就让其登陆。（redis 做这个很方便哦，key有过期时间）

来自：[如何保证http传输安全性](http://blog.csdn.net/jt521xlg/article/details/49717571)

#### 1.13. 排序：冒泡，选择，快速
#### 1.14. 数据库
##### ---触发器
> 一种特殊的存储过程，存储过程一般通过定义的名字直接调用，而触发器是通过增、删、改进行触发执行的。会在事件发生时自动强制执行

触发器是一种特殊的存储过程，主要是通过事件来触发而被执行的。它可以强化约束，来维护数据的完整性和一致性，可以跟踪数据库内的操作从而不允许未经许可的更新和变化。可以联级运算。如，某表上的触发器上包含对另一个表的数据操作，而该操作又会导致该表触发器被触发。

##### ---事务 & 锁
* 事务
    就是被绑定在一起作为一个逻辑工作单元的SQL语句分组，如果任何一个语句操作失败那么整个操作就被失败，以后操作就会回滚到操作前状态，或者是上有个节点。
    为了确保要么执行，要么不执行，就可以使用事务。要将一组语句作为事务考虑，就需要通过ACID测试，即原子性，一致性，隔离性和持久性。
* 锁：
    在所有的DBMS中，锁是实现事务的关键，锁可以保证事务的完整性和并发性。与现实生活中锁一样，它可以使某些数据的拥有者，在某段时间内不能使用某些数据或数据结构。当然锁还分级别的。共享锁（只读不写）、排他锁（可读可写） 


#### 1.15. 软件设计模式
设计原则
* 对接口编程而不是对实现编程
* 优先使用对象组合而不是继承

![design](/img/in-post/post-web-interview/design.png)
![design-rule](/img/in-post/post-web-interview/design-rule.png)
##### ---单例模式
> 单体是一个用来划分命名空间并将一批相关的属性和方法组织在一起的对象，如果他可以被实例化，那么他只能被实例化一次

```js
// 对象字面量
var Singleton = {
    attr1: 1,
    attr2: 2,
    method1: function(){
        return this.attr1;
    },
    method2: function(){
        return this.attr2;
    }
};

/* 上面的所有成员变量都是通过Singleton来访问的，但是它并不是单体模式；
    * 因为单体模式还有一个更重要的特点，就是可以仅被实例化一次，上面的只是不能被实例化的一个类，因此不是单体模式；对象字面量是用来创建单体模式的方法之一；
    */

/*要实现一个单体模式的话，我们无非就是使用一个变量来标识该类是否被实例化
如果未被实例化的话，那么我们可以实例化一次，否则的话，直接返回已经被实例化的对象
*/

// 单体模式
var Singleton = function(name){
    this.name = name;
    this.instance = null;
};
Singleton.prototype.getName = function(){
    return this.name;
}
// 获取实例对象
function getInstance(name) {
    if(!this.instance) {
        this.instance = new Singleton(name);
    }
    return this.instance;
}
// 测试单体模式的实例
var a = getInstance("aa");  
var b = getInstance("bb");

console.log(a === b)        // true
console.log(a.getName())    // aa
console.log(b.getName())    // aa
```
**应用案例**
> 弹窗
传统创建：比如我点击一个元素需要创建一个div，我点击第二个元素又会创建一次div，我们频繁的点击某某元素，他们会频繁的创建div的元素，虽然当我们点击关闭的时候可以移除弹出代码，但是呢我们频繁的创建和删除并不好，特别对于性能会有很大的影响，对DOM频繁的操作会引起重绘等，从而影响性能；因此这是非常不好的习惯；我们现在可以使用单体模式来实现弹窗效果，我们只实例化一次就可以

**编写通用的单体模式**
> 我们使用一个参数fn传递进去，如果有result这个实例的话，直接返回，否则的话，当前的getInstance函数调用fn这个函数，是this指针指向与这个fn这个函数；之后返回被保存在result里面；现在我们可以传递一个函数进去，不管他是创建div也好，还是创建iframe也好，总之如果是这种的话，都可以使用getInstance来获取他们的实例对象；

```js
// 创建div
var createWindow = function(){
    var div = document.createElement("div");
    div.innerHTML = "我是弹窗内容";
    div.style.display = 'none';
    document.body.appendChild(div);
    return div;
};
// 创建iframe
var createIframe = function(){
    var iframe = document.createElement("iframe");
    document.body.appendChild(iframe);
    return iframe;
};
// 获取实例的封装代码
var getInstance = function(fn) {
    var result;
    return function(){
        return result || (result = fn.call(this,arguments));
    }
};
// 测试创建div
var createSingleDiv = getInstance(createWindow);
document.getElementById("Id").onclick = function(){
    var win = createSingleDiv();
    win.style.display = "block";
};
// 测试创建iframe
var createSingleIframe = getInstance(createIframe);
document.getElementById("Id").onclick = function(){
    var win = createSingleIframe();
    win.src = "http://cnblogs.com";
};
```

##### ---以下为补充
##### ---工厂模式
> 客户类和工厂类分开。消费者任何时候需要某种产品，只需向工厂请求即可。消费者无须修改就可以接纳新产品。

工厂模式是为了解决多个类似对象声明的问题;也就是为了解决实列化对象产生重复的问题。
* 优点：能解决多个相似的问题。
* 缺点：
    - 不能知道对象识别的问题(对象的类型不知道)。
    - 当产品修改时，工厂类也要做相应的修改。
        如：如何创建及如何向客户端提供。

```js
function CreatePerson(name,age,sex) {
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.sex = sex;
    obj.sayName = function(){
        return this.name;
    }
    return obj;
}
var p1 = new CreatePerson("longen",'28','男');
var p2 = new CreatePerson("tugenhua",'27','女');
```

##### ---模块模式
> 模块模式的思路是为单体模式添加私有变量和私有方法能够减少全局变量的使用

prototype + constructor

##### ---装饰者模式
> 装饰者(decorator)模式能够在不改变对象自身的基础上，在程序运行期间给对像动态的添加职责（方法或属性）。
与继承相比，装饰者是一种更轻便灵活的做法。

可以动态的给某个对象添加额外的职责，而不会影响从这个类中派生的其它对象。
```js
// ES7装饰器
function isAnimal(target) {
    target.isAnimal = true
    return target
}

// 装饰器
@isAnimal
class Cat {
    // ...
}
console.log(Cat.isAnimal)    // true

// 作用于类属性的装饰器：
function readonly(target, name, descriptor) {
    discriptor.writable = false
    return discriptor
}
class Cat {
    @readonly
    say() {
        console.log("meow ~")
    }
}

var kitty = new Cat()
kitty.say = function() {
    console.log("woof !")
}
kitty.say()    // meow ~
```

##### ---观察者模式（发布-订阅）
> 发布---订阅模式又叫观察者模式，它定义了对象间的一种一对多的关系，让多个观察者对象同时监听某一个主题对象，当一个对象发生改变时，所有依赖于它的对象都将得到通知

发布订阅模式的流程如下：
1. 确定谁是发布者(比如我的博客)。
2. 然后给发布者添加一个缓存列表，用于存放回调函数来通知订阅者。
3. 发布消息，发布者需要遍历这个缓存列表，依次触发里面存放的订阅者回调函数。
4. 退订（比如不想再接收到这些订阅的信息了，就可以取消掉）

**【实现事件模型】**
> 即写一个类或是一个模块，有两个函数，一个bind一个trigger，分别实现绑定事件和触发事件，核心需求就是可以对某一个事件名称绑定多个事件响应函数，然后触发这个事件名称时，依次按绑定顺序触发相应的响应函数。

大致实现思路就是创建一个类或是匿名函数，在bind和trigger函数外层作用域创建一个字典对象，用于存储注册的事件及响应函数列表，bind时，如果字典没有则创建一个，key是事件名称，value是数组，里面放着当前注册的响应函数，如果字段中有，那么就直接push到数组即可。trigger时调出来依次触发事件响应函数即可
```js
var Event = (function(){
    var list = {},
        listen,
        trigger,
        remove;
        listen = function(key,fn){
            if(!list[key]) {
                list[key] = [];
            }
            list[key].push(fn);
        };
        trigger = function(){
            var key = Array.prototype.shift.call(arguments),
                fns = list[key];
            if(!fns || fns.length === 0) {
                return false;
            }
            for(var i = 0, fn; fn = fns[i++];) {
                fn.apply(this,arguments);
            }
        };
        remove = function(key,fn){
            var fns = list[key];
            if(!fns) {
                return false;
            }
            if(!fn) {
                fns && (fns.length = 0);
            }else {
                for(var i = fns.length - 1; i >= 0; i--){
                    var _fn = fns[i];
                    if(_fn === fn) {
                        fns.splice(i,1);
                    }
                }
            }
        };
        return {
            listen: listen,
            trigger: trigger,
            remove: remove
        }
})();

// 测试代码如下：
Event.listen("color",function(size) {
    console.log("尺码为:"+size); // 打印出尺码为42
});
Event.trigger("color",42);
```

##### ---代理模式
> 代理是一个对象，它可以用来控制对本体对象的访问，它与本体对象实现了同样的接口，代理对象会把所有的调用方法传递给本体对象的
本地对象注重的去执行页面上的代码，代理则控制本地对象何时被实例化，何时被使用

**优点：**
* 代理对象可以代替本体被实例化，并使其可以被远程访问；
* 它还可以把本体实例化推迟到真正需要的时候；对于实例化比较费时的本体对象，或者因为尺寸比较大以至于不用时不适于保存在内存中的本体，我们可以推迟实例化该对象；

```js
// 先申明一个奶茶妹对象
var TeaAndMilkGirl = function(name) {
    this.name = name;
};
// 这是京东ceo先生
var Ceo = function(girl) {
    this.girl = girl;
    // 送结婚礼物 给奶茶妹
    this.sendMarriageRing = function(ring) {
        console.log("Hi " + this.girl.name + ", ceo送你一个礼物：" + ring);
    }
};
// 京东ceo的经纪人是代理，来代替送
var ProxyObj = function(girl){
    this.girl = girl;
    // 经纪人代理送礼物给奶茶妹
    this.sendGift = function(gift) {
        // 代理模式负责本体对象实例化
        (new Ceo(this.girl)).sendMarriageRing(gift);
    }
};
// 初始化
var proxy = new ProxyObj(new TeaAndMilkGirl("奶茶妹"));
proxy.sendGift("结婚戒"); // Hi 奶茶妹, ceo送你一个礼物：结婚戒
```

* TeaAndMilkGirl 是一个被送的对象(这里是奶茶妹)；
* Ceo 是送礼物的对象，他保存了奶茶妹这个属性，及有一个自己的特权方法sendMarriageRing 就是送礼物给奶茶妹这么一个方法；
* 然后呢他是想通过他的经纪人去把这件事完成，于是需要创建一个经济人的代理模式，名字叫ProxyObj ；
* 他的主要做的事情是，把ceo交给他的礼物送给ceo的情人，因此该对象同样需要保存ceo情人的对象作为自己的属性，同时也需要一个特权方法sendGift ，该方法是送礼物，因此在该方法内可以实例化本体对象，这里的本体对象是ceo送花这件事情，因此需要实例化该本体对象后及调用本体对象的方法(sendMarriageRing).

理解使用虚拟代理实现图片的预加载

在网页开发中，图片的预加载是一种比较常用的技术，如果直接给img标签节点设置src属性的话，如果图片比较大的话，或者网速相对比较慢的话，那么在图片未加载完之前，图片会有一段时间是空白的场景，这样对于用户体验来讲并不好，那么这个时候我们可以在图片未加载完之前我们可以使用一个loading加载图片来作为一个占位符，来提示用户该图片正在加载，等图片加载完后我们可以对该图片直接进行赋值即可；下面我们先不用代理模式来实现图片的预加载的情况下代码如下：
```js
// 不使用代理的预加载图片函数如下
var myImage = (function(){
    var imgNode = document.createElement("img");
    document.body.appendChild(imgNode);
    var img = new Image();
    img.onload = function(){
        imgNode.src = this.src;
    };
    return {
        setSrc: function(src) {
            imgNode.src = "http://img.lanrentuku.com/img/allimg/1212/5-121204193Q9-50.gif";
            img.src = src;
        }
    }
})();
// 调用方式
myImage.setSrc("https://img.alicdn.com/tps/i4/TB1b_neLXXXXXcoXFXXc8PZ9XXX-130-200.png");
```

```js
//利用代理模式来编写预加载图片
var myImage = (function(){
    var imgNode = document.createElement("img");
    document.body.appendChild(imgNode);
    return {
        setSrc: function(src) {
            imgNode.src = src;
        }
    }
})();

// 代理模式
var ProxyImage = (function(){
    var img = new Image();
    img.onload = function(){
        myImage.setSrc(this.src);
    };
    return {
        setSrc: function(src) {
                    myImage.setSrc("http://img.lanrentuku.com/img/allimg/1212/5-121204193Q9-50.gif");
                    img.src = src;
        }
    }
})();
// 调用方式
ProxyImage.setSrc("https://img.alicdn.com/tps/i4/TB1b_neLXXXXXcoXFXXc8PZ9XXX-130-200.png");
```

这种懒加载方法不用代理模式也是可以实现的，只是用代理模式。我们可以让 myImage 只做一件事，只负责将实际图片加入到页面中，而loading图片交给ProxyImage去做。从而降低代码的耦合度。因为当我不想用loading的时候，可以直接调用myImage 方法。也即是说假如我门不需要代理对象的话，直接可以换成本体对象调用该方法即可
**对比**
* 不代理：不满足单一职责原则，代码耦合度高
* myimage 函数只负责一件事，其他交给代理

**优点**
* 用户可以放心地请求代理，他们只关心是否能得到想要的结果。假如我门不需要代理对象的话，直接可以换成本体对象调用该方法即可。
* 在任何使用本体对象的地方都可以替换成使用代理。


参考：[Javascript设计模式详解](http://www.cnblogs.com/tugenhua0707/p/5198407.html)

#### 1.2. Online Coding
js 实现两个超大数相加
基础：
* JS 中所有的数字类型，实际存储都是通过 8 字节 double 浮点型 表示的，并不是能够精确表示范围内的所有数
* 大整数存储（安全使用范围）
    - 其他语言 `2^63 - 1`
    - js  `Math.pow(2, 53) - 1`
        ```js
        //js 最大和最小安全值
        Number.MAX_SAFE_INTEGER  //9007199254740991
        Number.MIN_SAFE_INTEGER  //-9007199254740991
        ```

```js
var largeNumberAdd = function(num1, num2) {
    var arr1 = num1.split(''),
        arr2 = num2.split(''),
        tem = '',
        num3 = 0,
        result = []
    var longDiff = arr1.length - arr2.length
    if (longDiff > 0) {
        for (let i = 0; i < longDiff; i++) {
            arr2.unshift('0')            
        }
    }else if (longDiff < 0) {
        for (let i = 0; i < Math.abs(longDiff); i++) {
            arr1.unshift('0')
        }
    }
    for (let i = arr1.length - 1; i >= 0; i--) {
        tem = parseInt(arr1[i]) + parseInt(arr2[i]) + num3
        // check if tem > 10
        if (tem >= 10) {
            num3 = 1
            result.push((tem + '')[1])
        }else {
            num3 = 0
            result.push(tem)
        }
    }
    return result.reverse().join('')
}

// console.log(largeNumberAdd('11111','11111'))
console.log(largeNumberAdd('00000000000000000000011111','333331999'))
console.log(11111+333331999)
// console.log(largeNumberAdd('3333333333333333333333333333333311111111111111111111111111111111111111','333333333333333331111111111111111111111111111166666666666666'))
```

js 每秒钟的计算量
js 如何解析后台返回的超大数据
前提：
* js 用浮点数表示所有64位数字，所有达到 2^53 的可以被精确表示，更大的数字都会被裁剪，——如何表示64位数字
虽然js 能够解析进制数字表示64位数字，但底层的数字表示不支持 64 位
在浏览器中执行以下代码
```html
<html>
  <head>
    <script language="javascript">
      function showPrecisionLimits() {
        document.getElementById("r50").innerHTML = 0x0004000000000001 - 0x0004000000000000;
        document.getElementById("r51").innerHTML = 0x0008000000000001 - 0x0008000000000000;
        document.getElementById("r52").innerHTML = 0x0010000000000001 - 0x0010000000000000;
        document.getElementById("r53").innerHTML = 0x0020000000000001 - 0x0020000000000000;
        document.getElementById("r54").innerHTML = 0x0040000000000001 - 0x0040000000000000;
      }
    </script>
  </head>
  <body onload="showPrecisionLimits()">
    <p>(2^50+1) - (2^50) = <span id="r50"></span></p>
    <p>(2^51+1) - (2^51) = <span id="r51"></span></p>
    <p>(2^52+1) - (2^52) = <span id="r52"></span></p>
    <p>(2^53+1) - (2^53) = <span id="r53"></span></p>
    <p>(2^54+1) - (2^54) = <span id="r54"></span></p>
  </body>
</html>
```
在Firefox，Chrome和IE浏览器中，可以看到，如果能够存储64位数字，则以下减法结果皆为1。而结果相反，可以看到2 ^ 53 + 1和2 ^ 53 间的差异丢失
```js
（2 ^ 50 + 1） - （2 ^ 50）= 1
（2 ^ 51 + 1） - （2 ^ 51）= 1
（2 ^ 52 + 1） - （2 ^ 52）= 1
（2 ^ 53 + 1） - （2 ^ 53）= 0
（2 ^ 54 + 1） - （2 ^ 54）= 0
```

位运算
因此，我们可以选择用两个 32 位的数字表示 64 位整数，然后进行按位与
```js
var a = [ 0x0000ffff, 0xffff0000 ];
var b = [ 0x00ffff00, 0x00ffff00 ];
var c = [ a[0] & b[0], a[1] & b[1] ];

document.body.innerHTML = c[0].toString(16) + ":" + c[1].toString(16);

//结果
ff00:ff0000
```

#### 网络安全
前端网络安全的实现
* 保证http传输安全性

如何检测恶意脚本
如何屏蔽

## 2. 阿里
1. 简单介绍一下自己
2. 问题
    * HTTP 相关
        HTTP 与 HTTPS 区别，HTTPS 原理，如何加密
    * 谈谈闭包
    * 谈谈作用域链
    * 常用的跨域方式
    * vue
        - 特点
        - 生命周期
        - vuex
            实现原理（事件绑定）-如何实现
        - 与 react 的不同
            应用场景
        - 如何实现双向绑定
        - 如何通信
3. 其他
    * 还会哪些语言
    * 还有什么感觉没问到但掌握很好的
    * 是否还有其他的问题
    * 有什么问题想要问的



#### 2.1. 编写一个 css 层级选择器
根据一个给定的元素生成一个css 选择器，函数名为genCssSelector ，
点击某元素弹出该元素及其父元素，类似 querySelector
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>Document</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script language="javaScript">
        // your code here
        var genCssSelector = function (e) {
            e = e || window.event
            var tar = e.target || e.srcElement
            var objArr = []

            while (tar) {
                if (tar.className) {
                    objArr.push('.' + tar.className)
                } else if (tar.id) {
                    objArr.push('#' + tar.id)
                } else {
                    objArr.push(tar.nodeName.toLowerCase())
                }
                tar = tar.parentNode
            }
            objArr.pop()
            return objArr.reverse().join(' ')
        }

        document.addEventListener('click', function (e) {
            //点击li时，返回：html body #page .content.main .refer ul li 
            console.log(genCssSelector(e));
        })
    </script>
</head>
<body>
    <div id="page">
        <div class="main">
            <div class="reference">
                <ul>
                    <li></li>
                    <li></li>
                    23333
                </ul>
            </div>
        </div>
    </div>
</body>
</html>
```
