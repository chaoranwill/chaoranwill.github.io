---
layout:     post
title:      "Questions of FE "
subtitle:   "collected from nowcoder and blogs"
date:       2018-03-01 19:55:00
author:     "Chaoran"
header-img: "img/post-bg-fe-topics.jpeg"
noToc:      true
tags:
    - 前端开发
---

> “To be is to be perceived. ”

* 目录
{:toc #toc}

[Interview-Notebook](https://github.com/chaoranwill/Interview-Notebook)

## 1. HTML
#### 1.1. html5
> Html5是指的一系列新的API，或者说新规范，新技术

> HTML5指的是包括 HTML 、 CSS 和 JavaScript 在内的一套技术组合。它希望能够减少网页浏览器对于需要插件的丰富性网络应用服务（ Plug-in-Based Rich Internet Application ， RIA ），例如： AdobeFlash 、 Microsoft Silverlight 与 Oracle JavaFX 的需求，并且提供更多能有效加强网络应用的标准集。

**对WEB标准以及W3C的理解与认识**
标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率、使用外 链css和 js 脚本、结构行为表现的分离、文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，容易维 护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性


HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
1. 拖拽释放(Drag and drop) API 
2. 语义化更好的内容标签（header,nav,footer,aside,article,section）
3. 音频、视频API(audio,video)
4. 画布(Canvas) API
5. 地理(Geolocation) API
6. 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
7. sessionStorage 的数据在浏览器关闭后自动删除
8. 表单控件，calendar、date、time、email、url、search  
9. 新的技术webworker, websocket, Geolocation

**webworker**
- 为了利用多核 CPU 的计算能力，在 HTML5 中引入的工作线程使得浏览器端的 JavaScript 引擎可以并发地执行 JavaScript 代码，从而实现了对浏览器端多线程编程的良好支持。
- Web Worker 允许 JavaScript 脚本创建多个线程，但是子线程完全受主线程控制，可以用来加载和运行特定的JavaScript文件，这个新的线程和主线程之间并不会互相影响和阻塞执行，且**不得操作 DOM** 。所以，这个新标准并没有改变 JavaScript 单线程的本质。

**移除的元素：**
1. 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
2. 对可用性产生负面影响的元素：frame，frameset，noframes；

#### 1.2. 语义化
1. 去掉或者丢失样式的时候能够让页面呈现出清晰的结构
2. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
3. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
4. 便于团队开发和维护，语义化使得网页更具可读性，是进一步开发网页的必要步骤，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

#### 1.3. Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?
1. <!DOCTYPE> 声明位于文档中的最前面，处于 html 标签之前。告知浏览器以何种模式来渲染文档 
    * 声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。
2. 严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。
3. 在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
4. DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。

#### 1.4. 块与行内元素
标准文档流里面，块级元素：
`div  , p  , form,   ul,  li ,  ol, dl, h1-h6,   address,  fieldset,  hr, menu,  table`
* 总是在新行上开始，占据一整行；
* 高度，行高以及外边距和内边距都可控制；
* 默认宽度填满父元素宽度，与内容无关；
* 它可以容纳内联元素和其他块元素。

**行内元素：**
`span,   strong,   em,  br,  img ,  input,  label,  select,  textarea,  cite`
* 和其他元素都在一行上；
* 高，行高及外边距和内边距部分可改变；
* 宽度只与内容有关；
* 行内元素只能容纳文本或者其他行内元素。
* 不可以设置宽高，其宽度随着内容增加，高度随字体大小而改变
* 内联元素可以设置外边界，水平方向起作用，竖直方向无作用

**replaced  和 non-replaced**
默认具有 CSS 格式化外表范围的元素，比如 img 元素，有自己的宽和高
`input，textarea，select`

#### 1.5. iframe的优缺点？
**优点：**
1. 解决加载缓慢的第三方内容如图标和广告等的加载问题
2. Security sandbox
3. 并行加载脚本
4. 方便页面的部分修改
5. 重载时减少数据传输

**缺点：**
1. iframe会阻塞主页面的Onload事件
2. 即时内容为空，加载也需要时间
3. 没有语意，不利于SEO，搜索引擎不容易解读
4. 浏览器后退无效
5. IFRAME销毁是无法全部释放内存，容易导致内存泄漏

如果需要使用 iframe ，最好是通过 javascript动态给iframe添加 src 属性值
**可用 Ajax 代替iframe** 

#### 1.6. 浏览器内多个标签页之间的通信
> sessionStorage 和 localStorage 是 HTML5 Web Storage API 提供的，可以方便的在 web 请求之间保存数据。有了本地数据，就可以避免数据在浏览器和服务器间不必要地来回传递
h5 新方法：`postMessage`

**通信方式：**
* localStorge & sessionStorage
    > 利用了 localStorage 的增删改事件监听

    sessionStorage 是在同源的同窗口（或 tab ）中，始终存在的数据。也就是说只要这个浏览器窗口没有关闭，即使刷新页面或进入同源另一页面，数据仍然存在。关闭窗口后， sessionStorage 即被销毁。同时“独立”打开的不同窗口，即使是同一页面

    ```js
    //页面A发送事件
    function sendMsg(text) {
        window.localStorage.setItem('msg',text);
    }

    //页面B接收事件 (localstorage 被添加、修改或删除时，它都会触发一个事件，可监听事件)
    window.addEventListener('storage', function (evt) {
        if(evt.key==='msg')
        console.log(evt.newValue);
    });

    //需要注意的是重复设置相同的键值不会再次触发事件
    ```
    **localstorage不能存对象。 如果传递对象就先转成字符串。 然后取值的时候再转成对象。**

* cookie+setInterval
    > 将要传递的信息存储在cookie里面，然后每隔一定时间读取cookie信息来实现

    ```js
    //a页面
    var mess=document.getElementById("butOk").value();    
    document.cookie="mess="+mess;
    //b页面
    //获取Cookie天的内容  
    function getKey(key) {  
        return JSON.parse("{\""+ document.cookie.replace(/;\s+/gim,"\",\"").replace(/=/gim, "\":\"") +"\"}")[key];  
    }  
    //每隔1秒获取Cookie的内容  
    setInterval(function(){  
        console.log(getKey("mess"));  
    },1000); 
    ```

* postMessage
    用于在两个窗口间发送消息
    ```js
    win.postMessage(data, origin)

    // win 这个参数为需要接受消息的 window 对象
    // 当我们通过 window.open() 打开一个新窗口时，会返回一个新窗口的 window 对象，通过这个新窗口的 window 对象，就可以向新窗口发送消息
    // 如果页面中有 frame 时，也可以通过这个 frame 对象发送消息

    // data 为我们想要发送的数据，理论上 data 可以是任何可以被复制的数据类型，但是由于部分浏览器只支持传输 String 类型，所以传输的数据最好是通过 JSON.stringify() 序列化后再传输

    // origin 为字符串，为目标窗口的源，由 协议+ip/域名+端口号 组成
    // 如果想要传递给任意窗口，可以将这个参数设置为 * ，为了安全起见，不建议设置为 *
    // 如果目标窗口与当前窗口同源，则设置为 /
    ```

    数据接收
    ```js
    window.addEventListener('message', function (e) {...})

    // 第一个参数为这个事件监听器的类型，'message' 表示会监听当前窗口接收到的消息
    // 第二个参数为接收到消息后的回调函数，在回调函数中，我们可以对发送消息的源进行一些验证，从而保证安全性
    // 回调函数参数 e 上有很多属性，我们可以将其打印出来，其中 origin 表示发送消息窗口的源；source 属性表示发送消息的窗口
    // 通过 e.source == window.opener 可以判断发送消息的窗口与打开当前页面的窗口是否为同一个；data 属性标书传递过来的数据
    ```

    **安全**

    - 在必要时，可以在接收窗口验证Domian，甚至验证URL，以防止来自非法页面的消息。这实际上是在代码中实现一次同源策略的验证过程。
    - 接收的消息写入textContent，但在实际应用中，如果将消息写入innerHtml，甚至直接写入script中，则可能会导致DOM based XSS的产生。在接受窗口不应该信任接收到的消息，而需要对信息进行安全检查。

**特征**
* Cookie
    - 每个域名存储量比较小（各浏览器不同，大致 4K ）
    - 所有域名的存储量有限制（各浏览器不同，大致 4K ）
    - 有个数限制（各浏览器不同）
    - 会随请求发送到服务器

* LocalStorage
    - 永久存储
    - 单个域名存储量比较大（推荐 5MB ，各浏览器不同）
    - 总体数量无限制

* SessionStorage
    - 只在 Session 内有效
    - 存储量更大（推荐没有限制，但是实际上各浏览器也不同）

#### 1.7. cookie & session
>  由于HTTP协议是无状态的协议，所以服务端需要记录用户的状态时，就需要用某种机制来识具体的用户，这个机制就是Session

* session 在服务器端，cookie 在客户端（浏览器）
* session 默认被存在在服务器的一个文件里（不是内存）
* session 的运行依赖 session id，而 session id 是存在 cookie 中的，也就是说，如果浏览器禁用了 cookie ，同时 session 也会失效（但是可以通过其它方式实现，比如在 url 中传递 session_id）
* session 可以放在 文件、数据库、或内存中都可以。
* 用户验证这种场合一般会用 session 因此，维持一个会话的核心就是客户端的唯一标识，即 session id
* cookie 可以随HTTP请求发送给后端

#### 1.8. `data-`属性的作用是什么
`data-`为H5新增的为前端开发者提供自定义的属性，这些属性集可以通过对象的 `dataset` 属性获取，不支持该属性的浏览器可以通过 `getAttribute` 方法获取 :


需要注意的是：`data-`之后的以连字符分割的多个单词组成的属性，获取的时候使用驼峰风格。 所有主流浏览器都支持 data-* 属性。
即：当没有合适的属性和元素时，自定义的 data 属性是能够存储页面或 App 的私有的自定义数据。

#### 1.9. 浏览器内核
主要分成两部分：
* 渲染引擎(layout engineer或 Rendering Engine)：
    负责取得网页的内容（HTML、 XML 、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。

* JS引擎则：
    解析和执行 javascript 来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。

浏览器 | 内核 | 前缀 | js 引擎
-| :-: | -:  | -: 
IE(360, 搜狗浏览器) | Trident | -ms- | Chakra
Chrome | Webkit | -webkit- | V8 
Safari | Webkit | -webkit- | Javascriptcore
Opera | Presto | -o- | Carakan
FireFox | gecko | -moz- |

#### 1.10. src && href
* src
    - 用于替换当前元素
    - src是 source 的缩写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求 src 资源时会将其指向的资源下载并应用到文档内
    例如 js 脚本， img 图片和 frame 等元素
    - `<script src ='js.js'></script>`
    当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。
    
* href 
    - 用于在当前文档和引用资源之间确立联系
    - href是 Hypertext Reference 的缩写，指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接
    如果我们在文档中添加 `<link href='common.css' rel='stylesheet'/>`
    那么浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。这也是为什么建议使用 link 方式来加载 css ，而不是使用 @import 方式。

#### 1.11. viewport
```js
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />

// width    设置viewport宽度，为一个正整数，或字符串‘device-width’
// device-width  设备宽度
// height   设置viewport高度，一般设置了宽度，会自动解析出高度，可以不用设置
// initial-scale    默认缩放比例（初始缩放比例），为一个数字，可以带小数
// minimum-scale    允许用户最小缩放比例，为一个数字，可以带小数
// maximum-scale    允许用户最大缩放比例，为一个数字，可以带小数
// user-scalable    是否允许手动缩放
```

#### 1.12. BigPipe
[bigpipe 实现原理](http://www.mamicode.com/info-detail-1115810.html)


## 2. CSS
#### 2.1. CSS3有哪些新特性
1. CSS3实现圆角（`border-radius`），阴影（`box-shadow`），
2. 对文字加特效（`text-shadow`），线性渐变（`gradient`），旋转（`transform`）
3. `transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg)`
    
    旋转,缩放,定位,倾斜
4. 增加了更多的CSS选择器  多背景 `rgba`
5. 在CSS3中唯一引入的伪类是 `::selection`.
6. 媒体查询，多栏布局
7. `border-image`

#### 2.2. CSS中 使用方式及其区别？
1. 内联式
    直接用在标签上，维护成本高
2. 样式块
    页面较为清晰，但不能被其他页面使用
3. 外链式 -link
    XHTML标签。css，html代码分离，便于代码重复使用
4. 外部导入式-import
    CSS标签。可以在一个样式块中导入多个样式表，类似外链

**link import区别**
* link属于 XHTML 标签，除了加载CSS外，还可以定义RSS等其他事务；而 @import 是 CSS 提供的,只能加载CSS
* 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载
* link是html标签，因此没有兼容性，而@import只有IE5以上才能识别
* link方式样式的权重高于@import的

更多： [link 与 @import之对比](http://www.cnblogs.com/chaoran/p/4783933.html)

#### 2.3. FOUC（无样式内容闪烁）
>FOUC - Flash Of Unstyled Content 文档样式闪烁

```html
<style type="text/css" media="all">@import "../fouc.css";</style> 
```

引用CSS文件的@import就是造成这个问题的罪魁祸首。IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。
解决方法: 
* 用 link 代替 @import
* 在 head 之间加入一个 link 或者 script 元素

#### 2.4. 盒模型
* 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)
* 有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 padding;

#### 2.5. CSS 选择符及其优先级
**CSS 选择符：**
1. id选择器(# myid)
2. 类选择器(.myclassname)
3. 标签选择器(div, h1, p)
4. 相邻选择器(h1 + p)
5. 子选择器(ul > li)
6. 后代选择器(li a)
7. 通配符选择器( * )
8. 属性选择器(a[rel = "external"])
9. 伪类选择器(a: hover, li:nth-child)

**可继承的样式：**
1. font-size
2. font-family
3. color
4. text-indent

**不可继承的样式：**
1. border
2. padding
3. margin
4. width
5. height

**优先级算法：**
1. 优先级就近原则，同权重情况下样式定义最近者为准;
2. 载入样式以最后载入的定位为准;
3. !important >  id > class > tag  > *
4. !important > 内嵌 > ID > 类 > 标签、 伪类、 属性选择 > 伪对象 > 继承 > 通配符

**伪类与伪元素**
> 伪类的效果可以通过添加一个实际的类来达到，而伪元素的效果则需要通过添加一个实际的元素才能达到，这也是为什么他们一个称为伪类，一个称为伪元素的原因。
```css
// 伪类
p>i:first-child { color: red; }
// 伪元素
p:first-leter { color: red; }
```

* 伪类本质上是为了弥补常规CSS选择器的不足，以便获取到更多信息；
* 伪元素本质上是创建了一个有内容的虚拟容器；

    比如：document 接口不提供访问元素内容的第一个字或者第一行的机制，而伪元素可以使开发者可以提取到这些信息。并且，一些伪元素可以使开发者获取到不存在于源文档中的内容（比如常见的 `::before,::after`
* CSS3中伪类和伪元素的语法不同；
* 可以同时使用多个伪类，而只能同时使用一个伪元素；

    一个选择器只能使用一个伪元素，并且伪元素必须处于选择器语句的最后
    ```css
    q:lang(en)::after{
        content: " (English) ";
    }
    ```


**CSS3新增伪类举例：**

* `:nth-child()`

    选择某个元素的一个或多个特定的子元素；    
    - 父元素下的第n个子元素
    - 并且这个子元素的标签名为elem

* [p:first-of-type](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:first-of-type) 
    
    选择属于其父元素的首个 `<p>` 元素的每个 `<p>` 元素。

* `p:last-of-type`
      
    选择属于其父元素的最后 `<p>` 元素的每个 `<p>` 元素。
* `p:only-of-type`
      
    选择属于其父元素唯一的 `<p>` 元素的每个 `<p>` 元素。
* `p:only-child`
        
    选择属于其父元素的唯一子元素的每个 `<p>` 元素。
* `p:nth-child(2)`
      
    选择属于其父元素的第二个子元素的每个 `<p>` 元素。
* `:enabled :disabled`
     
    控制表单控件的禁用状态。
* `:checked`
            
    单选框或复选框被选中。
* `:empty`
    
    选择的元素里面没有任何内容。

#### 2.6. position的absolute与fixed
**共同点：**
* 改变行内元素的呈现方式，display被置为inline-block；
* 让元素脱离普通流，不占据空间；
* 默认会覆盖到非定位元素上

**不同点：**
* absolute的根元素是可以设置的，而fixed的根元素固定为浏览器窗口。
* 当你滚动网页，fixed元素与浏览器窗口之间的距离是不变的。

**relative：**
* 生成相对定位的元素，相对于其正常位置进行定位。
* 元素的位置通过left、right、top、bottom属性进行规定，
* 可以通过z-index进行层次分级。
* 元素元素仍保持其未定位前的形状，原本所占的空间仍将保留。
* 如果没有定位偏移量，对元素本身没有任何影响

**absolute：**
* 生成绝对定位元素，脱离文档流，并相对于其包含块进行定位
* 所占的空间会会被后面元素占据；
* 元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框；
* 绝对定位元素的包含块由离它最近的 'position' 属性为 'absolute'、'relative' 或者 'fixed' 的祖先元素创建。如果没有定义，那么就相对于整个文档body定位（注意不是相对于浏览器窗口定位）
* 相对定位一般都是配合绝对定位元素使用

**fixed：**
* 生成绝对定位元素，相对于浏览器窗口的定位
* 通常配合z-index一起来使用。
* 比如说网页上悬挂的聊天图标或者广告就是用了fixed

#### 2.7. display
![display](/img/in-post/post-web-nowcoder/display.png)
display 值的作用：
1. block 块级元素一样显示
2. inline 缺省值。象行内元素类型一样显示。
3. inline-block 象行内元素一样显示，但其内容象块类型元素一样显示。
4. list-item 象块类型元素一样显示，并添加样式列表标记。

#### 2.8. display:none和visibility:hidden
* display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，就当他从来不存在。
* visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间。

#### 2.9. position 值的定位区别
* absolute 生成绝对定位的元素，相对于 static 定位以外的第一个祖先元素进行定位。
* fixed 生成固定定位的元素，相对于浏览器窗口进行定位（老IE不支持）。
* relative 生成相对定位的元素，相对于其在普通流中的位置进行定位。
* static 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。
* inherit 规定从父元素继承 position 属性的值。

#### 2.10. 清除浮动
* 父级div定义 height 
    - 原理：父级div手动定义height，就解决了父级div无法自动获取到高度的问题。 
    - 优点：简单、代码少、容易掌握 
    - 缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题 
    - 建议：不推荐使用，只建议高度固定的布局时使用 
* 结尾处加空div标签 clear:both 
    - 原理：添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度 
    - 优点：简单、代码少、浏览器支持好、不容易出现怪问题 
    - 缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不好 
    - 建议：不推荐使用，但此方法是以前主要使用的一种清除浮动方法 

* 父级div添加 伪元素:after 和 zoom 
    - 原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题 
    - 优点：浏览器支持好、不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等） 
    - 缺点：代码多、不少初学者不理解原理，要两句代码结合使用才能让主流浏览器都支持。 
    - 建议：推荐使用，建议定义公共类，以减少CSS代码。
    
    注意：clear属性只是在block元素是起作用，如果把clear:both用在一个inline-block或inline元素上，是不会起任何作用的
    ```css
    .clearfix:after {
        clear:both;
        content:"";
        display:block;
        height:0;
        line-height:0;
        visibility:hidden;
    }
    .clearfix {
        /* 触发 hasLayout */ 
        zoom: 1; 
    }
    ```

* 父级div定义 overflow:hidden 
    - 原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度 
    - 优点：简单、代码少、浏览器支持好 
    - 缺点：不能和position配合使用，因为超出的尺寸的会被隐藏。 
    - 建议：只推荐没有使用position或对overflow:hidden理解比较深的朋友使用。 
* 父级div定义 overflow:auto 
    - 原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度 
    - 优点：简单、代码少、浏览器支持好 
    - 缺点：内部宽高超过父级div时，会出现滚动条。 
    - 建议：不推荐使用，如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧。
* 父级一起浮动 
    - 原理：所有代码一起浮动，就变成了一个整体 
    - 优点：没有优点 
    - 缺点：会产生新的浮动问题。 
    - 建议：不推荐使用，只作了解。
* 父级div定义 display:table 
    - 原理：将div属性变成表格 
    - 优点：没有优点 
    - 缺点：会产生新的未知问题。 
    - 建议：不推荐使用，只作了解

#### 2.11. 垂直水平居中
* **水平或垂直居中**
    - 单行内容垂直居中
    - div水平居中
    - float
* **水平+垂直居中**
    - 非固定高度居中
    - 利用表格
    - margin负值
    - 完全居中
    - fixed（可视区域内居中）
    - transform
    - inline-block
    - Flex方法
    - 设置当前div的宽度，然后设置margin-left:50%; position:relative; left:-250px;其中的left是宽度的一半。
    - 给父元素设置float，然后父元素设置position:relative和left:50%,子元素设置position:relative和left:-50%来实现
* **图片居中**
    - align
    - text-align

更多了解：[CSS 居中](http://www.cnblogs.com/chaoran/p/7061932.html)

#### 2.12. 怪异模式
> 为了在那些针对 HTML5 设计，但是又没有添加 doctype(可以决定浏览器工作在哪种模式下，后面会详细讨论)的页面而存在

浏览器 | 内核 | 前缀 | js 引擎
- | :-: | -:  | -: 
IE | Trident | -ms- | Chakra
Chrome | Webkit | -webkit- | V8 
Safari | Webkit | -webkit- | Javascriptcore
Opera | Presto | -o- | Carakan
FireFox | gecko | -moz- | 


IE6 时，渲染引擎（MSHTML.dll）做出了一个重要的改变，将自己原先不符合 W3C 规范中的盒模型 box mode 绘制方式改为与 W3C 标准一致（后面会详细讨论），由于这个重大的改动，原先针对 IE 旧版本所设计的 HTML 页面都不能正确显示了，所以在 IE6 发布的时候附带了一个切换回 IE5 页面渲染方式的功能，这个功能中就首次提出了 Quirks Mode。

当用户需要显示旧版本的页面时切换到 Quirks Mode，这时浏览器的渲染引擎就切换到 IE5.5 所对应的版本(MSHTML.dll 5.5.x)，box mode 还是按照之前的方式绘制

当用户需要显示一些新的、满足 W3C 规范的页面时，渲染引擎切换到一个与 Quirks Mode 对应的 Standards Mode（标准模式）

**浏览器如何判断文档类型**
1. Doctype 检测
当 doctype 为<!DOCTYPE html>，表明该页面是遵守了 HTML5 规范的，浏览器会选择 Standards Mode
当 doctype 缺失的时候，浏览器会选择 Quirks Mode

2. x-ua-compatible 信息
![meta](/img/in-post/post-web-nowcoder/meta.png)

**标准模式下的页面与怪异模式下的页面区别**
1. 盒模型
开发人员描述 CSS 中块级元素的一种约定俗称
![box-ie](/img/in-post/post-web-nowcoder/box-ie.png)
![box-standard](/img/in-post/post-web-nowcoder/box-stan.png)

2. 图片元素的垂直对齐方式
vertical-align：定义行内元素的 base line 相对于该元素所在行的 base line 的垂直对齐
    `baseline，sub，supper，top，text-top，bottom，text-bottom，middle `
    base line 指的是一行字横排时下沿的基础线，baseline 并不是汉字的下端沿，而是英文字母 e 的下端沿，bottom line，指的是汉字，或者英文字母 p，g 的下端沿。
    * 对于 inline 元素和 table-cell 元素，在 IE Standards Mode 下 vertical-align 属性默认取值为 baseline。而当 inline 元素的内容只有图片时，如 table 的单元格 table-cell。在 IE Quirks Mode 下，table 单元格中的图片的 vertical align 属性默认为 bottom，因此，在图片底部会有几像素的空间
3. table 元素中的字体
 IE Quirks Mode 下，对于 table 元素，字体的某些属性将不会从 body 或其他封闭元素继承到 table 中，特别是 font-size 属性。
4. 内联元素的尺寸
IE Standards Mode 下，non-replaced inline 元素无法自定义大小，而在 IE Quirks Mode 下，定义这些元素的 width 和 height 属性，能够影响该元素显示的大小尺寸。
5. 元素的百分比高度
 IE Standards Mode 下，高度取决于内容的变化，而在 Quirks Mode 下，百分比高度则被正确应用。
6. 元素溢出的处理
IE Standard Mode 下，overflow 取默认值 visible，即溢出可见，这种情况下，溢出内容不会被裁剪，呈现在元素框外。而在 Quirks Mode 下，该溢出被当做扩展 box 来对待，即元素的大小由其内容决定，溢出不会被裁剪，元素框自动调整，包含溢出内容

#### 2.13. CSS reset
> 是否使用，取决于 “是否需要依赖浏览器默认样式”

1. 导致blockquote、ol、ul、hn等语义元素在没有赋以其他合理的样式时（常常如此），缺乏恰当的样式展现。而因为视觉上无法区分，这进一步导致许多开发人员忽视或误用这些语义元素
2.  CSS reset 通常会增加浏览器进行样式计算的成本（即有一定的性能负担）

#### 2.14. html常见兼容性问题
1. png24位的图片在iE6浏览器上出现背景
    解决方案：做成PNG8，也可以引用一段脚本处理.

2. 浏览器默认的margin和padding不同
    解决方案：加一个全局的 *{margin:0;padding:0;} 来统一。

3. IE6双边距bug：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。
`#box{ float:left; width:10px; margin:0 0 0 10px;} `
这种情况之下IE会产生20px的距离
解决方案：
    * 在float的标签样式控制中加入 _display:inline; 将其转化为行内属性。( _ 这个符号只有ie6会识别)
    * 或者用padding-left代替margin-left

4. 渐进识别的方式，从总体中逐渐排除局部。 
首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。 
接着，再次使用 "+" 将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
    ```js
    .bb{
        background-color:#f1ee18; /*所有识别*/
        .background-color:#00deff\9; /*IE6、7、8识别*/
        +background-color:#a200ff; /*IE6、7识别*/
        _background-color:#1e0bd1; /*IE6识别*/ 
    } 
    ```

5. IE下，可以使用获取常规属性的方法来获取自定义属性，也可以使用 getAttribute() 获取自定义属性；Firefox下,只能使用getAttribute()获取自定义属性
解决方法：统一通过getAttribute()获取自定义属性

6. IE下，event对象有 x、y 属性，但是没有 pageX、pageY属性; Firefox下，event对象有 pageX、pageY 属性，但是没有 x、y 属性
解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

7. Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示
解决方法：可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决

8. 超链接访问过后 hover 样式就不出现了，被点击访问过的超链接样式不在具有 hover 和 active 了
解决方法：改变CSS属性的排列顺序 L-V-H-A
    ```css
    a:link {}
    a:visited {}
    a:hover {}
    a:active {}
    ```

9. 怪异模式问题：漏写 DTD 声明，Firefox 仍然会按照标准模式来解析网页，但在 IE 中会触发怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写 DTD 声明的好习惯。现在可以使用[html5](http://www.w3.org/TR/html5/single-page.html) 推荐的写法：<!DOCTYPE html>

10. 上下margin重合问题：ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。
解决方法：养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。

11. ie6对png图片格式支持不好
解决方案：引用一段脚本处理

12. li之间有间距
解决方法：li 设置vertical-align:middle;

#### 2.15. 适配 & CSS 中的单位
假定已经存在一个使用px单位，且完全适配320xp宽度手机的页面
1. 改变viewport的initial-scale的数值

    首屏渲染 -> js改变initial-scale -> 二次渲染，页面放大(闪烁)
    得提前知道所适配的设备的尺寸,然后服务端根据userAgent来判断。
    ```html
    <% if(device === 1){ %>
        <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=2.0,user-scalable=no" />
    <% } %>

    <% if(device === 2){ %>
        <meta name="viewport" content="width=device-width,initial-scale=1.5,maximum-scale=2.0,user-scalable=no" />
    <% } %>
    ```

    或者使用js计算缩放比例 ,然后替换initial-scale的值
    ```js
    var scale =  screen.width/320,
        viewport =  document.querySelector('meta[name=viewport]');
        
    viewport.setAttribute('content',
        viewport.getAttribute('content')
                .replace(/(initial-scale)=[\d\.]?\d/,'$1='+scale))    
    ```

    使用js会有滞后性，页面会多渲染一次，且会导致页面闪烁
    > 首屏渲染 -> js改变initial-scale -> 二次渲染，页面放大(闪烁)

2. 监听窗口缩放事件-触发重绘事件

    ```js
    (function (win, doc) {
        var docEl = doc.documentElement,
        // 监听横屏和缩放事件
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',

        // 设置默认字体大小
        recalc = function () {
          var clientWidth = docEl.clientWidth;
          if (!clientWidth) return;
          if (isMob) {
            window.baseFontSize = 20 * (clientWidth / 320);
            docEl.style.fontSize = window.baseFontSize + 'px';
          } else {
            window.baseFontSize = 20 * (640 / 320);
            docEl.style.fontSize = window.baseFontSize + 'px';
          }
        };
        if (!doc.addEventListener) return;

        // 监听窗口缩放和dom 加载事件
        win.addEventListener(resizeEvt, recalc, false);
        doc.addEventListener('DOMContentLoaded', recalc, false);
    })(window, document)
    ```
3. 替换px转而使用rem

4. **页面闪烁**
* `html{font-size: 50px;}` ---这个一定写 
* JS动态计算和密集的媒体查询二选一
    
fontsize 初始值设定： iPhone 6 尺寸 fontsize： 50
* 原因： 值得浮动不大

**单位大体分为两大类：**
* 绝对单位 ，不会因为其他元素的尺寸变化而变化。
* 相对单位 ，没有一个固定的度量值，而是由其他元素尺寸来决定的相对值。


类型 | 简介 | 类型	
- | :-: | -:  | -: 
px | 像素 (计算机屏幕上的一个点)，1px = 1/96in | absolute
pt | Points, 1pt = 1/72in
pc | Picas, 1pc = 12pt
in | Inches, 1in = 96px = 2.54cm
cm | Centimeters, 1cm = 96/2.54px
mm | Millimeters, 1mm = 1/10cm
q |	Quarter-millimeters, 1q = 1/4mm
% |	相对于父元素的宽度或字体大小 | relative
em | 相对于父元素的字体大小
rem | (即root em) 相对于html标签的字体大小
ex | 当前字体环境中 x 字母的高度
ch | 当前字体环境中 0 数字的高度
vw | 1% 视口（浏览器可视区域）的宽度
vh | 1% 视口（浏览器可视区域）的高度
vmin | 1% 视口（浏览器可视区域）的宽度和高度中较小的尺寸
vmax | 1% 视口（浏览器可视区域）的宽度和高度中较大的尺寸

相对单位：
* %
    > 相对于父元素的相同属性的大小
    - 参照父元素宽度的元素：padding margin width text-indent
    - 参照父元素高度的元素：height
    - 参照父元素属性:font-size   line-height
    -  **特殊**：
        - 相对定位的时候，top(bottom)   left(right)参照的是父元素的 content-box
        - 绝对定位的时候参照的是最近的定位元素 padding-box

* em && rem
    两者都是基于字体尺寸的，区别在于 em 是相对于当前父元素的字体大小为标准，而 rem 是相对于 html 元素的字体大小为标准。
* ex && ch
    ex 和ch 单位，依赖于当前字体 font-family 和字体大小 font-size。 ex 指当前字体环境中小写字母x 的高度，ch 指当前字体环境中数字 0 的宽度。
![ex](/img/in-post/post-web-nowcoder/ex.jpg)
* vw && vh
    > vh 等于视窗高度的 1/100.

    “视区”所指为浏览器内部的可视区域大小，即window.innerWidth/window.innerHeight大小，不包含任务栏标题栏以及底部工具栏的浏览器区域大小。

    例如，如果浏览器的高是 900px, 1vh 求得的值为 9px 。同理，如果显示窗口宽度为 750px, 1vw 求得的值为 7.5px。
    **应用场景**
    * 元素的尺寸限制
        ```css
        img { max-height: 90vh; }
        ```
    * 视区覆盖以及边界定位
        ```css
        </* 弹出框的半透明覆盖层 */>
        .dialog_container {
            width: 100%;
            width: 100vw;
            height: 100%;
            height: 100vh;
            background-color: rgba(0,0,0,.35);
            position: fixed;
            top: 0;
            left: 0;
        }
        ```
    * 滚动条跳动
        ```css
        .wrap-outer {
            margin-left: calc(100vw - 100%);
        }

        /* 或者： */
        .wrap-outer {
            padding-left: calc(100vw - 100%);
        }
        ```
        100vw相对于浏览器的window.innerWidth，是浏览器的内部宽度，注意，滚动条宽度也计算在内！而100%是可用宽度，是不含滚动条的宽度。
        于是，calc(100vw - 100%)就是浏览器滚动条的宽度大小

        vw, vh视区大小相关单位只适用于非定位元素的高度相关属性上！ (高度相关属性如 –`height/min-height/max-height/line-height/padding-top/padding-bottom` 等)

参考： 
[CSS 单位](https://segmentfault.com/a/1190000004043937)
[视区相关单位vw, vh..简介以及可实际应用场景](http://www.zhangxinxu.com/wordpress/2012/09/new-viewport-relative-units-vw-vh-vm-vmin/)

#### 2.16. 响应式
> 使网站在手机和平板电脑上有更好的浏览阅读体验

* 设置 Meta 标签

    使用设备的宽度作为视图宽度并禁止初始的缩放

    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">

    <!-- user-scalable = no 属性能够解决 iPad 切换横屏之后触摸才能回到具体尺寸的问题 -->
    ```

* 通过媒介查询来设置样式 Media Queries

    ```css
    @media screen and (max-width: 980px) {
        #head { … }
        #content { … }
        #footer { … }
    }
    ```

* 设置多种视图宽度

    假如我们要设定兼容 iPad 和 iphone 的视图，那么可以这样设置：
    ```css
    /** iPad **/
    @media only screen and (min-width: 768px) and (max-width: 1024px) {}
    /** iPhone **/
    @media only screen and (min-width: 320px) and (max-width: 767px) {}
    ```

* 响应式内容

    - 百分比
    - rem
* 图片缩放

    简单的解决方法可以使用百分比，但这样不友好，会放大或者缩小图片。那么可以尝试给图片指定的最大宽度为百分比。假如图片超过了，就缩小。假如图片小了，就原尺寸输出。
    `img { width: auto; max-width: 100%; }`

#### 2.17. CSS 性能优化
* 减小选择器的复杂性
* 减少样式的计算量
* 慎重选择高消耗的样式
    - box-shadows
    - border-radius
    - transparency
    - CSS filters（性能杀手）

* 避免过分重排
* 提升移动或渐变元素的绘制层
    - 新建渲染层 will-change 与 transform 属性一起使用
        ```css
        .element {
            will-change: transform;
        }
        ```

    - 不支持 will-change 属性、但支持创建渲染层的浏览器,用一个 3D transform 属性
        ```css
        .element {
            transform: translateZ(0);
        }
        ```

* 动画性能优化
    - requestAnimationFrame 代替 setTimeout, setInterval
    
    - 多利用硬件能力，如通过 3D 变形开启 GPU 加速
        - translate 取代 absolute 定位
            ```css
            backface-visibility: hidden;
            perspective: 1000;
            ```
        

## 3. JavaScript
#### 3.1. JavaScript 的同源策略
> 同源策略是客户端脚本（尤其是Javascript）的重要的安全度量标准。它最早出自Netscape Navigator2.0，其目的是防止某个文档或脚本从多个不同源装载

这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议，指一段脚本只能读取来自同一来源的窗口和文档的属性。

**为什么要有同源限制：**
比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。

**限制范围**
* Cookie、LocalStorage 和 IndexDB 无法读取。
* DOM 无法获得。
* AJAX 请求不能发送。

#### 3.2. use strict
> ECMAscript 5添加了第二种运行模式："严格模式"（strict mode）。顾名思义，这种模式使得Javascript在更严格的条件下运行

设立"严格模式"的目的，主要有以下几个：
1. 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
2. 消除代码运行的一些不安全之处，保证代码运行的安全；
3. 提高编译器效率，增加运行速度；
4. 为未来新版本的Javascript做好铺垫。

注：经过测试 IE6,7,8,9 均不支持严格模式。

**使用方式**
* 针对整个脚本文件

    将"use strict"放在脚本文件的第一行，则整个脚本都将以"严格模式"运行

    ```html
    <script>
        "use strict";
        console.log("这是严格模式。");
    </script>
    ```

* 针对单个函数
    
    将"use strict"放在函数体的第一行，则整个函数以"严格模式"运行。
    ```js
    function strict(){
        "use strict";
        return "这是严格模式。";
    }
    ```

* 脚本文件的变通写法

    因为第一种调用方法不利于文件合并，所以更好的做法是，借用第二种方法，将整个脚本文件放在一个立即执行的匿名函数之中。
    ```js
    (function (){

        "use strict";
        // some code here

    })();
    ```

**限制**
* 全局变量显式声明

    严格模式下，变量都必须先用var命令声明，然后再使用
* 静态绑定
    - 禁止使用with语句
    - 创设eval作用域

        正常模式下，eval语句的作用域，取决于它处于全局作用域，还是处于函数作用域。严格模式下，eval语句本身就是一个作用域，不再能够生成全局变量了，它所生成的变量只能用于eval内部
* 增强的安全措施

    - 禁止this关键字指向全局对象
    - 禁止在函数内部遍历调用栈

        ```js
        function f(){
            "use strict";
            this.a = 1;
        };

        f();// 报错，this未定义
        ```

    - 禁止在函数内部遍历调用栈

* 禁止删除变量
* 显式报错

    正常模式下，对一个对象的只读属性进行赋值，不会报错，只会默默地失败。严格模式下，将报错

* 重名错误
    - 对象不能有重名的属性
    - 函数不能有重名的参数

* 禁止八进制表示法
* arguments 对象的限制
    - 不允许对arguments赋值
    - arguments 不再追踪参数的变化
    - 禁止使用arguments.callee

        无法在匿名函数内部调用自身

* 函数必须声明在顶层

**缺点：**
现在网站的 JS 都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 merge 后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。

#### 3.3. 消息推送(WebSocket && Server-Sent Events)
> HTTP 协议缺陷：通信只能由客户端发起

##### ---WebSocket
**解决方法：双向通信与消息推送**
* 轮询：客户端**定时向服务器发送Ajax请求**，服务器接到请求后马上返回响应信息并关闭连接。 
    - 优点：后端程序编写比较容易。 
    - 缺点：请求中有大半是无用，浪费带宽和服务器资源。 
    - 实例：适于小型应用。

* 长轮询：客户端向服务器发送Ajax请求，服务器接到请求后 **hold 住连接**，直到有新消息才返回响应信息并关闭连接，客户端处理完响应信息后再向服务器发送新的请求。 
    - 优点：在无消息的情况下不会频繁的请求，耗费资小。 
    - 缺点：服务器hold连接会消耗资源，返回数据顺序无保证，难于管理维护。 Comet 异步的 ashx ， 
    - 实例：WebQQ、 Hi 网页版、 Facebook IM 。

* 长连接：在页面里嵌入一个隐蔵iframe，将这个隐蔵 iframe 的 src 属性设为对一个长连接的请求或是采用 xhr 请求，服务器端就能源源不断地往客户端输入数据。 
    - 优点：消息即时到达，不发无用请求；管理起来也相对方便。 
    - 缺点：服务器维护一个长连接会增加开销。 
    - 实例：Gmail聊天

* Flash Socket：在页面中内嵌入一个使用了 Socket 类的 Flash 程序 JavaScript 通过调用此 Flash 程序提供的 Socket 接口与服务器端的 Socket 接口进行通信， JavaScript 在收到服务器端传送的信息后控制页面的显示。 
    - 优点：实现真正的即时通信，而不是伪即时。 
    - 缺点：客户端必须安装Flash插件；非 HTTP 协议，无法自动穿越防火墙。 
    - 实例：网络互动游戏。

* WebSocket是 HTML5 开始提供的一种浏览器与服务器间进行全双工通讯的网络技术。依靠这种技术可以实现客户端和服务器端的长连接，双向实时通信。
    - 主要特点:
        - 事件驱动
        - 异步
        - 使用 ws 或者 wss 协议的客户端 socket
        - 能够实现真正意义上的推送功能
    - 缺点：少部分浏览器不支持，浏览器支持的程度与方式有区别。

    ```js
    // WebSocket 对象作为一个构造函数，用于新建 WebSocket 实例
    var ws = new WebSocket("wss://echo.websocket.org");

    // 指定连接成功后的回调函数,如果要指定多个回调函数，可以使用addEventListener方法
    ws.onopen = function(evt) { 
        console.log("Connection open ..."); 
        ws.send("Hello WebSockets!");
    };

    ws.onmessage = function(evt) {
        console.log( "Received Message: " + evt.data);
        ws.close();
    };

    ws.onclose = function(evt) {
        console.log("Connection closed.");
    };      
    ```

    读取接收到的内容
    ```js
    ws.onmessage = function(evt) {  
        if(typeof(evt.data)=="string"){  
            //textHandler(JSON.parse(evt.data));  
        }else{  
            var reader = new FileReader();  
            reader.onload = function(evt){  
                if(evt.target.readyState == FileReader.DONE){  
                    var url = evt.target.result;  
                    alert(url);  
                    var img = document.getElementById("imgDiv");  
                    img.innerHTML = "<img src = "+url+" />";  
                }  
            }  
            reader.readAsDataURL(evt.data);  
        }  
    };  
    ```

* Server-Sent Events

**webSocket 特点：**
* 服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于**服务器推送**技术的一种
* 建立在 TCP 协议之上，服务器端的实现比较容易。
* 与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
* 数据格式比较轻量，性能开销小，通信高效。
* 可以发送文本，也可以发送二进制数据。
* 没有同源限制，客户端可以与任意服务器通信。
* 协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。

**webSocket.readyState**

readyState属性返回实例对象的当前状态，共有四种:
* CONNECTING：值为0，表示正在连接。
* OPEN：值为1，表示连接成功，可以通信了。
* CLOSING：值为2，表示连接正在关闭。
* CLOSED：值为3，表示连接已经关闭，或者打开连接失败。

##### ---Server-Sent Events
SSE 使用流信息向浏览器推送信息。它基于 HTTP 协议，目前除了 IE/Edge，其他浏览器都支持。
流信息
> 也就是说，发送的不是一次性的数据包，而是一个数据流，会连续不断地发送过来。这时，客户端不会关闭连接，会一直等着服务器发过来的新的数据流，视频播放就是这样的例子。本质上，这种通信就是以流信息的方式，完成一次用时很长的下载。

* 相似：
    SSE 与 WebSocket 作用相似，都是建立浏览器与服务器之间的通信渠道，然后服务器向浏览器推送信息。

* 区别：
    WebSocket 更强大和灵活。因为它是全双工通道，可以双向通信；SSE 是单向通道，只能服务器向浏览器发送，因为流信息本质上就是下载。如果浏览器向服务器发送信息，就变成了另一次 HTTP 请求。

**优点：**
* 使用 HTTP 协议，现有的服务器软件都支持。WebSocket 是一个独立协议。
* 属于轻量级，使用简单；WebSocket 协议相对复杂。
* 默认支持断线重连，WebSocket 需要自己实现。
* 一般只用来传送文本，二进制数据需要编码后传送，WebSocket 默认支持传送二进制数据。
* 支持自定义发送的消息类型。


参考：[Server-Sent Events 教程](http://www.ruanyifeng.com/blog/2017/05/server-sent_events.html)

#### 3.4. null和undefined
* null 是一个表示"无"的对象，转为数值时为0
* undefined 是一个表示"无"的原始值，转为数值时为NaN
* 当声明的变量还未被初始化时，变量的默认值为undefined
* null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象

undefined表示 “缺少值”，就是此处应该有一个值，但是还没有定义。典型用法是：
1. 变量被声明了，但没有赋值时，就等于 undefined
2. 调用函数时，应该提供的参数没有提供，该参数等于 undefined
3. 对象没有赋值的属性，该属性的值为 undefined
4. 函数没有返回值时，默认返回 undefined

null表示“没有对象”，即该处不应该有值。典型用法是：
1. 作为函数的参数，表示该函数的参数不是对象
2. 作为对象原型链的终点

#### 3.5. new操作符具体干了什么
1. 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型
2. 属性和方法被加入到 this 引用的对象中
3. 新创建的对象由 this 所引用，并且最后隐式的返回 this

    ```js
    var obj  = {};
    obj.__proto__ = Base.prototype;
    Base.call(obj); 
    ```

#### 3.6. JSON
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小。
```json
{"age":"12", "name":"back"}
```

* JSON很像XML

    - 他们都“自我描述”，这意味着值都是可列举的，是“人类可读”的 都是有层级的。(例如你可以在值里再存放值) 
    - 都能被多种的编程语言解析和使用 
    - 都能使用AJAX方法来传递(例如httpWebRequest) 

* JSON跟XML不一样

    - XML里在元素的开始和结尾处有尖括号和标签名：JSON使用花括号，而且只在数据的开始和结束时使用。 
    - JSON更简练，毫无疑问更适合人类书写，也许也能让我们更快速的阅读。 
    - JSON可以在JavaScript里简单的传递到eval()方法里使用 
    - JSON里有数组{每个元素没有自己的名称} 
    - 在XML里你可以对一个元素使用任意想要的名称，在JSON里你不能使用Javascript里的保留字 

#### 3.7. js延迟加载
方法：
1. defer和async
    差别在于脚本下载完之后何时执行
    * async
        加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步），不考虑依赖关系
    * **defer**--常用
        `<script defer src="script.js"></script>`
        加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在**所有元素解析完成**之后，DOMContentLoaded 事件触发之前完成。
        **按照加载顺序执行脚本**
2. 动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）
    ```js
    function loadScript(url, callback){
        var script = document.createElement ("script")
        script.type = "text/javascript";
        if (script.readyState){ //IE
            script.onreadystatechange = function(){
                if (script.readyState == "loaded" || script.readyState == "complete"){
                    script.onreadystatechange = null;
                    callback();
                }
            };
        } else { //Others
            script.onload = function(){
                callback();
            };
        }
        script.src = url;
        document.getElementsByTagName_r("head")[0].appendChild(script);
    }
    ```

3. 按需异步载入js
4. 放到最后加载

**script 的位置是否会影响首屏显示时间**
* 在解析 HTML 生成 DOM 过程中，js 文件的下载是并行的，不需要 DOM 处理到 script 节点。因此，script的位置不影响首屏显示的开始时间。
* 浏览器解析 HTML 是自上而下的线性过程，script作为 HTML 的一部分同样遵循这个原则
因此，script 会延迟 `DomContentLoad`，只显示其上部分首屏内容，从而影响首屏显示的完成时间

#### 3.8. documen.write和 innerHTML 
* document.write 只能重绘整个页面
* innerHTML 可以重绘页面的一部分

#### 3.9. 内存泄漏
> 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在

垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

js 常用的垃圾回收策略是标记清除
* 内存中的所有变量都加上标记（当然，可以使用任何标记方式）。然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后再被加上标记的变量将被视为准备删除的变量

IE7-8 的 DOM 的回收方式是引用计数
所以，在 ie 中有dom 的循环引用会导致内存泄漏，ie9 已修复
```js
window.onload=function outerFunction(){
    var obj = document.getElementById("element");
    obj.onclick=function innerFunction(){};
};
// 可以理解成闭包循环引用导致的内存泄漏
```

* obj是外部的一个对象
* obj.onclick 定义的这个函数隐式的调用到了obj这个对象（obj.onclick函数中的this就是对象obj）
* obj.onclick 实际上是一个outerFunction外部的函数(DOM监听事件不可能是局部作用域的，是全局作用域)
* 所以DOM触发这个事件相当于是在函数outerFunction外部调用了obj.click()，而事件内部使用了outerFunction的变量obj,这就形成了一个闭包。

改成如下结构
```js
window.onload=function outerFunction(){
    var obj = document.getElementById("element");
    obj.onclick=function innerFunction(){};
    obj=null;
};
// 将变量设置为null意味着切断变量与它此前引用的值之间的连接。当垃圾回收器下次运行时，就会删除这些值并回收它们占用的内存。


// 使用jq
window.onload=function outerFunction(){
  var obj = document.getElementById("element");
  $(obj).click(function innerFunction(){});
};
// jQuery绑定事件最终都没有直接绑定到DOM对象上，而是使用jQuery缓存来绑定的
// jQuery考虑到了内存泄漏的潜在危害，所以它会手动释放自己指定的所有事件处理程序
```

**内存泄漏原因**
* 基础的DOM泄漏
    - 当原有的DOM被移除时，子结点引用没有被移除则无法回收。
        ```js
        var select = document.querySelector;
        var treeRef = select('#tree');

        var leafRef = select('#leaf');   //在COM树中leafRef是treeFre的一个子结点

        select('body').removeChild(treeRef);//#tree不能被回收入，因为treeRef还在
        　　
        // 解决方法:
        treeRef = null; //tree还不能被回收，因为叶子结果leafRef还在
        leafRef = null; //现在#tree可以被释放了
        ```
    - 页面交叉泄漏
        - 第一种方式是，依次将元素先添加到其父元素中，最后将整个子树添加到文档树中，如果同时满足其他条件，这种方式将导致中间对象的泄漏；
        - 另一种方式是，从上至下依次将动态创建的元素附加到文档数中，这样每次附加的元素都直接继承了原始文档树德作用域对象，从而不会生成任何中间对象，这种方式避免了潜在的内存泄露。
        ![dom-leak](/img/in-post/post-web-nowcoder/dom-leak-model.gif)
    
* setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
    
    使用setTimeout一般不会出现内存泄漏的现象（使用规范），但是如果和其他函数在一起，形成了闭包就难逃内存泄漏了
* 闭包
* 控制台日志
* 循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

**GC 优化**
* 分代回收（Generation GC）
    - 这个和Java回收策略思想是一致的。目的是通过区分“临时”与“持久”对象；多回收“临时对象”区（young generation），少回收“持久对象”区（tenured generation），减少每次需遍历的对象，从而减少每次GC的耗时
    - 对于tenured generation对象，有额外的开销：
        把它从young generation迁移到tenured generation，另外，如果被引用了，那引用的指向也需要修改
* 增量GC
    - “每次处理一点，下次再处理一点，如此类推”
    - 虽然耗时短，但中断较多，带来了上下文切换频繁的问题

推荐阅读：
* [跟我学习javascript的垃圾回收机制与内存管理](http://www.jb51.net/article/75292.htm)
* [js晋级篇——前端内存泄漏探讨](https://www.cnblogs.com/chuaWeb/p/5196330.html)

#### 3.10. 判断当前脚本运行在浏览器还是node环境
通过判断 Global 对象是否为window，如果不为window，当前脚本没有运行在浏览器中。
* 在node中的全局变量是global 
* 浏览器的全局变量是window

可以通过该全局变量是否定义来判断宿主环境

#### 3.11. Node的优点和缺点
> 在Node中，除了代码，一切都是并行的！

特点：单线程、异步I/O、事件驱动

事件驱动：
* 通过事件或状态的变化来进行应用程序的流程控制
* 当执行过程中遇到I/O阻塞(读取文件、查询数据库、请求套接字、访问远程服务等)时，事件循环线程不会停下等待结果,转而继续执行队列中的下一个任务,不会在事件循环线程中执行

NodeJS的事件循环模型一般要注意下面几点：
* 因为是单线程的，所以当顺序执行js文件中的代码的时候，事件循环是被暂停的
* 当JS文件执行完以后，事件循环开始运行，并从消息队列中取出消息，开始执行回调函数
* 因为是单线程的，所以当回调函数被执行的时候，事件循环是被暂停的
* 当涉及到I/O的时候，nodejs会开一个独立的线程来进行异步I/O操作，操作结果以后将消息压入消息队列

**优点：**
1. 因为Node是基于事件驱动和无阻塞的，所以非常适合处理并发请求，因此构建在Node上的代理服务器相比其他技术实现（如Ruby）的服务器表现要好得多。
2. 与Node代理服务器交互的客户端代码是由javascript语言编写的，因此客户端和服务器端都用同一种语言编写，这是非常美妙的事情。

**缺点：**
1. Node是一个相对新的开源项目，所以不太稳定，它总是一直在变。
2. 缺少足够多的第三方库支持。看起来，就像是Ruby/Rails当年的样子（第三方库现在已经很丰富了，所以这个缺点可以说不存在了）。

**Node.js 的适用场景:**
1. 高并发
2. 聊天
3. 实时消息推送   

#### 3.12. javascript 创建对象
1. Object构造函数创建
    ```js
    var Person = new Object();
    Person.name = 'Nike';
    Person.age = 29;
    //创建了Object引用类型的一个新实例，然后把实例保存在变量Person中
    ```

2. 对象字面量表示法
    ```js
    var Person = {};//相当于var Person = new Object();
    var Person = {
        name:'Nike';
        age:29;  
    }
    ```
    对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。
    也就是说，第一种和第二种方式创建对象的方法其实都是一样的，只是写法上的区别不同

    避免过多的重复代码

3. 工厂模式
    ```js
    function createPerson(name,age,job){
        var o = new Object();
        o.name = name;
        o.age = age;
        o.job = job;
        o.sayName = function(){
            alert(this.name); 
        };
        return o; 
    }
    var person1 = createPerson('Nike',29,'teacher');
    var person2 = createPerson('Arvin',20,'student');
    ```
    createPerson函数中，返回的是一个对象。我们无法判断返回的对象究竟是一个什么样的类型

4. 使用构造函数创建对象
    ```js
    function Person(name,age,job){
        this.name = name;
        this.age = age;
        this.job = job;
        this.sayName = function(){
            alert(this.name);
        }; 
    }
    var person1 = new Person('Nike',29,'teacher');
    var person2 = new Person('Arvin',20,'student');
    ```

    **new**
    * 创建了一个对象
    * 将this指向这个对象
    * 返回这个对象
    * 实例对象都有一个属性constructor(构造函数)，指向Person
    可以通过constructor判断对象类型的原理
    
    **对比工厂模式，我们可以发现以下区别：**
    * 没有显示地创建对象
    * 直接将属性和方法赋给了this对象
    * 没有return语句
    * 终于可以识别的对象的类型。对于检测对象类型，我们应该使用instanceof操作符
    * 按照惯例，构造函数始终要应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头

    **构造函数缺点：**
    每个方法都要在每个实例上重新创建一遍，方法指的就是我们在对象里面定义的函数。如果方法的数量很多，就会占用很多不必要的内存

5. 原型创建对象模式
    > 与构造函数模式不同的是，原型模式的每个实例都是访问同一属性同一函数，函数不用重新创建

    ```js
    function Person(){}
        Person.prototype.name = 'Nike';
        Person.prototype.age = 20;
        Person.prototype.jbo = 'teacher';
        Person.prototype.sayName = function(){
        alert(this.name);
    };
    var person1 = new Person();
    var person2 = new Person();
    person1.name ='Greg';
    alert(person1.name); //'Greg' --来自实例
    alert(person2.name); //'Nike' --来自原型
    ```
    * 使用原型创建对象的方式，可以让所有对象实例共享它所包含的属性和方法。
    * 当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性。
    * 这时候我们就可以使用构造函数模式与原型模式结合的方式，构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性

6. 组合使用构造函数模式和原型模式
    ```js
    function Person(name,age,job){
        this.name =name;
        this.age = age;
        this.job = job;
    }
    Person.prototype = {
        constructor:Person,
        sayName: function(){
            alert(this.name);
        };
    }
    var person1 = new Person('Nike',20,'teacher');
    ```

#### 3.13. javascript 继承
1. 原型链

    基本思想：利用原型让一个引用类型继承另外一个引用类型的属性和方法。

    构造函数，原型，实例之间的关系：
    * 每个构造函数都有一个原型对象
    * 原型对象包含一个指向构造函数的指针
    * 实例都包含一个指向原型对象的内部指针

    ```js
    SubType.prototype = new SuperType();// 继承了SuperType
    
    SubType.prototype.constructor = SubType;// 指回原来的构造函数
    ```

2. 构造函数

    基本思想：在子类型构造函数的内部调用超类构造函数，通过使用call()和apply()方法可以在新创建的对象上执行构造函数。
    ```js
    function SubType() {
        SuperType.call(this);//继承了SuperType
    }
    ```

3. 组合继承

    基本思想：将原型链和借用构造函数的技术组合在一块，从而发挥两者之长的一种继承模式。
4. 原型式继承

    基本想法：借助原型可以基于已有的对象创建新对象，同时还不必须因此创建自定义的类型
    ```js
    function object(o) {
        function F() {}
        F.prototype = o;
        return new F();
    }
    ```
5. 寄生式继承

    基本思想：创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真正是它做了所有工作一样返回对象。 
6. 寄生组合式继承

    基本思想：通过借用函数来继承属性，通过原型链的混成形式来继承方法 
    ```js
    function inheritProperty(subType, superType) {
        var prototype = object(superType.prototype); //创建对象
        prototype.constructor = subType; //增强对象
        subType.prototype = prototype; //指定对象
    }
    ```

#### 3.14. 原型与原型链
* 原型对象
    - 每个函数对象都有一个prototype 属性，这个属性指向函数的原型对象
    - 原型上的属性和方法都是共有的
    - prototype这个对象上，自带一个属性，constructor指向当前这个类
    - 原型对象（Person.prototype）是 构造函数（Person）的一个实例
    
    **注意：**
    - 添加和修改原型的属性和方法都能立即在所有对象实例中反应出来（即使先创建实例后修改原型）
    - 但是如果重写整个原型对象，创建在前的实例并不能获得重写后的属性或方法
    这是因为重写原型之后是新生成原型对象，和声明在前的任何已经存在的实例都没有关系。

* 原型链
> 原型链是由一些用来继承和共享属性的对象组成的（有限的）对象链

    每个对象数据类型（普通对象，prototype，实例）都有一个属性，叫做 __proto__
    __proto__指针 指向构造函数的 prototype
    `person1.__proto__ == Person.prototype`
![prototype](/img/in-post/post-web-nowcoder/prototype.jpg)

console.log（Tom.age）的查找过程
1. 首先在私有空间内查找age属性，私有空间的属性包括自身的属性和从类那里继承的属性
2. 找不到的话：通过__proto__去当前实例所属类的原型上进行查找，找到的话，说明是共有属性；
3. 还找不到的话：继续通过__proto__去当前实例所属类的原型进行查找，找不到将继续通过__proto__一直找到Object。 

原型和原型链是JS实现继承的一种模型。
原型链的形成是真正是靠__proto__ 而非prototype

![prototype](/img/in-post/post-web-nowcoder/prototype02.jpg)
```js
// 原型对象的结构：

Function.prototype = {
    constructor : Function,
    __proto__ : parent prototype,
    some prototype properties: ...
};
```
总结：
* 函数的原型对象constructor默认指向函数本身
* 原型对象除了有原型属性外，为了实现继承，还有一个原型链指针__proto__，该指针指向上一层的原型对象，而上一层的原型对象的结构依然类似，这样利用__proto__一直指向Object的原型对象上
* Object 的原型对象用 `Object.prototype.proto = null` 表示原型链的最顶端，如此变形成了javascript的原型链继承，同时也解释了为什么所有的javascript对象都具有Object的基本方法。




更多：
* [JS之理解原型和原型链](https://segmentfault.com/a/1190000010354583)
* [最详尽的 JS 原型与原型链终极详解](https://www.jianshu.com/p/dee9f8b14771)

#### 3.15. ajax
> Asynchronous JavaScript and XML

通过Ajax可以使用Javascript语句来调用XMLHttpRequest对象，直接与服务器进行通讯，可以在不重载页面的情况下与服务器交换数据

**过程**

1. 创建XMLHttpRequest对象,也就是创建一个异步调用对象
2. 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
3. 设置响应HTTP请求状态变化的函数
4. 发送HTTP请求
5. 获取异步调用返回的数据
6. 使用JavaScript和DOM实现局部刷新
```js
//ajax
function myAjax(url) {
    //创建xml对象
     var ajax = new XMLHttpRequest()
    //open 设置参数
    ajax.open('get', url)
    //发送请求
    ajax.send()
    //注册事件
    ajax.onreadystatechange = function () {
        if (ajax.status == 200) {
            console.log(xml.responseText)
        }
    }

    // post
    xhr.setRequestHeader("Content-Type", "x-www-form-urlencoded")
    xhr.send(data)
}
```

用原生 ajax 与 promise
```js
// 封装一个get请求的方法
function getJSON(url) {
    return new Promise(function(resolve, reject){
        var XHR = new XMLHttpRequest();
        XHR.open('GET', url, true);
        XHR.send();
 
        XHR.onreadystatechange = function() {
            if (XHR.readyState == 4) {
                if (XHR.status == 200) {
                    try {
                        var response = JSON.parse(XHR.responseText);
                        resolve(response);
                    } catch (e) {
                        reject(e);
                    }
                } else {
                    reject(new Error(XHR.statusText));
                }
            }
        }
    })
}
 
getJSON(url).then(res => console.log(res));
```

#### 3.16. `setTimeout` & `this` & `setInterval`
**setTimeout this**
> 超时调用的代码都是在全局作用域中执行的，因此函数中的this的值在非严格模式下指向window对象，在严格模式下是undefined

![mvc](/img/in-post/post-web-fragment/this.jpg)
* setTimeout()中，如果是setTimeout(this)这样的形式，那么this要看上下文，默认是window；
* 如果setTimeout里面的函数中的this的话，都统一指向window
* 第14行代码的this是指向test1对象的，那只要我们保存一下这个变量，然后使用闭包就能获取到它了，因为闭包可以保存自身当前作用域上的变量（当然这肯定是耗费内存的）
    ```js
    function test1() {
        var _this = this; 
        this.name = "chaoran";
        this.sayName = function() {
            console.log(this.name);
        }
        setTimeout(function () {
            // 由于闭包的原因保存了_this为test1对象，所以sayName()输出“chaoran”
            _this.sayName();     
            },0);
        }
    new test1();
    ```

**事件添加**
> 定时器对队列的工作方式：当特定时间过去后将代码添加到队列中，但并不意味着会马上将执行，设定一个200ms后执行的定时器，指的是在200ms后它将被添加到队列中，是否执行，还得看主线程及队列中是否没有其他的东西

> 定时器的回调函数并不是相当于在时间到了就执行，而是有一个主js执行进程，这个进程是页面刚加载的时候页面按照加载顺序执行的js代码，此外还有一个需要在进程空闲的时候执行的代码队列

（1）所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。

（2）主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。

（3）一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。

（4）主线程不断重复上面的第三步。


```js
var a=document.getElementById("nav");
    a.onclick=function(){
    setTimeout(alertsomething,200);
    //一些其他的代码
}
function alertsomething(){
    alert("it is working");
}
```
假定onclick处理程序需要执行300ms，这时虽然在205ms添加了定时器代码，但是仍旧需要等待onclick事件完成后才能够执行。如图所示，本来在205ms处添加了定时器代码，但是由于此时onclick事件还没结束，故要等到300ms后才执行定时器代码
![load-order1](/img/in-post/post-web-nowcoder/settimeout.png)

**为什么常用setTimeout模拟setInterval**

**setInterval**
![load-order1](/img/in-post/post-web-nowcoder/setinterval.png)


* setInterval每隔100ms往队列中添加一个事件；
* 100ms后，添加T1定时器代码至队列中，主线程中还有任务在执行，所以等待;
* some event执行结束后执行T1定时器代码；又过了100ms，T2定时器被添加到队列中，主线程还在执行T1代码，所以等待；
* 又过了100ms，理论上又要往队列里推一个定时器代码，但由于此时T2还在队列中，所以T3不会被添加，结果就是此时被跳过；
* **这里我们可以看到，T1定时器执行结束后马上执行了T2代码，所以并没有达到定时器的效果。**

综上所述，setInterval 有两个缺点：

* 使用 setInterval 时，某些间隔会被跳过

    setInterval 间歇调用，是在前一个方法执行前，就开始计时，比如间歇时间是500ms，那么不管那时候前一个方法是否已经执行完毕，都会把后一个方法放入执行的序列中
* 多个定时器的代码执行之间的间隔可能比预期的小
* 可能多个定时器会连续执行；

**解决方法：**
> 重复定时器

```js
setTimeout(function(){
    //处理代码
    setTimeout(arguments.callee,interval)
},interval);
```

原理：
* 链式 setTimeout 调用，每次函数执行的时候都会创建一个新的定时器。第二个setTimeout() 调用使用了 arguments.callee 来获取对当前执行的函数的引用，并为其设置另外一个定时器。
    - 这样做的好处是，在前一个定时器代码执行完之前，不会向队列插入新的定时器代码，确保不会有任何缺失的间隔。
    - 而且，它可以保证在下一次定时器代码执行之前，至少要等待指定的间隔，避免了连续的运行。

**应用**
* 调整事件发生顺序
    网页开发中，某个事件先发生在子元素，然后冒泡到父元素，即子元素的事件回调函数，会早于父元素的事件回调函数触发。如果，我们先让父元素的事件回调函数先发生，就要用到 `setTimeout(f, 0)`

更多了解：
* [理解 setTimeout 和 setInterval](https://www.cnblogs.com/xiaohuochai/p/5773183.html)
* [由 setTimeout 的 this 讲起](http://blog.csdn.net/qq_26598303/article/details/52668683)
    
#### 3.17. 数组方法
**改变原数组的：**
* shift：将第一个元素删除并且返回删除元素，空即为undefined
* unshift：向数组开头添加元素，并返回新的长度
* pop：删除最后一个并返回删除的元素
* push：向数组末尾添加元素，并返回新的长度
* reverse：颠倒数组顺序
* sort：对数组排序
* splice:splice(start,length,item)删，增，替换数组元素，返回被删除数组，无删除则不返回

**不改变原数组的：**
* concat：连接多个数组，返回新的数组
* join：将数组中所有元素以参数作为分隔符放入一个字符
* slice：slice(start,end)，返回选定元素
* map,filter,forEach,some,every等不改变原数组

**splice和slice的区别：**
* splice(i,j,”a”) 删除，添加元素
* splice() 方法与 slice() 方法的作用是不同的，splice() 方法会直接对数组进行修改。从i开始删j个(包括i),并将”a”插入到i处。 
* slice(start,end) 从某个已有的数组返回选定的元素，从start位开始返回到end（包括start不包括end）如果是负数，表示从数组尾部进行计算（同样：包括start不包括end）
请注意，该方法并不会修改数组，而是返回一个子数组。

来源： [是否改变原数组的常用方法归纳](http://blog.csdn.net/cristina_song/article/details/77917404)


#### 3.18. 浏览器引擎 & js 引擎
* GUI 渲染线程
* JavaScript引擎线程
* 定时触发器线程
* 事件触发线程
* 异步http请求线程

**GUI 渲染线程 与 JavaScript引擎线程互斥！**

* 由于JavaScript是可操纵DOM的，如果在修改这些元素属性同时渲染界面（即JavaScript线程和UI线程同时运行），那么渲染线程前后获得的元素数据就可能不一致了。
* 为了防止渲染出现不可预期的结果，浏览器设置GUI渲染线程与JavaScript引擎为互斥的关系，当JavaScript引擎执行时GUI线程会被挂起，GUI更新会被保存在一个队列中等到引擎线程空闲时立即被执行。

**JS阻塞页面加载**

* 由于GUI渲染线程与JavaScript执行线程是互斥的关系，当浏览器在执行JavaScript程序的时候，GUI渲染线程会被保存在一个队列中，直到JS程序执行完成，才会接着执行。因此如果JS执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

**定时触发器线程**

* 浏览器定时计数器并不是由JavaScript引擎计数的, 因为JavaScript引擎是单线程的, 如果处于阻塞线程状态就会影响记计时的准确, 因此通过单独线程来计时并触发定时是更为合理的方案。

**事件触发线程**

* 当一个事件被触发时该线程会把事件添加到待处理队列的队尾，等待JS引擎的处理。这些事件可以是当前执行的代码块如定时任务、也可来自浏览器内核的其他线程如鼠标点击、AJAX异步请求等，但由于JS的单线程关系所有这些事件都得排队等待JS引擎处理。

**异步http请求线程**

* 在XMLHttpRequest在连接后是通过浏览器新开一个线程请求， 将检测到状态变更时，如果设置有回调函数，异步线程就产生状态变更事件放到 JavaScript引擎的处理队列中等待处理。

[聊聊 JavaScript 与浏览器的那些事 - 引擎与线程](https://zhuanlan.zhihu.com/p/32751855)

#### 3.19. Promise
> 用同步操作的流程写法来表达异步操作，避免了层层嵌套的异步回调

* `Promise.prototype.then()`
    ```js
    //原生Primose顺序嵌套回调示例
    var fs = require('fs')

    var read = function (filename){
        var promise = new Promise(function(resolve, reject){
            fs.readFile(filename, 'utf8', function(err, data){
                if (err){
                    reject(err);
                }
                resolve(data);
            })
        });
        return promise;
    }

    read('./text1.txt')
    .then(function(data){
        console.log(data);
        return read('./text2.txt');   // 返回了一个新的Promise实例
    })
    .then(function(data){
        console.log(data);
    });
    ```
    
    Promise构造函数的参数是一个函数，在这个函数中我们写异步操作的代码
    在异步操作的回调中，根据err变量来选择是执行resolve方法还是reject方法
    - 一般来说调用resolve方法的参数是异步操作获取到的数据(如果有的话)，但还可能是另一个Promise对象，表示异步操作的结果有可能是一个值
    - 也有可能是另一个异步操作，调用reject方法的参数是异步回调用的err参数

调用read函数时，实际上返回的是一个Promise对象，通过在这个Promise对象上调用then方法并传入resolve方法和reject方法来指定异步操作成功和失败后的操作。

* `Promise.prototype.catch()`
    > 用于指定发生错误时的回调函数

    ```js
    read('./text1.txt')
    .then(function(data){
        console.log(data);
        return read('not_exist_file');
    })
    .then(function(data){
        console.log(data);
    })
    .catch(function(err){
        console.log("error caught: " + err);
    })
    .then(function(data){
        console.log("completed");
    })
    ```
    使用Promise对象的catch方法可以捕获异步调用链中callback的异常
    Promise对象的catch方法返回的也是一个Promise对象，因此，在catch方法后还可以继续写异步调用方法

* Promise异步并发
    - `Promise.all()`
        - 将多个Promise实例，包装成一个新的Promise实例
            `var p = Promise.all([p1,p2,p3]);`
        - 接受一个数组作为参数，p1、p2、p3都是Promise对象实例
        - 只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
        - 只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。
            ```js
            var promises = [1, 2].map(function(fileno){
                return read('./text' + fileno + '.txt');
            });

            Promise.all(promises)
            .then(function(contents){
                console.log(contents);
            })
            .catch(function(err){
                console.log("error caught: " + err);
            })
            ```
    - `Promise.race()`
        - 将多个Promise实例，包装成一个新的Promise实例
            `var p = Promise.race([p1,p2,p3]);`
        - p1、p2、p3只要有一个实例率先改变状态，p的状态就会跟着改变，那个率先改变的Promise实例的返回值，就传递给p的返回值。
        - 如果Promise.all方法和Promise.race方法的参数不是Promise实例，就会先调用下面讲到的Promise.resolve方法，将参数转为Promise实例，再进一步处理

    - `Promise.resolve()`
        - 将现有对象转换成Promise对象

        ```js
        var p = Promise.resolve('Hello');
        p.then(function (s){
            console.log(s)
        });
        ```
    
    - `Promise.reject()`
        - 返回一个新的Promise实例，该实例的状态为rejected。
        - `Promise.reject` 方法的参数reason，会被传递给实例的回调函数。

        ```js
        var p = Promise.reject('出错了');
        p.then(null, function (s){
            console.log(s)
        });
        ```

#### 3.20. 立即执行表达式
* 循环中定时输出数据项
* 插件和模块化开发——避免变量污染

```js
for(var i = 0; i < 5; i++) {
    (function(i) {
      setTimeout(function() {
        console.log(i);  
      }, 1000);
    })(i)
}

(function($) { 
        //代码
 } )(jQuery);
 ```

#### 3.21. 数字操作
##### ---浮点数
js 中number 类型就是浮点型，采用 IEEE-754  64 位双精度浮点数，是二进制表示法，可以精确表示分数，每个浮点数 64 位
**JavaScript提供的有效数字最长为53个二进制位（64位浮点的后52位+有效数字第一位的1）**

最高的1位是符号位，接着的11位是指数，剩下的52位为有效数字，具体：

* 第0位：符号位， s 表示 ，0表示正数，1表示负数；
* 第1位到第11位：储存指数部分， e 表示 ；
* 第12位到第63位：储存小数部分（即有效数字），f 表示，

![bit](/img/in-post/post-web-nowcoder/bit.jpg)

 由于采用二进制
 不能有限表示分数
 ```js
 0.1 + 0.2

 // 先转成二进制 
 // 0.1 ----> 0.0001 1001 1001...
 // 0.2 ----> 0.0011 0011 0011...
 // 双精度浮点数的小数部分最多支持 52 位，所以两者相加之后得到这么一串
 // 0.0100110011001100110011001100110011001100...
 ```

 准确计算：
 * 一是先升幂再降幂：
    ```js
    function add(num1, num2){
        let r1, r2, m;
        r1 = (''+num1).split('.')[1].length;
        r2 = (''+num2).split('.')[1].length;

        m = Math.pow(10,Math.max(r1,r2));
        return (num1 * m + num2 * m) / m;
    }
    console.log(add(0.1,0.2));   //0.3
    console.log(add(0.15,0.2256)); //0.3756
    ```

* 二是是使用内置的 toPrecision() 和 toFixed() 方法，注意，方法的返回值字符串。
    ```js
    // toFixed() 返回一个数值的字符串表现形式。
    parseFloat((数学表达式).toFixed(digits))

    // toFixed() 精度参数须在 0 与20 之间
    // 运行
    parseFloat((1.0 - 0.9).toFixed(10)) // 结果为 0.1 
    ```

* 将浮点数转换字符串，分隔成为整数部分和小数部分，小数部分再转换为整数，计算结果后，再转换为浮点数

##### ---实现 `isInteger`
> 将x 转化为十进制整数，判断和本身是否相等

```js
function checkInteger(num) {
    return parseInt(num, 10) === num
}

// ES6
Number.isInteger(25)   // true
Number.isInteger(25.0) // true
Number.isInteger(25.1) // false
```

JavaScript能够准确表示的整数范围在 -2^53 到 2^53 之间（不含两个端点），超过这个范围，无法精确表示这个值。ES6 引入了Number.MAX_SAFE_INTEGER 和 Number.MIN_SAFE_INTEGER这两个常量，用来表示这个范围的上下限，并提供了 Number.isSafeInteger() 来判断整数是否是安全型整数。

##### ---运算规则
**数字 & 字符串**
* 多个数字和数字字符串混合运算时，跟操作数的位置有关
    ```js
    console.log(2 + 1 + '3'); / /‘33’
    console.log('3' + 2 + 1); //'321'
    ```

* 数字字符串之前存在数字中的正负号(+/-)时，会被转换成数字
    ```js
    console.log(typeof '3');   // string
    console.log(typeof +'3');  //number
    ```

* 同样，可以在数字前添加 ''，将数字转为字符串
    ```js
    console.log(typeof 3);   // number
    console.log(typeof (''+3));  //string
    ```

* 对于运算结果不能转换成数字的，将返回 NaN
    ```js
    console.log('a' * 'sd');   //NaN
    console.log('A' - 'B');  // NaN
    ```

**逻辑运算**
* 逻辑与返回第一个是 false 的操作数 或者 最后一个是 true的操作数
    ```js
    console.log(1 && 2 && 0);  //0
    console.log(1 && 0 && 1);  //0
    console.log(1 && 2 && 3);  //3

    //如果某个操作数为 false，则该操作数之后的操作数都不会被计算
    ```

* 逻辑或返回第一个是 true 的操作数 或者 最后一个是 false的操作数
    ```js
    console.log(1 || 2 || 0); //1
    console.log(0 || 2 || 1); //2
    console.log(0 || 0 || false); //false

    // 如果某个操作数为 true，则该操作数之后的操作数都不会被计算
    ```

* 如果逻辑与和逻辑或作混合运算，则逻辑与的优先级高：
    ```js
    console.log(1 && 2 || 0); //2
    console.log(0 || 2 && 1); //1
    console.log(0 && 2 || 1); //1
    ```

* 在 JavaScript，常见的 false 值：
    ```js
    0, '0', +0, -0, false, '', null, undefined, NaN
    // 要注意空数组([])和空对象({}):

    console.log([] == false) //true
    console.log({} == false) //false
    console.log(Boolean([])) //true
    console.log(Boolean({})) //true
    ```

（1）空数组[]和空对象{}都是object类型，因此直接用于if判断条件时就会被转化为true。

（2）任意值与布尔值比较，都会将两边的值转化为Number

##### ---判断回文
总结：[判断方法汇总](https://github.com/dwqs/awesome-codewars/blob/master/codewars/palindrome-for-your-dome.md)

#### 3.22. for 循环中为元素添加点击事件
```js
for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  btn.addEventListener('click', function(){ console.log(i); });
  document.body.appendChild(btn);
}

// 点击每个元素结果都为 5
```

每次的循环中onclick的函数体并没有执行。当点击按钮时，触发了onclick函数，这时再执行函数体中的内容。但是，此时循环已经结束

解决方案：IIFE


#### 3.23. JavaScript 防篡改对象
> 防篡改对象有三个级别，分别是不可拓展对象、密封对象和冻结对象

* 默认
    - 所有对象可扩展--无论什么时候都可以向对象中添加属性和方法

* 一级保护 —— 不可拓展对象
    * Object.preventExtensions()
        - 不能向对象中新添加属性和方法

        ```js
        var obj = {
            name: "Tom"
        }
        Object.preventExtensions(obj); //阻止篡改对象
        obj.age = 21;
        console.log(obj.age); //undefined
        
        
        //修改原有的属性
        obj.name = "Bob";
        console.log(obj.name); //Bob
        ```
    * Object.isExtensible() —— 鉴定对象是否为可篡改

        ```js
        var obj = {
            name: "Tom"
        }
        
        console.log(Object.isExtensible(obj)); //true
        
        Object.preventExtensions(obj); //阻止篡改对象
        console.log(Object.isExtensible(obj)); //false
        ```

* 二级保护 —— 密封对象
    - Object.seal()
        - 不可扩展➕对象的属性和方法不能通过delete操作符删除

        ```js
        var obj = {
            name: "Tom"
        }
        
        //密封对象
        Object.seal(obj);
        
        obj.age = 21;
        console.log(obj.age); //undefined 不能新添加属性
        
        delete obj.name;
        console.log(obj.name); //Tom 不能删除对象的属性
        ```

    - Object.isSealed()
        - 鉴定对象是否是密封对象

* 三级保护 —— 冻结对象
    - Object.freeze()
        - 不可扩展的+密封+属性值也不能修改

    ```js
    var obj = {
        name: "Tom"
    }
    
    Object.freeze(obj); //冻结对象
    
    obj.age = 21;
    console.log(obj.age); //undefined 不可扩展
    
    delete obj.name;
    console.log(obj.name); //Tom 不可删除
    
    obj.name = "Bob";
    console.log(obj.name); //Tom 不可修改
    ```
    - Object.isFrozen()

* 进阶保护
    - freeze 如果属性是一个对象值的, 那么这个属性还是可以被修改的, 除非再次让这个属性为 freeze
    - Object.defineProperty 分别设置其 configurable 和 writable 为 false.

**参考**
* [JavaScript之防篡改对象（高级技巧）](https://blog.csdn.net/h15882065951/article/details/72229056)
* [让 JavaScript 对象完全只读不可以被修改](https://www.douban.com/note/602809588/)
* [深入理解javascript之防篡改对象](https://www.2cto.com/kf/201508/428682.html)

#### 3.24. 前端编码
#### --转义场景
* 使用URL
    - 标准URL只能使用英文、数字、某些部分标点符号，包含汉字的URL是无法直接使用的
    - 假如我们请求了上述包含汉字的地址，浏览器会帮我们做些转义工作。然而，不同浏览器在不同的操作系统，不同的网页编码，不同的请求方式下，使用的编码方式大相径庭，我们必须赶在浏览器之前对URL进行统一编码
* 表单提交或本地数据存储
    - 永远不要相信用户输入的内容。为了防止XSS攻击，我们需要对用户提交的表单进行HTML标签转义处理
* 使用JavaScript渲染页面
    - 页面上的一些功能经常会异步渲染，当用户点击时，才会通过Ajax异步获取数据，然后经JavaScript解析后渲染成HTML片段，最后拼接在页面上。假如返回的数据内容不可控，则需要尽可能的转义以保证渲染正确。

#### --编码函数
* `escape()`
    - 不能直接用于URL编码，它的真正作用是返回一个字符的Unicode编码值
    - 比如"春节"的返回结果是%u6625%u8282，，escape()不对"+"编码 主要用于汉字编码，现在已经不提倡使用。

* `encodeURI()`
    - 是Javascript中真正用来对URL编码的函数。 编码整个url地址，但对特殊含义的符号 `; / ? : @ & = + $ , #` ，也不进行编码
    - 对应的解码函数是：decodeURI()。

* `encodeURIComponent()`
    - 能编码 `; / ? : @ & = + $ , #` 这些特殊字符
    - 对应的解码函数是 decodeURIComponent()。

假如要传递带&符号的网址，所以用encodeURIComponent()

#### 3.25. JS 设计模式
##### 发布订阅模式

#### 3.26. 状态码

* 301 永久重定向 & 302
    - 从搜索引擎优化角度出发，301重定向是网址重定向最为可行的一种办法。当网站的域名发生变更后，搜索引擎只对新网址进行索引，同时又会把旧地址下原有的外部链接如数转移到新地址下，从而不会让网站的排名因为网址变更而收到丝毫影响。同样，在使用301永久性重定向命令让多个域名指向网站主域时，亦不会对网站的排名产生任何负面影响。
    - 302重定向可影响搜索引擎优化效果
    - 迄今为止，能够对302重定向具备优异处理能力的只有Google。也就是说，在网站使用302重定向命令将其它域名指向主域时，只有Google会把其它域名的链接成绩计入主域，而其它搜索引擎只会把链接成绩向多个域名分摊，从而削弱主站的链接总量。既然作为网站排名关键因素之一的外链数量受到了影响，网站排名降低也是很自然的事情了。
    - 综上所述，在众多重定向技术中，301永久性重定向是最为安全的一种途径，也是极为理想的一款解决方案。

[面试必考之http状态码有哪些](http://hpoenixf.com/%E9%9D%A2%E8%AF%95%E5%BF%85%E8%80%83%E4%B9%8Bhttp%E7%8A%B6%E6%80%81%E7%A0%81%E6%9C%89%E5%93%AA%E4%BA%9B.html)

## 4. 其他
[页面加载全解](https://www.cnblogs.com/jingwhale/p/4714082.html?utm_source=tuicool&utm_medium=referral)
#### 4.1. GET 和 POST
* 用途
    - get 是从服务器上获取数据
    - post 是向服务器传送数据。

* 参数传递方式
    - get 是把参数数据队列加到提交表单的 ACTION 属性所指的 URL 中，值和表单内各个字段一一对应，在 URL 中可以看到
    - post 是通过 HTTP post 机制，将表单内各个字段与其内容放置在 HTTP 的 body 内一起传送到 ACTION 属性所指的 URL 地址, 用户看不到这个过程。
    - post请求不能通过管道的方式进行通信

* 参数获取方式
    - 对于 get 方式，服务器端用 Request.QueryString 获取变量的值
    - 对于 post 方式，服务器端用 Request.Form 获取提交的数据。

* 参数
    - get 传送的数据量较小，不能大于 2KB
    - post 传送的数据量较大，一般被默认为不受限制。但理论上， IIS4 中最大量为 80KB ， IIS5 中为 100KB 。
    - post能发送更多的数据类型（get只能发送ASCII字符）

* post更安全（不会作为url的一部分，不会被缓存、保存在服务器日志、以及浏览器浏览记录中）

在以下情况中，请使用 POST 请求：
1. 无法使用缓存文件（更新服务器上的文件或数据库）
2. 向服务器发送大量数据（POST 没有数据量限制）
3. 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

**为什么get比post更快**
* post请求包含更多的请求头 
    
    因为post需要在请求的body部分包含数据，所以会多了几个数据描述部分的首部字段（如：content-type）,这其实是微乎其微的。

* 最重要的一条，post在真正接收数据之前会先将请求头发送给服务器进行确认，然后才真正发送数据 
    - post请求的过程： 

        - （1）浏览器请求tcp连接（第一次握手） 
        - （2）服务器答应进行tcp连接（第二次握手） 
        - （3）浏览器确认，并发送post请求头（第三次握手，这个报文比较小，所以http会在此时进行第一次数据发送） 
        - （4）服务器返回100 Continue响应 
        - （5）浏览器发送数据 
        - （6）服务器返回200 OK响应 
    - get请求的过程： 

    （1）浏览器请求tcp连接（第一次握手） 
    （2）服务器答应进行tcp连接（第二次握手） 
    （3）浏览器确认，并发送get请求头和数据（第三次握手，这个报文比较小，所以http会在此时进行第一次数据发送） 
    （4）服务器返回200 OK响应 


也就是说，目测get的总耗是post的2/3左右

更多：[学习前端前必知的——HTTP协议详解](http://www.cnblogs.com/chaoran/p/4783633.html)
[http GET 和 POST 请求的优缺点和误区 --前端优化](https://blog.csdn.net/zzk220106/article/details/78595108/)
[99%的人都理解错了HTTP中GET与POST的区别](http://www.techweb.com.cn/network/system/2016-10-11/2407736.shtml)

#### 4.2. 页面从输入 URL 到页面加载过程
![web请求](/img/in-post/post-php-study/web请求1.png)
![web请求](/img/in-post/post-php-study/web请求2.png)

* 检查浏览器缓存
* 检查操作系统缓存，常见的如hosts文件
* 检查路由器缓存
* 如果前几步都没没找到，会向ISP(网络服务提供商)的LDNS服务器查询
* 如果LDNS服务器没找到，会向跟域名服务器(Root Server)请求解析，分为以下几步：

    - 跟服务器返回顶级域名(TLD)服务器如.com，.cn，.org等的地址，全球只有13台，该例子中会返回.com的地址
    - 接着向TLD发送请求，然后会返回次级域名(SLD)服务器的地址，本例子会返回.example的地址
    - 接着向SLD域名服务器通过域名查询目标IP，Local DNS Server会缓存结果，并返回给用户，缓存在系统中。

**页面请求过程**

分为4个步骤：
1. 当发送一个 URL 请求时，不管这个 URL 是 Web 页面的 URL 还是 Web 页面上每个资源的 URL，浏览器都会开启一个线程来处理这个请求，同时在远程 DNS 服务器上启动一个 DNS 查询。这能使浏览器获得请求对应的 IP 地址。
2. 浏览器与远程 Web 服务器通过 TCP 三次握手协商来建立一个 TCP/IP 连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
3. 一旦 TCP/IP 连接建立，浏览器会通过该连接向远程服务器发送 HTTP 的 GET 请求。远程服务器找到资源并使用 HTTP 响应返回该资源，值为 200 的 HTTP 响应状态表示一个正确的响应。
4. 此时，Web 服务器提供资源服务，客户端开始下载资源。

请求返回后，便进入了我们关注的前端模块
简单来说，浏览器会解析 HTML 生成 DOM Tree，其次会根据 CSS 生成 CSS Rule Tree，而 javascript 又可以根据 DOM API 操作 DOM

**页面资源加载**
* 解析HTML结构
* 加载并解析外部脚本
* DOM树构建完成，执行脚本。//DOMInteractive –> DOMContentLoaded
* 加载图片、样式表文件等外部文件
* 页面加载完毕。`window.onload`

**涉及到的事件**

**ready & load**
![load](/img/in-post/post-web-nowcoder/load.png)
* 一是ready，表示文档结构（DOM结构）已经加载完成（不包含图片等非文字媒体文件）

* 二是onload，指示页面包含图片等文件在内的所有元素都加载完成。

    (可以说：ready 在onload 前加载！！！)

    一般样式控制的，比如图片大小控制放在onload 里面加载;而：jS事件触发的方法，可以在ready 里面加载;

**load**

* `document.onload: `

    整个html文档加载的时候触发
* `DOMContentLoaded:` 

    当页面的DOM树解析好并且需要等待JS执行完才触发 

    当初始的 HTML 文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而无需等待样式表、图像和子框架的完成加载
    ```js
    <script>
    document.addEventListener("DOMContentLoaded", function(event) {
        console.log("DOM fully loaded and parsed");
    });

    for(var i=0; i<1000000000; i++){
        // 这个同步脚本将延迟DOM的解析。
        // 所以DOMContentLoaded事件稍后将启动。
    } 
    </script>
    ```
    support
    ![support](/img/in-post/post-web-nowcoder/support.png)
    
* `onreadytstatechange: `
   
    发生在Document对象和XMLHttpRequest对象，它们的readyState属性发生变化时触发
    
    一个文档的 readyState 可以是以下之一：
    - uninitialized(未初始化)：对象存在但尚未初始化 
    - loading(正在加载)：对象正在加载数据
    - loaded(加载完毕)：对象加载数据完成
    - interactive(交互)：可以操作对象了，但还没有完全加载
    - complete(完成)：对象已经加载完毕

* `window.onload: `

    当页面全部加载完成（包括所有资源）

**document.ready的实现**

作用：监控dom是否加载完毕，dom加载完毕时及资源加载之前触发 
```js
document.ready = function(callback) {
    if (document.addEventListener) {
        document.addEventListener('DOMContentLoaded', function() {
            document.removeEventListener('DOMContentLoaded', arguments.callee, false);
            callback();
        }, false);
    }else if (document.attachEvent) {// 兼容ie
        document.attachEvent('onreadytstatechange', function() {
            if (document.readyState == "complete") {
                document.detachEvent("onreadystatechange", arguments.callee);
                callback();
            }
        });
    }
}
```

更多：
* [从输入 URL 到页面加载完的过程中都发生了什么事情？](http://www.cnblogs.com/chaoran/p/4795642.html)
* [资源加载和页面事件 load, ready, DOMContentLoaded等](http://blog.csdn.net/u011700203/article/details/47656857)

#### 4.3. 网站的文件和资源优化
1. 文件合并
2. 文件最小化/文件压缩
3. 使用 CDN 托管
4. 缓存的使用（多个域名来提供缓存）
5. cookie优化
5. 其他

**CDN**
> 就近访问，提供离用户最近，响应最快的节点

每个CDN节点由两部分组成:负载均衡设备和高速缓存服务器

当用户访问加入CDN服务的网站时，域名解析请求将最终交给全局负载均衡DNS进行处理。全局负载均衡DNS通过一组预先定义好的策略，将当时最接近用 户的节点地址提供给用户，使用户能够得到快速的服务。同时，它还与分布在世界各地的所有CDNC节点保持通信，搜集各节点的通信状态，确保不将用户的请求 分配到不可用的CDN节点上，实际上是通过DNS做全局负载均衡。

负载均衡设备负责每个节点中各个Cache的负载均衡，保证节点的工作效率;同时，负载均衡设备还负责收集节点与周围环境的信息，保持与全局负载DNS的通信，实现整个系统的负载均衡

![cdn](/img/in-post/post-web-nowcoder/cdn.png)
1.用户向浏览器输入www.web.com这个域名，浏览器第一次发现本地没有dns缓存，则向网站的DNS服务器请求；

2.网站的DNS域名解析器设置了CNAME，指向了www.web.51cdn.com,请求指向了CDN网络中的智能DNS负载均衡系统；

3.智能DNS负载均衡系统解析域名，把对用户响应速度最快的IP节点返回给用户；

4.用户向该IP节点（CDN服务器）发出请求；

5.由于是第一次访问，CDN服务器会向原web站点请求，并缓存内容；

6.请求结果发给用户。

**cookie 优化**
* 去除没有必要的cookie，如果网页不需要cookie就完全禁掉。

* 将cookie的大小减到最小。
    由于cookie在访问对应域名下的资源时都会通过HTTP请求发送到服务器，因此，减小cookie的大小，能减小HTTP请求报文的大小，提高响应速度。

* 设置合适的过期时间，较长的过期时间可以提高响应速度。
    给cookie添加一个过期时间，则cookie信息将存储到硬盘上，即使浏览器退出Cookie还会存在。只要Cookie未被清除且还在过期时间内，该Cookie就会在访问对应域名时发送给服务器。

* 通过使用不同的domain减少cookie的使用。
    cookie在访问对应域名下的资源时都会通过HTTP请求发送到服务器，但在访问一些资源，如js，css和图片时，大多数情况下cookie是多余的，可以使用不同的domain来存储这些静态资源，这样访问这些资源时就不会发送多余的cookie，从而提高响应速度。

测试代码性能
* Profiler
* JSPerf（http://jsperf.com/nexttick-vs-setzerotimeout-vs-settimeout）
* Dromaeo

更多：
* [网站性能优化](http://www.cnblogs.com/chaoran/p/4795800.html)
* [一张图说明CDN网络的原理](http://blog.csdn.net/coolmeme/article/details/9468743)


#### 4.4. 前端的安全问题
1. XSS (Cross Site Scripting) 跨站脚本攻击

    指攻击者在网页中嵌入客户端脚本(例如JavaScript), 当用户浏览此网页时，脚本就会在用户的浏览器上执行，从而达到攻击者的目的.  比如获取用户的Cookie，导航到恶意网站,携带木马等

    * 将重要的cookie标记为http only, 这样的话Javascript 中的document.cookie语句就不能获取到cookie了.
    * 只允许用户输入我们期望的数据
    * 对数据进行Html Encode 处理
    * 过滤或移除特殊的Html标签
    * 过滤JavaScript 事件的标签。例如 "onclick=", "onfocus" 等等。
2. sql注入
3. CSRF：（Cross-site request forgery）跨站请求伪造

    **CSRF的原理：**

    * CSRF攻击者在用户已经登录目标网站之后，诱使用户访问一个攻击页面，利用目标网站对用户的信任，以用户身份在攻击页面对目标网站发起伪造用户操作的请求，达到攻击目的
    
        核心是请求伪造，通过伪造身份提交POST和GET请求来进行跨域的攻击

    **与 XSS 区别：**

    * XSS是攻击者自己提交，等待结果，而CSRF呢，是由用户(管理员)自身提交

    完成CSRF需要两个步骤：
    * 登陆受信任的网站A，在本地生成 COOKIE
    * 在不登出A的情况下，或者本地 COOKIE 没有过期的情况下，访问危险网站B。

    **例子：**

    * 如用户当前已经登录了bbs，同时用户又在使用另外一个钓鱼网站。这个网站上面可能因为某个图片吸引你，你去点击一下，此时可能就会触发一个js的点击事件，构造一个发帖的请求，去往你的bbs发帖，由于当前你的浏览器状态已经是登陆状态，所以session登陆cookie信息都会跟正常的请求一样，纯天然的利用当前的登陆状态，让用户在不知情的情况下，帮你发帖或干其他事情

    **防范：**
    * 验证码、验证Refer、以及验证token，对特殊参数进行加密
    * 杜绝用户的一切外链资源。需要站外图片，可以抓回后保存在站内服务器里。
    * 对于富文本内容，使用白名单策略，只允许特定的 CSS 属性。
    * 尽可能开启 Content Security Policy 配置，让浏览器底层来实现站外资源的拦截。
    * 采用POST请求,增加攻击的难度.用户点击一个链接就可以发起GET类型的请求。而POST请求相对比较难，攻击者往往需要借助javascript才能实现
    * 对请求进行认证，确保该请求确实是用户本人填写表单并提交的，而不是第三者伪造的.具体可以在会话中增加token,确保看到信息和提交信息的是同一个人

    ![csrf](/img/in-post/post-web-nowcoder/csrf.jpg)
    
更多：[web 攻击](http://www.cnblogs.com/chaoran/p/6581024.html)

#### 4.5. css阻塞 && js阻塞
**页面加载：**
* 加载完静态资源后通过ajax请求去后台获取数据，数据回来后渲染内容
![load-order1](/img/in-post/post-web-nowcoder/load-order-1.png)
* 使用后台直出，返回的html已经带上内容了
![load-order2](/img/in-post/post-web-nowcoder/load-order-2.png)

1. DOM 加载到 link 标签
    css 文件的加载是与 DOM 的加载并行的，也就是说，css 在加载时 Dom 还在继续加载构建，而过程中遇到的 css 样式或者 img，则会向服务器发送一个请求，待资源返回后，将其添加到 dom 中的相对应位置中；

2. DOM加载到 script 标签
    由于js文件不会与 DOM 并行加载，因此需要等待 js 整个文件加载完之后才能继续 DOM 的加载，倘若 js 脚本文件过大，则可能导致浏览器页面显示滞后，出现“假死”状态，这种效应称之为“阻塞效应”；会导致出现非常不好的用户体验；

js阻塞其他资源的加载的原因是：**浏览器为了防止js修改DOM树，需要重新构建DOM树的情况出现**

**js 阻塞**
* 特性：
    > 所有浏览器在下载 JS 的时候，会阻止一切其他活动，比如其他资源的下载，内容的呈现等等。直到 JS 下载、解析、执行完毕后才开始继续并行下载其他资源并呈现内容。为了提高用户体验，新一代浏览器都支持并行下载 JS，但是 JS 下载仍然会阻塞其它资源的下载（例如.图片，css文件等）。

    - 由于浏览器为了防止出现 JS 修改 DOM 树，需要重新构建 DOM 树的情况，所以就会阻塞其他的下载和呈现。
    - 嵌入 JS 会阻塞所有内容的呈现
    - 外部 JS 只会阻塞其后内容的显示
    - 2 种方式都会阻塞其后资源的下载
    也就是说外部样式不会阻塞外部脚本的加载，但会阻塞外部脚本的执行。

**CSS 阻塞**
> CSS 本来是可以并行下载的，在什么情况下会出现阻塞加载了(在测试观察中，IE6 下 CSS 都是阻塞加载）

当 CSS 后面跟着嵌入的 JS 的时候，该 CSS 就会出现阻塞后面资源下载的情况。而当把嵌入 JS 放到 CSS 前面，就不会出现阻塞的情况了（css文件可以和body里的请求并行）。
根本原因：因为浏览器会维持 html 中 css 和 js 的顺序，样式表必须在嵌入的 JS 执行前先加载、解析完。而嵌入的 JS 会阻塞后面的资源加载，所以就会出现上面 CSS 阻塞下载的情况。

**嵌入JS应该放在什么位置？**
1. 放在底部，虽然放在底部照样会阻塞所有呈现，但不会阻塞资源下载。
2. 如果嵌入JS放在head中，请把嵌入JS放在CSS头部。
3. 使用 defer
4. 不要在嵌入的JS中调用运行时间较长的函数，如果一定要用，可以用 setTimeout 来调用

**Javascript无阻塞加载具体方式：**
1. 将脚本放在底部。link 还是放在head中，用以保证在js加载前，能加载出正常显示的页面。script 标签放在 /body 前。
2. 阻塞脚本：由于每个 script 标签下载时阻塞页面解析过程，所以限制页面 script 总数也可以改善性能。适用于内联脚本和外部脚本。
3. 非阻塞脚本：等页面完成加载后，再加载js代码。也就是，在 window.onload 事件发出后开始下载代码。
4. defer属性：支持IE4和firefox3.5更高版本浏览器
5. 动态脚本元素：文档对象模型（DOM）允许你使用js动态创建HTML的几乎全部文档内容。代码如下：
    ```js
    <script>
        var script=document.createElement("script");
        script.type="text/javascript";
        script.src="file.js";
        document.getElementsByTagName("head")[0].appendChild(script);
    </script>
    ```
    此技术的重点在于：无论在何处启动下载，文件额下载和运行都不会阻塞其他页面处理过程，即使在head里（除了用于下载文件的 http 链接）。

#### 4.6. 线程与进程
1. 一个程序至少有一个进程,一个进程至少有一个线程
2. 线程的划分尺度小于进程，使得多线程程序的并发性高
3. 进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率
4. 线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制 
5. 从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别

#### 4.7. 服务器推送
1. html5 websocket
2. WebSocket 通过 Flash
3. XHR 长轮询
    客户端向服务器发送Ajax请求，服务器接到请求后hold住连接，直到有新消息才返回响应信息并关闭连接，客户端处理完响应信息后再向服务器发送新的请求。 
4. XHR Multipart Streaming
5. 不可见的Iframe
    在页面里嵌入一个隐蔵iframe，将这个隐蔵iframe的src属性设为对一个长连接的请求或是采用xhr请求，服务器端就能源源不断地往客户端输入数据。 
6. script 标签的长时间连接(可跨域)

#### 4.8. Gulp、Webpack比较
Gulp
> 为规范前端开发流程，实现前后端分离、模块化开发、版本控制、文件合并与压缩、mock数据等功能的一个前端自动化构建工具。


* 就像是一个产品的流水线，整个产品从无到有，都要受流水线的控制，在流水线上我们可以对产品进行管理。
* 是通过task对整个开发过程进行构建。

Webpack
* 当下最热门的前端资源模块化管理和打包工具
* 可以很好的管理模块以及各个模块之间的依赖
* 对js、css、图片等资源文件都支持打包
* 有独立的配置文件webpack.config.js
* 可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间
* 可以生成优化且合并后的静态资源

两大特色：
* 代码可以自动完成编译。
* loader 可以处理各种类型的静态文件，并且支持串联操作

区别
* 是一种工具 —— 优化前端的工作流程

    比如自动刷新页面、combo、压缩 css、js、编译 less 等等
* webpack 则是一种打包工具，或者说是一种模块化解决方案
* gulp 的处理任务需要自己去写，webpack 则有现成的解决方案，只需要在webpack.config.js 配置好即可;

#### 4.9. 三次握手
> TCP在传输之前会进行三次沟通，一般称为“三次握手”，传完数据断开的时候要进行四次沟通，一般称为“四次挥手”。

两个序号和六个标志位：
两个序号位：
* 序号：seq序号，占32位，用来标识从TCP源端向目的端发送的字节流，发起方发送数据时对此进行标记。
* 确认序号：ack序号，占32位，只有ACK标志位为1时，确认序号字段才有效，ack=seq+1。

标志位
* URG：紧急指针（urgent pointer）有效。
* ACK：确认序号有效。
* PSH：接收方应该尽快将这个报文交给应用层。
* RST：重置连接。
* SYN：发起一个新连接。
* FIN：释放一个连接。

![tcp](/img/in-post/post-web-nowcoder/tcp.png)
1. 客户端给服务器发送数据包（带SYN标志的数据包）。此时服务器确认自己可以接收客户端的包，而客户端不确认服务器是否接收到了自己发的数据包。

2. 服务器端回复（回传一个带有SYN/ACK标志的数据包以示传达确认信息）客户端。此时客户端确认自己发的包被服务器收到，也确认自己可以正常接收服务器包，客户端对此次通信没有疑问了。服务器也可以确认自己能接收到客户端的包，但不能确认客户端能否接收自己发的包。

3. 客户端回复（发送端再回传一个带ACK标志的数据包，代表“握手”结束）服务器。客户端已经没有疑问了，服务器也确认刚刚客户端收到了自己的数据包。两边都没有问题，开始通信。

为什么要三次握手：
* 为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。也防止了服务器端的一直等待而浪费资源
* TCP作为一种可靠传输控制协议，其核心思想：既要保证数据可靠传输，又要提高传输的效率，而用三次恰恰可以满足以上两方面的需求！

四次挥手
1. 主机向服务器发送一个断开连接的请求（不早了，我该走了）,发送一个FIN报文段；
2. 服务器接到请求后发送确认收到请求的信号（知道了）回一个ACK报文段；
3. 服务器向主机发送断开通知（我也该走了）发送FIN报文段，请求关闭连接；
4. 主机接到断开通知后断开连接并反馈一个确认信号（嗯，好的），服务器收到确认信号后也断开连接；

#### 4.10. TCP和UDP的区别
* TCP（Transmission Control Protocol，传输控制协议）是基于连接的协议，也就是说，在正式收发数据前，必须和对方建立可靠的连接。一个TCP连接必须要经过三次“对话”才能建立起来

* UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是面向非连接的协议，它不与对方建立连接，而是直接就把数据包发送过去！
UDP适用于一次只传送少量数据、对可靠性要求不高的应用环境。

#### 4.11. HTTP HTTPS HTTP2.0
![tcp](/img/in-post/post-web-nowcoder/http.png)

**HTTP HTTPS**
![http](/img/in-post/post-web-nowcoder/http-https.png)

* HTTP协议通常承载于TCP协议之上，在HTTP和TCP之间添加一个安全协议层（SSL或TSL），这个时候，就成了我们常说的HTTPS
* 默认HTTP的端口号为80，HTTPS的端口号为443
* HTTPS 相对于HTTP 性能上差点，因为多了SSL/TLS 的几次握手和加密解密的运算处理，但是加密解密的运算处理已经可以通过特有的硬件来加速处理。

**HTTP1.0 & HTTP1.1**
* http1.0 性能

    - 每一个传输都需要建立TCP连接、传输数据、释放TCP连接

        三次握手建立TCP连接的过程中，通信双方会在SYN报文段（前两次握手）中“选项”字段的MSS（最大报文段长度）值来协商数据传输最大传输数据大小。HTTP请求是封装在TCP报文段中进行传输的，但是如果客户端发送的HTTP请求报文的长度大于MSS时，缓慢的建立使每一个TCP连接增加了额外的时延

* http1.1

    - 使用了持续的TCP连接（长连接）
    
        只用一次TCP连接就可以传输一个页面所需的所有资源，从而避免了不必要的时间浪费
        - 单独的网页的请求和应答使用单独的TCP连接
        
            也就是说客户端访问另外一个网页，需要建立一条新的TCP连接

        - 实现 TCP 持续连接

            请求头中新加入了一个字段Connection
            - 例如，当一个HTTP请求头中Connection字段值为Keep-Alive时（Connection: Keep-Alive），用来告诉服务器对这个请求返回后客户端与服务器端继续保持TCP连接。
            - 如果HTTP请求头中Connection字段值为Close时（Connection: Close），用来告诉服务器对这个请求返回后断开客户端与服务器端继续保持TCP连接

    - 支持请求流水线（流水线）

        使用持续TCP连接的非流水线数据传输时，当客户端没有收到上一个http请求的响应报文之前是不会发送下一个http请求的
        - 带有流水线的持续TCP连接。也就说当客户端需要一个资源时就向服务器发送一个请求，不受上一次请求的响应报文的约束。但服务器端必须按照接收到客户端请求的先后顺序依次回送响应结果，以保证客户端能够区分出每次请求的响应内容。

    - 100-continue响应码（节约带宽）

        如果客户端想要发送数据量很大的请求时，客户端在发送之前先发送一个只含有请求头的http报文。
        - 如果服务器拒绝请求，返回响应码为401的响应报文，这样客户端就不会发送这个大的请求报文。
        - 如果服务器允许该请求，会返回响应码为100的响应报文，客户端就可以发送大的请求报文了

        使用
        - 客户端在发request消息body之前先用只含header的request试探一下server，看server是否允许接收这个request，再决定要不要发request body
        - 客户端的request的header中有"Expect: 100-continue"字段，server看到这request后返回响应报文。如果客户端收到100响应码的响应报文，客户端发送完整request

    步骤
    - 三次握手建立TCP连接

    - 客户端发送HTTP请求报文

    - 服务器端返回HTTP响应报文

    - 服务器端释放连接

    


**HTTP2.0的新特性**
> 预先加载，合并请求，缩小数据，提升性能

* 新的二进制格式（Binary Format）
    - HTTP1.x的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的表现形式有多样性，要做到健壮性考虑的场景必然很多
    - 二进制则不同，只认0和1的组合。基于这种考虑HTTP2.0的协议解析决定采用二进制格式，实现方便且健壮。
* 多路复用（MultiPlexing）

    即连接共享，即每一个request都是是用作连接共享机制的。

    一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面。多路复用原理图：
![multiplexing](/img/in-post/post-web-nowcoder/multiplexing.png)
* header压缩

    HTTP1.x的header带有大量信息，而且每次都要重复发送，HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。
* 服务端推送（server push）

> 产生背景：

HTTP 1.1时代，每个TCP连接一次只能下载一个资源，比如浏览器发送一个请求获取index.html的数据，服务端收到后只会返回index.html，随后浏览器会解析index.html，如果里面含有 `<link rel="stylesheet"href="xxx.css">或<scriptsrc="app.js"></script>` ，则会再次向服务器发送请求，获取xxx.css和app.js的数据。 这一过程会产生 三个性能问题：
如果index.html里含有多个js和css文件，请求数则随之增加，从而导致在TCP往返连接所耗费的时间增多。
每次发送的请求，HTTP头部信息基本是一样的，从而导致一定的头部信息冗余，耗费了不必要的流量。
index.html与内部的资源文件之间会产生了一个延时，而非同步获取。

![http2](/img/in-post/post-web-nowcoder/http2.0.jpg)
* 因为是同一个请求，因此 HTTP头信息 只需要有一个就足够，下图可看出，HTTP/2中一个请求头中允许有多个方法，既可以GET，也可以PUT，在切换到下一个方法时，只需要获取数据即可，而不用再次获取头信息
* HTTP/2 新加入了 PUSH 方法，该方法的主要作用就是让服务器试探性的去推送信息给客户端，如问题3 中所述情况，当请求index.html时，服务器在返回index.html的同时，会主动把xxx.css和app.js一同发送给浏览器。这样当浏览器解析DOM，准备发送请求获取xxx.css和app.js的时候，也许两个资源已经下载完了，只需要从缓存中获取即可。这样就大大减少了网络请求的时间。

**对前端的影响**
* 减少HTTP请求不一定提升性能
    - 使用HTTP/2后，合并为一个大文件的加载时间反而会比不合并更长
* 压缩仍然需要
* 如何使用 HTTP/2
    - 如何使用 HTTP/2
    
    虽然目前规范中并没有达成一致意见来决定HTTP/2 是否需要加密（ Encryption ），但目前主流的实施方案都是需要加密的（如SSL/TLS），因此，如同 HTTPS，HTTP/2 同样需要创建公私密钥，来搭建站点
    - 搭建服务

![http2-support](/img/in-post/post-web-nowcoder/http2-support.jpg)


更多了解：
* [学习前端前必知的——HTTP协议详解](http://www.cnblogs.com/chaoran/p/4783633.html)
* [HTTP,HTTP2.0,SPDY,HTTPS你应该知道的一些事](http://web.jobbole.com/87695/)
* [谈谈HTTP/2对前端的影响](https://mp.weixin.qq.com/s/aFGMPhL3PpjGS4ZKtypeSQ)

#### 4.12. 页面加载优化
* 懒加载（延迟加载）
    - 延迟加载或符合某些条件时才加载某些资源
    - 主要目的是作为服务器前端的优化，减少请求数或延迟请求数

    实现方式：

    - 第一种是纯粹的延迟加载，使用setTimeOut或setInterval进行加载延迟。
    - 第二种是条件加载，符合某些条件，或触发了某些事件才开始异步下载。
    - 第三种是可视区加载，即仅加载用户可以看到的区域，这个主要由监控滚动条时正好能看到图片
* 预加载

    - 牺牲服务器前端性能，换取更好的用户体验，这样可以使用户的操作得到最快的反映
     
    实现方式：

    - 实现预载的方法非常多，可以用 CSS(background)、JS(Image)、HTML(`<img />`)都可以。
    
    - 常用的是 `new Image();` 设置其src来实现预载，再使用onload方法回调预载完成事件。只要浏览器把图片下载到本地，同样的src就会使用缓存，这是最基本也是最实用的预载方法。当Image下载完图片头后，会得到宽和高，因此可以在预载前得到图片的大小(方法是用记时器轮循宽高变化)

    ```css
    /* css */

    #preload-01 { background: url(http://domain.tld/image-01.png) no-repeat -9999px -9999px; }  
    #preload-02 { background: url(http://domain.tld/image-02.png) no-repeat -9999px -9999px; }  
    #preload-03 { background: url(http://domain.tld/image-03.png) no-repeat -9999px -9999px; }
    ```
    将这三个ID选择器应用到(X)HTML元素中，我们便可通过CSS的background属性将图片预加载到屏幕外的背景上。只要这些图片的路径保持不变，当它们在Web页面的其他地方被调用时，浏览器就会在渲染过程中使用预加载（缓存）的图片。简单、高效，不需要任何 JavaScript

    **不足：**
    该法加载的图片会同页面的其他内容一起加载，增加了页面的整体加载时间

    ```js
    // 增加了一些JavaScript代码，来推迟预加载的时间，直到页面加载完毕

    // 1. 获取使用类选择器的元素，并为其设置了background属性，以预加载不同的图片
    // 2. 使用addLoadEvent()函数来延迟preloader()函数的加载时间，直到页面加载完毕

    function preloader() {  
        if (document.getElementById) {  
            document.getElementById("preload-01").style.background = "url(http://domain.tld/image-01.png) no-repeat -9999px -9999px";  
            document.getElementById("preload-02").style.background = "url(http://domain.tld/image-02.png) no-repeat -9999px -9999px";  
            document.getElementById("preload-03").style.background = "url(http://domain.tld/image-03.png) no-repeat -9999px -9999px";  
        }  
    }  
    function addLoadEvent(func) {  
        var oldonload = window.onload;  
        if (typeof window.onload != 'function') {  
            window.onload = func;  
        } else {  
            window.onload = function() {  
                if (oldonload) {  
                    oldonload();  
                }  
                func();  
            }  
        }  
    }  
    addLoadEvent(preloader);
    ```

    ```js
    // 使用Ajax实现预加载

    // 利用DOM，不仅仅预加载图片，还会预加载CSS、JavaScript等相关的东西
    // 使用Ajax，比直接使用JavaScript，优越之处在于JavaScript和CSS的加载不会影响到当前页面

    window.onload = function() {  
        setTimeout(function() {  
            // XHR to request a JS and a CSS  
            var xhr = new XMLHttpRequest();  
            xhr.open('GET', 'http://domain.tld/preload.js');  
            xhr.send('');  
            xhr = new XMLHttpRequest();  
            xhr.open('GET', 'http://domain.tld/preload.css');  
            xhr.send('');  
            // preload image  
            new Image().src = "http://domain.tld/preload.png";  
        }, 1000);  
    };
    ```

- 京东优化（前端缓存和异步加载jd）

    - jd.com已经将它们的页面结构放到了localstorage
    - DOM lazyload
    - 把需要请求的路径写在 dom 上
    
        （例如:data-tpl="elevator_tpl"）
        ```html
        <div class="J_f J_lazyload J_f_lift mod_lazyload need_ani chn" id="portal_8" data-backup="basic_8" data-source="cms:basic_8" data-tpl="portal_tpl">
        ```
        - 用户滚动时，一旦该模块进入了视窗，则请求 dom 上对应的 data-tpl 地址，拿到渲染这个模块所需要的脚本和数据，不过这中间还有一层本地缓存 localstorage
        - 如果在本地缓存中匹配到了对应的 hash string 内容，则直接渲染，否则请求到数据之后更新本地缓存。
        - localstorage中的 version 会在页面加载时候，与后端文件 hash相对比，hash不变直接取localstorage中的内容（当然也可以使用cookie判断版本）

    - css静态文件

        - 首页是没有css外链
        - 页面切分为模块化加载，对应模块下的css交给js或jsonp请求返回
    - js文件怎么加载

        采用请求的方式减少了与服务器交互的时间
        ```html
        <script src="//misc.360buyimg.com/??/jdf/lib/jquery-1.6.4.js,/jdf/2.0.0/ui/ui/1.0.0/ui.js,/mtd/pc/index/gb/lib.min.js,/mtd/pc/base/1.0.0/base.js,/mtd/pc/common/js/o2_ua.js,/mtd/pc/index/home/index.min.js,/mtd/pc/index/home/init.min.js"></script>
        ```

    - 服务器

        - 少量静态文件的域名，图片与iconfont均是放在同一个域下，减少DNS的解析事件，最好做到域名收敛
        - 模块化接口的支持
        - 首屏内容最好做到静态缓存

#### 4.13. 浏览器缓存机制
* [详解HTTP缓存](https://www.cnblogs.com/isLiu/p/8335235.html)
* [彻底弄懂HTTP缓存机制及原理](https://www.cnblogs.com/chenqf/p/6386163.html)

#### 4.14. 前端存储方式
* cookie
    - 随请求发送，只能字符串， 大小< 4k，一个浏览器下的个数< 20 , 主domain 污染
* localstorage
    - 键值对方式存储，数据为字符串格式，如需存储对象需要JSON.stringfy()，永不失效，手动删除，同域共享，本页操作时会触发其他页面的storage事件，受同源策略限制

    
* sessionStorage
    - 相同：在本地（浏览器端）存储数据
    - 不同：
        - localStorage、sessionStorage

        - localStorage只要在相同的协议、相同的主机名、相同的端口下，就能读取/修改到同一份localStorage数据。

        - sessionStorage比localStorage更严苛一点，除了协议、主机名、端口外，还要求在同一窗口（也就是浏览器的标签页）下。

        - localStorage是永久存储，除非手动删除。

        - sessionStorage当会话结束（当前页面关闭的时候，自动销毁）

        - cookie的数据会在每一次发送http请求的时候，同时发送给服务器而localStorage、sessionStorage不会

* web SQL database--（关系型）
* indexedDB
    - 对象仓库 objectStore， 可存放多种类型的数据
    - 可以使用每条记录中的某个指定字段作为键值（keyPath），也可以使用自动生成的递增数字作为键值（keyGenerator），也可以不指定。选择键的类型不同，objectStore可以存储的数据结构也有差异

* 离线缓存（application cache）
    - manifest
    - 离线缓存与传统浏览器缓存区别：
        - 离线缓存是针对整个应用，浏览器缓存是单个文件
        - 离线缓存断网了还是可以打开页面，浏览器缓存不行
        - 离线缓存可以主动通知浏览器更新资源

[关于前端存储](https://www.cnblogs.com/youngGao/p/8127321.html)
[前端HTML5几种存储方式的总结](https://www.cnblogs.com/LuckyWinty/p/5699117.html)

#### 4.15. webpack 打包文件过大
* 去除不必要的插件
* 提取第三方库
* 代码压缩
    webpack-UglifyJsPlugin
* 代码分割
    - webpack 的 code split 以及配合 react router 
* 设置缓存

[大公司里怎样开发和部署前端代码](https://github.com/fouber/blog/issues/6)

#### 4.15. 前端防抖与节流
> 假设网站有个搜索框, 用户输入文本我们会自动联想匹配出一些结果供用户选择,我们可能首先想到的做法就是监听keypress事件, 然后异步查询结果. 但是如果用户快速的输入了一串字符, 假设是10个字符, 那么就会在瞬间触发10次请求 —— 想要的是用户停止输入的时候才去触发查询的请求

##### 函数防抖
> 通过限制需要经过的时间，直到再次调用函数

让某个函数在上一次执行后, 满足等待某个时间内不再触发此函数后再执行, 而在这个等待时间内再次触发此函数, 等待时间会重新计算.

* 原生实现

    ```js
    // debounce函数用来包裹我们的事件
    function debounce(fn, delay) {
    // 持久化一个定时器 timer
    let timer = null;
    // 闭包函数可以访问 timer
    return function() {
        // 通过 'this' 和 'arguments'
        // 获得函数的作用域和参数
        let context = this;
        let args = arguments;
        // 如果事件被触发，清除 timer 并重新开始计时
        clearTimeout(timer);
        timer = setTimeout(function() {
        fn.apply(context, args);
        }, delay);
    }
    }
    ```

    ```js
    // 使用
    // 当用户滚动时函数会被调用
    function foo() {
    console.log('You are scrolling!');
    }
    
    // 在事件触发的两秒后，我们包裹在debounce中的函数才会被触发
    let elem = document.getElementById('container');
    elem.addEventListener('scroll', debounce(foo, 2000));
    ```


* underscore.js的函数防抖定义: `_.debounce(fn, wait, [immediate]);`

    ```js
    debounce接收三个参数:
    @params fn: 需要进行函数防抖的函数;
    @params wait: 需要等待的时间, 单位为毫秒;
    @params immediate: 如果为true, 则debounce会在调用时立刻执行一次fn,
                    而不需要等到wait结束后.

    _.debounce = function(fn, wait, immediate) {
        var timeout,
            args,
            context,
            timestamp,
            result;

        var later = function() {
            var last = _.now() - timestamp;

            if(last < wait && last >= 0) {
                timeout = setTimeout(later, wait - last);
            } else {
                timeout = null;
                if(!immediate) {
                    result = fn.apply(context, args);

                    if(!timeout) {
                        context = args = null;
                    }
                }
            }
        };

        return function() {
            context = this;
            args = arguments;
            timestamp = _.now();
            var callNow = immediate && !timeout;

            if(!timeout) {
                timeout = setTimeout(later, wait);
            }

            if(callNow) {
                result = fn.apply(context, args);
                context = args = null;
            }

            return result;
        }
    };

    // demo:
    $('#input').keypress(_.debounce(function() {
        //异步调用查询
    }, 300));
    ```

##### 函数节流
> 是另一个类似函数防抖的技巧，除了使用等待一段时间再调用函数的方法，函数节流还限制固定时间内只能调用一次。所以一个事件如果在100毫秒内发生10次，函数节流会每2秒调用一次函数，而不是100毫秒内全部调用。

* `_.throttle`

    ```js
    function throttle(fn, delay){
        var last = 0
        return function(){
            var curr = +new Date()
            if(curr - last > delay){
            fn.apply(this, arguments)
            last = curr
            }
        }
    }
    ```

* `requestAnimationFrame（rAF）`
    - 优点
        - 动画保持 60fps（每一帧 16 ms），浏览器内部决定渲染的最佳时机
        - 简洁标准的 API，后期维护成本低
    - 缺点
        - 动画的开始/取消需要开发者自己控制，不像 ‘.debounce’ 或 ‘.throttle’由函数内部处理。
        - 浏览器标签未激活时，一切都不会执行。
        - 尽管所有的现代浏览器都支持 rAF，IE9，Opera Mini 和 老的 Android 还是需要打补丁。
        - Node.js 不支持，无法在服务器端用于文件系统事件。

* 如果 JavaScript 方法需要绘制或者直接改变属性，我会选择 requestAnimationFrame，只要涉及到重新计算元素位置，就可以使用它。

* 涉及到 AJAX 请求，添加/移除 class （可以触发 CSS 动画），我会选择 _.debounce 或者 _.throttle ，可以设置更低的执行频率（例子中的200ms 换成16ms）

**总结**
* debounce：把触发非常频繁的事件（比如按键）合并成一次执行。
* throttle：保证每 X 毫秒恒定的执行次数，比如每200ms检查下滚动位置，并触发 CSS 动画。
* requestAnimationFrame：可替代 throttle ，函数需要重新计算和渲染屏幕上的元素时，想保证动画或变化的平滑性，可以用它。注意：IE9 不支持

#### 4.16. 优雅降级 & 渐进增强
**优雅降级：**

* Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会针对旧版本的IE进行降级处理了,使之在旧式浏览器上以某种形式降级体验却不至于完全不能用。 
    - 如：border-shadow 

**渐进增强：**
* 从被所有浏览器支持的基本功能开始，逐步地添加那些只有新版本浏览器才支持的功能,向页面增加不影响基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。 
    - 如：默认使用flash上传，但如果浏览器支持 HTML5 的文件上传功能，则使用HTML5实现更好的体验


## 5. 代码
#### 5.1. 通用的事件监听器
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


#### 5.2. 实现事件模型（发布-订阅）
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

#### 5.3. bind
> bind() 函数会创建一个新函数（称为绑定函数），新函数与被调函数（绑定函数的目标函数）具有相同的函数体（在 ECMAScript 5 规范中内置的call属性）。
当目标函数被调用时 this 值绑定到 bind() 的第一个参数，该参数不能被重写。绑定函数被调用时，bind() 也接受预设的参数提供给原函数。

**思路**
* 因为bind方法不会立即执行函数，需要返回一个待执行的函数
    （这里用到**闭包**，可以返回一个函数）`return function(){}`
* 作用域绑定
    这里可以使用apply或者call方法来实现 `xx.call(yy) / xx.apply(yy)`
* 参数传递
    由于参数的不确定性，需要用apply传递数组（实例更明了）`xx.apply(yy,[...Array...])` 

```js
Function.prototype.testBind = function(that){
    var _this = this,
    
    // 由于参数的不确定性，统一用arguments来处理，这里的arguments只是一个类数组对象，有length属性
    // 可以用数组的slice方法转化成标准格式数组，除了作用域对象that以外，
    // 后面的所有参数都需要作为数组参数传递
    // Array.prototype.slice.apply(arguments,[1])/Array.prototype.slice.call(arguments,1)

    slice = Array.prototype.slice,
    args = slice.apply(arguments,[1]);
    //返回函数    
    return function(){
        //apply绑定作用域，进行参数传递
        return _this.apply(that,
            args.concat(Array.prototype.slice.apply(arguments,[0]))
        )
    }    
}

//test
var test = function(a,b){
    console.log('作用域绑定 '+ this.value)
    console.log('testBind参数传递 '+ a.value2)
    console.log('调用参数传递 ' + b)
}
var obj = {
    value:'ok'
}
var fun_new = test.testBind(obj,{value2:'also ok'})

fun_new ('hello bind')

// 作用域绑定 ok
// testBind参数传递 also ok
// 调用参数传递 hello bind

//  Array.prototype.slice.apply(arguments,[0]) 指的是这个返回函数执行的时候传递的一系列参数，所以是从第一个参数开始 [0] 
// args = slice.apply(arguments,[1])指的是 testBind方法执行时候传递的参数，所以从第二个开始 [1]
// 只有两者合并了之后才是返回函数的完整参数
```

#### 5.4. 将url的查询参数解析成字典对象
> 解决方案:拆字符或者用正则匹配来解决
烈建议用正则匹配，因为url允许用户随意输入，如果用拆字符的方式，有任何一处没有考虑到容错，就会导致整个js都报错

```js
function getQueryObject(url) {
    url = url == null ? window.location.href : url;
    var search = url.substring(url.lastIndexOf("?") + 1);
    var obj = {};
    var reg = /([^?&=]+)=([^?&=]*)/g;
    search.replace(reg, function (rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);
        val = String(val);
        obj[name] = val;
        return rs;
    });
    return obj;
}
```

#### 5.5. 数组去重
建一个空对象和空数组，循环遍历需要去重的数组，判断对象有没有此属性，没有的话就给对象添加此属性，并向空数组中push这个值。
```js
//es5
function unique(arr){
    var obj = {}
    var result = []
    for(var i in arr){
        if(!obj[arr[i]]){
            obj[arr[i]] = true;
            result.push(arr[i]);
        }
    }
    return result;
}
//es6
[...new Set(arr)]
```

#### 5.6. 冒泡排序
相邻两个对比，最后把最大的排到了最后，重复此过程。
```js
functionbubbleSort(arr) {
      var len = arr.length;
   for (var i = 0; i < len; i++) {
        for (var j = 0; j < len - 1 - i; j++) {
                 if (arr[j] > arr[j+1]) {        //相邻元素两两对比
                              var temp = arr[j+1];        //元素交换
                              arr[j+1] = arr[j];
                             arr[j] = temp;
                  }
              }
       }
       return arr;
}
```

#### 5.7. 选择排序
寻找最小的数，保存索引，然后与第一层循环其下标对于的值进行交换
```js
functionselectionSort(arr) {
   var len = arr.length;
   var minIndex, temp;
     for (var i = 0; i < len - 1; i++) {
            minIndex = i;
          for (var j = i + 1; j <len; j++) {
                     if (arr[j] < arr[minIndex]) {     //寻找最小的数
                              minIndex = j;                 //将最小数的索引保存
                       }
              }
              temp = arr[i];
         arr[i] =arr[minIndex];
        arr[minIndex] =temp;
   }
       return arr;
}
```

#### 5.8. 快速排序
选取一个记录作为中间轴，然后将比‘这个记录值’小的移到‘记录值’之前，大的移到之后，然后递归
```js
functionquickSort(arr) {
    if (arr.length == 0) {
        return []; // 返回空数组
    }
    var cIndex = Math.floor(arr.length / 2);
    var c = arr.splice(cIndex, 1);
    var l = [];
    var r = [];
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < c) {
            l.push(arr[i]);
        } else {
            r.push(arr[i]);
        }
    }
    return quickSort(l).concat(c, quickSort(r));
}
```