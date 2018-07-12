---
layout:     post
title:      "mpvue holes"
subtitle:   "basic knowledge"
date:       2018-07-09 22:00:00
author:     "Chaoran"
header-img: "img/post-bg-php-basic.jpg"
noToc:      true
tags:
    - 前端开发
    - 小程序
    - mpvue
---

> “To be a better girl ”

* 目录
{:toc #toc}

## 1. 不支持
* v-html
  - 小程序里所有的 BOM／DOM 都不能用，也就是说 v-html 指令不能用

* 部分复杂的 JavaScript 渲染表达式
  - {{}} 双花括号的部分，直接编码到 wxml 文件中，小程序能力限制
  - 小程序支持运算
    - 三元运算
    - 算数运算
    - 逻辑判断
    - 字符串运算 （+连接等）

* 过滤器
* template 中使用methods 中的函数

## 2. 规范
#### 2.1. 变量绑定
**使用 vue.js 规范**
```html
<!-- 小程序 -->
<view class="tab-item {{currentTab==0 ? 'on' : ''}}" >超然haha</view>
<view  current="{{currentTab}}"  style="height:{{currentTab==1?Height+'rpx':'100%'}}">超然haha</view>

<!-- vue.js -->
<view class="tab-item" :class="{'on': currentTab==0 ? true : false}" >超然haha</view>
<view  :current="currentTab"  :style="{'height':currentTab==1 ? Height+'rpx':'100%'}">超然haha</view>
```

#### 2.1. 事件处理
小程序原生事件 ---> vue.js 规范
![mp-架构](/img/in-post/post-mp-vue-holes/function.png)
* 列表中没有的原生事件也可以使用例如 `bindregionchange` 事件直接在 `dom` 上将 `bind` 改为@ `@regionchange`,在监听此类事件的时候同时监听事件名和事件类型既 `<map @regionchange="functionName" @end="functionName" @begin="functionName"><map>`

* 不支持组件引用时原生事件

**关于修饰符**

* .stop 的使用会阻止冒泡，但是同时绑定了一个非冒泡事件，会导致该元素上的 catchEventName 失效！
* .prevent 可以直接干掉，因为小程序里没有什么默认事件，比如submit并不会跳转页面
* .capture 支持 1.0.9
* .self 没有可以判断的标识
* .once 也不能做，因为小程序没有 removeEventListener, 虽然可以直接在 handleProxy 中处理，但非常的不优雅，违背了原意，暂不考虑

## 3. 组件
#### 3.1. 限制
* **只能使用单文件组件（.vue 组件）的形式进行支持**
  - 其他的诸如：动态组件，自定义 render，和 `<script type="text/x-template">` 字符串模版等都不支持
* 组件上定义原生事件
* v-show---》v-if
* slot
* 动态组件
* 异步组件
* inline-template
* X-Templates
* keep-alive
* transition
* class
* style

#### 3.2. 小程序组件使用
* 原生组件的事件绑定需用vue语法

## 4.0. 参数获取
* page onLoad 时候传递的 options
  - `this.$root.$mp.query`
  - 也可以通过 onLoad 方法

* app onLaunch/onShow 的参数
  - `this.$root.$mp.appOptions`

## 5. 小程序踩坑记
#### 5.1. 组件
`input, map, canvas, video, live-player,camera , textarea` 是由客户端创建的原生组件，层级最高，z-index 没用
而其它组件都是基于Web Component规范实现的Custom Element，而诸如picker弹出选择器行为，navigator跳转行为，都是基于微信原生提供的能力，理解为调用wx.xxxApi

> 微信小程序的组件是否都是原生实现的，类似React Native？
No，小程序视图层仍然依赖于Webview，只有部分组件是原生组件，用来解决Mobile Web体验问题。目前原生组件包括：
input，textarea，video，map，canvas
>* tip: input 组件是一个 native 组件，字体是系统字体，所以无法设置 font-family；
>* tip: textarea 组件是由客户端创建的原生组件，它的层级是最高的。
>* tip: video 组件是由客户端创建的原生组件，它的层级是最高的。
>* tip: map 组件是由客户端创建的原生组件，它的层级是最高的。
>* tip: canvas 组件是由客户端创建的原生组件，它的层级是最高的。



![z-index](/img/in-post/post-mp-vue-holes/index.png)


#### 5.2. 页面层级
小程序页面跳转打开最多五层，超出五层不会跳转了

#### 5.3. 组件名
mpvue 组件名大写会提示，统一小写，警告信息如下：
![component-name](/img/in-post/post-mp-vue-holes/component-name.png)

#### 5.4. 图片路径
* **相对路径图片不显示**
`<img src="../../images/logo.png">`
  - **解决方案：**

    - 把路径 `import` 进来，或把图片放在 static 目录下

- `background-image`

  背景图在真机无法显示
  - 解决方案
    - 外链
    - base64 编码
      ```css
      background-image: url('转换后的编码')

      <!-- 如果多次引用可将其设为全局变量，在js文件引用 -->
      ```
      
    - 使用 image 组件，去掉背景图（可以使用相对路径）

#### 5.5. wx.request post 方法失败

* `wx.request` post 方法参数传输失败

  `wx.request` post 的 `content-type` 默认为 `application/json`
  如果服务器没有用到 json 解析，可以更改 `content-type` 为 `urlencoded`
  ```js
  wx.request({
    ...
    method: 'post',
    header: {
      'content-type': 'application/x-www-form-urlencoded'
    },
    ...
  })
  ```

#### 5.6. 录音管理相关
##### 5.6.1 onPause
> 录音暂停事件

监听情况：
* pause 事件--手动

不能监听：
* 自然播放结束
* stop 事件--手动

#### 5.6.2. 小程序实现语音流式识别
见博文-目前未更新： [mp - Voice stream processing](https://chaoranwill.github.io/2018/07/06/mp-Audio-stream-processing/)

#### 5.7. 开发工具相关
##### 5.7.1. 调试与非调试模式

假如工具内开启不校验域名选项
此时，调试模式下，可以不校验域名问题；http或者不合规范的请求地址将被允许，比如带有端口的地址（正常情况下url是不允许带端口的）

![uncheck](/img/in-post/post-mp-vue-holes/uncheck.jpg)

主要用途：
* 使用本地服务
* 使用未配置的域名
* 使用非 https 域名
* 在域名不合规范时，使用必须appid才可以使用的部分调试

##### 5.7.1. 真机预览问题
* 调试模式下可用，而非调试模式下不可用的情况：
  - 检查下是否没有配置好合法域名
  - 假如配置好了域名，**排查https**问题

* `request fail` 问题排查
  - 后台域名没有配置配置完毕请点击刷新按钮
  - 重启开发者工具，检查配置信息是否更新
  - 域名没有备案或或是备案后不足24小时；备案未生效
    ![域名](/img/in-post/post-mp-vue-holes/yuming.png)

  - ssl 协议有问题
    ![ssl](/img/in-post/post-mp-vue-holes/ssl.png)

* 同时测试ios和安卓，假如有一方可以，一方不行，则是证书问题，请选用受认可的证书

其他可参考：[https 解决方案](http://www.wxapp-union.com/forum.php?mod=viewthread&tid=648&highlight=https)

#### 5.8. 视频相关
--待续















