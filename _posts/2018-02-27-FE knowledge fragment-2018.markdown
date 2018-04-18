---
layout:     post
title:      "FE knowledge fragment"
subtitle:   " "
date:       2018-02-27 19:55:00
author:     "Chaoran"
header-img: "img/post-bg-web-basic.png"
noToc:      true
tags:
    - 前端开发
---

> “To be is to be perceived. ”

* 目录
{:toc #toc}

![mvvm](/img/in-post/post-web-fragment/summary.jpg)

## 1. ES6
最重要特征
* 箭头函数
* promises
* 异步函数 (Async Functions)
* 解构
* 默认和剩余参数（Default and Rest Parameters）

其他
* 字符串模板
* generators(生成器)
* async/await
* 解构赋值
* class
* 引入module模块的概念

#### 1.1. 箭头函数：
> 箭头函数可以让this指向固定化，这种特性很有利于封装回调函数

* 函数内的this对象，是定义时所在的对象，不是使用时所在的对象
* 不可当构造函数
* 用rest代替argument
* this指向一般可变，但在箭头函数中固定，取决于定义时的环境
* 简单，单行，不会复用的函数建议使箭头函数 
    复杂，行多，使用传统


#### 1.2. promise
> 解决异步回调多层嵌套的问题，使异步任务的处理方式变成线性

* 是一个容器；
    包含某个未来结束的事件
* 是一个对象：
    从它可获取异步操作的消息

1. pending 进行中
2. resolved 已完成
3. rejected 已失败

**特点**
* 状态不受外界影响，只有事件结果决定
* 状态改变不会再变

**缺点：**
* 无法取消promise，一旦建立立即执行，中途无法撤回
* 无回掉函数的话，错误不反应到外部
* pending时，状态无法得知

**Promise.all**
> 接收 Promise 数组为参数，将多个Promise实例，包装成一个新的Promise实例，所有 resolve ，返回所有值

在不同的接口请求数据然后拼合成自己所需的数据，通常这些接口之间没有关联（例如不需要前一个接口的数据作为后一个接口的参数）
```js
var p = Promise.all([p1, p2, p3]);
```

p的状态由p1、p2、p3决定，分成两种情况:
* 只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
* 只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

**Promise.race**
它同样接收一个数组，不同的是只要该数组中的 Promise 对象的状态发生变化（无论是 resolve 还是 reject）该方法都会返回

**async/await**
> async 会将其后的函数（函数表达式或 Lambda）的返回值封装成一个 Promise 对象，而 await 会等待这个 Promise 完成，并将其 resolve 的结果返回出来

**async/await 的优势在于处理 then 链，解决 promise 的返回值和参数传递**

* async 用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成
* 如果在函数中 return 一个直接量，async 会把这个直接量通过 Promise.resolve() 封装成 Promise 对象

* 如果它等到的不是一个 Promise 对象，那 await 表达式的运算结果就是它等到的东西。

* 如果它等到的是一个 Promise 对象，await 就忙起来了，它会**阻塞**后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果
    async 函数调用不会造成阻塞，它内部所有的阻塞都被封装在一个 Promise 对象中异步执行


**await 作用**
* 是写异步代码的新方式，以前的方法有回调函数和Promise。
* 是基于Promise实现的，它不能用于普通的回调函数。
* 与Promise一样，是非阻塞的。
* 使得异步代码看起来像同步代码，这正是它的魔力所在。

更多了解：[理解 JavaScript 的 async/await](https://segmentfault.com/a/1190000007535316)

#### 1.3. 解构
> 快速解压缩对象属性和数组中的值，并将它们分配给各个变量

```js
//解构数组
var soccerteam = ['George', 'Dennis', 'Sandy']
var [a, b] = soccerteam // destructure soccerteam array
console.log(a) // "George"
console.log(b) // "Dennis"
```

#### 1.4. 默认&剩余参数&扩展运算符
**默认参数**
```js
//我们都使用过一下模式来创建具有默认值的参数：
function getarea(w,h){
  var w = w || 10
  var h = h || 15
  return w * h
}

//有了ES6对默认参数的支持，显式定义的参数值的日子已经结束：
function getarea(w=10, h=15){
  return w * h
}
getarea(5) // returns 75
```

**剩余参数**

```js
//将函数参数转换成数组
function addit(...theNumbers){
  // get the sum of the array elements
  //reduce 将结果序列和下一个参数做累计计算
  // ...将参数转化为数组
  //console.log(...theNumbers)   [1,2,3,4]
    return theNumbers.reduce((prevnum, curnum) => prevnum + curnum, 0) 
}

addit(1,2,3,4) // returns 10
```

**扩展运算符**
* 在数组中的使用
    * 简化数组 push 方法
    * 合并数组
    * 替代 apply 方法
    * 将字符转为数组
* 在对象中的使用
    * 将目标对象中所有可遍历属性取出，并拷贝到当前对象中

```js
console.log(...[1,2,3,4])   // 1,2,3,4 ---> console.log(1,2,3,4)

let a = [],
    b = [1,2,3,4]
a.push(...b)          // 可将整个数组 push

// apply:  Array.prototype.push.apply(a, b)
// 为什么用push ： vue 中对数组元素的改变只监听 push 方法，concat 只改变了数据模型，视图不会变化

// 合并数组
let arr1 = [1],
    arr2 = [2,3]
let arr = [...arr1, ...arr2]

// 将字符串转为数组
[...'hello world']

// 将目标对象中所有可遍历属性取出，并拷贝到当前对象
let obj1 = {key1:'value1', key2: 'value2'}
let obj2 = {
    key3: 'value3',
    ...obj1
}
console.log(obj2)
// { key3: 'value3', key1:'value1', key2: 'value2'}
// Object.assign({key3: 'value3'}, obj1)

// 合并两个对象
let total = {...a, ...b}
```

#### 1.5. interator 
> 是一种接口，为所有数据结构提供一种统一的访问机制，即for...of 循环 

**作用：**
* 一是为各种数据结构，提供一个统一的、简便的访问接口；
* 二是使得数据结构的成员能够按某种次序排列；
* 三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。

**interator遍历过程：**
1. 创建一个只针对象，指向当前数据结构的起始位置（遍历器对象本质是指针对象）
2. 调用指针对象的next方法

**使用场合：**
* 解构赋值
* 扩展运算符（...）
* yield*

**for...in**
* 为遍历对象设计，不适用数组
* key
* 以字符串作为键名
* 遍历所有的可枚举属性，包括原型
* 可能会以任意顺序遍历键名
* 循环除了遍历数组元素以外,还会遍历自定义属性

**for...of**
* 语法简洁，无以上缺点,for of遍历的只是数组内的元素，而不包括数组的原型属性
* 循环value
* 不同用于foreach方法，可以与break，continue，return配合使用
* 提供了遍历所有数据结构的统一操作接口，循环普通对象结合 `Object.keys()` 搭配使用
* 可自动遍历generator函数生成的iterator对象

#### 1.6. generator 函数
> 一种异步解决方案（一种封装了多个内部状态的状态机）

* 返回的不是函数运行结果，而是指向内部状态的指针对象
* 调用next方法，从停止地方开始执行，移向下一个状态

#### 1.7. yield 与 return
相似：都能返回紧跟在语句后面那个表达式的值
区别：记忆功能，执行次数，返回值数量

#### 1.8. 回调函数
JavaScript对异步编程的实现

#### 1.9. ES6 Object.assign
> 将源对象（source）的所有可枚举属性，复制到目标对象（target）

`Object.assign(target, source1, source2);`
后面属性覆盖前面同名属性
* 一个参数时，返回该参数
* 参数不是对象，转成对象（undefined，null会报错），若为源对象位置，则跳过
* 可用来操作数组，将数组视为对象
* 浅拷贝非深拷贝（若源对象的有对象属性值，则拷贝的是该引用）

**用途：**
* 为兑现添加属性/方法
* 克隆对象
* 合并对象
* 为属性指定默认值

## 2. 通信
#### 2.1. JSONP 
被包含在一个回调函数中的 json

**核心：** 动态添加script标签调用服务器提供的js脚本
#### 2.2. cors
使用自定义的http头部让浏览器与服务器进行沟通，确定该请求是否成功

**核心：** 由服务器发送一个响应标头

详细：[JSONP && CORS](http://www.cnblogs.com/chaoran/p/6579588.html)

#### 2.3. web安全
* 将重要的cookie标记为http only
* 只允许用户输入期望值
* encode
* 过滤或移除特殊标签
* 过滤JavaScript事件标签

更多：[web 攻击](http://www.cnblogs.com/chaoran/p/6581024.html)

## 3. 架构
#### 3.1. 模块化
* **原理：** 将复杂系统分解为代码结构更合理，可维护性更高，可管理的模块
* **目的：** 只需完成自己的业务代码
* **发展过程：**
    1. commonjs
        模块为单独的文件，require，同步使用
    nodejs主要用于服务器进程，加载内容在本地磁盘
    异步情况：浏览器环境中需要从服务器加载模块，需要采用异步模式
    2. AMD（Asynchronous Module Definition）
        * 允许输出模块兼容commonjs规范
        * require([module], callback);
        * 模块加载与调用不同步，浏览器不会发生假死
        * requirejs   curljs
    3. CMD
        seajs推广中对模块定义的产出

**CMD与AMD区别：**
* amd推崇依赖前置（定义模块时申明其依赖的模块），cmd推崇依赖就近（用时再require）
* amd的api默认一当多，cmd推崇职责单一（amd中require分全局和局部）

**requirejs 与 seajs 分析：**
1. 定位，requirejs想成为浏览器端的模块加载器，也想成为rhino/node等环境的模块加载器
seajs专注web浏览器端，通过node扩展方式方便跑在node端
2. 标准，requirejs醉醺amd规范，seajs遵循cmd，api不同
3. 理念，requirejs尝试让第三方类库修改自身来支持requirejs，seajs不强推，采用资助封装方式，已较成熟封装策略
4. 质量，require<seajs
5. 插件

更多了解：[AMD && CMD](http://www.cnblogs.com/chaoran/p/6696690.html?_blank)

#### 3.2. react
> 用于构建用户界面的JavaScript库，主要用于构建ui，将普通的DOM以数据结构的形式展现出来

永远只需要关心数据整体，两次数据之间的UI如何变化，则完全交给框架去做，使用React大大降低了逻辑复杂性
Virtual DOM并没有完全实现DOM，Virtual DOM最主要的还是保留了Element之间的层次关系和一些基本属性

基于React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新

虚拟DOM是内存数据，性能是极高的，而对实际DOM进行操作的仅仅是Diff部分，因而能达到提高性能的目的。这样，不再需要关注某个数据的变化如何更新到一个或多个具体的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的

**设计特点：**
* 变换：react核心认为ui只是把数据通过映射关系变换成另一种形式的数据——函数
* 组合：将两个或多个不同的抽象合并为一个
* 组件化：推荐以组件的方式思考ui构成，将小组件通过组合或嵌套构成大组件

**组件特征：**
* 可组合
* 可重用
* 可维护

**jsx语法：**
HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写

**生命周期：**
组件的生命周期分成三个状态：
* Mounting：已插入真实 DOM
* Updating：正在被重新渲染
* Unmounting：已移出真实 DOM

React 为每个状态都提供了两种处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数:
* componentWillMount()
* componentDidMount()
* componentWillUpdate(object nextProps, object nextState)
* componentDidUpdate(object prevProps, object prevState)
* componentWillUnmount()

两种特殊状态的处理函数：
* componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
* shouldComponentUpdate(object nextProps, object nextState)：判断是否重新渲染时调用

#### 3.3. angular
**特性：**
* MVVM
* 模块化
* 自动化双向数据绑定
* 语义化标签
* 依赖注入

#### 3.4. vue
* 父-->子
    - props
    - 父组件中通过 $refs.组件名 来获得子组件，也就可以调用子组件的属性和方法
    
* 子-->父
    - on/emit  
    - 子组件通过 $parent 获得父组件，通过 $root 获得最上层的组件
* 其他
    使用空的vue实例作为中央事件总线

**生命周期**

总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。
![vue](/img/in-post/post-web-fragment/vue.png)


* beforecreate : 可以在这加个loading事件，在加载实例时触发 
* created : 初始化完成时的事件写在这里，如在这结束loading事件，异步请求也适宜在这里调用 
* mounted : 挂载元素，获取到DOM节点 
* updated : 如果对数据统一处理，在这里写上相应函数 
* beforeDestroy : 可以做一个确认停止事件的确认框 
* nextTick : 更新数据后立即操作dom 

**axios**
* Axios 是一个基于 promise 的 HTTP 库，支持promise所有的API
* 它可以拦截请求和响应
* 它可以转换请求数据和响应数据，并对响应回来的内容自动转换成 JSON类型的数据
* 安全性更高，客户端支持防御 XSRF

**Vuex**
> 大型单页应用（SPA），会出现多个视图组件依赖同一个状态，来自不同视图的行为需要变更同一个状态

> 一个应用可以看作是由上面三部分组成: View, Actions,State,数据的流动也是从 View => Actions => State =>View 以此达到数据的单向流动. 但是项目较大的, 组件嵌套过多的时候, 多组件共享同一个State会在数据传递时出现很多问题.

Vuex可以被看作项目中所有组件的数据中心,我们将所有组件中共享的State抽离出来,任何组件都可以访问和操作我们的数据中心.
![vuex](/img/in-post/post-web-fragment/vuex.png)
一个实例化的Vuex.Store由state, mutations和actions三个属性组成:

* state中保存着共有数据
* 改变state中的数据有且只有通过mutations中的方法,且mutations中的方法必须是同步的
* 如果要写异步的方法,需要些在actions中, 并通过commit到mutations中进行state中数据的更改.


##### 3.4.1. 双向绑定
> 将对象属性变化绑定到UI
简单理解：在单向绑定的基础上给可输入元素（input、textare等）添加了change(input)事件，来动态修改model和 view

双向数据绑定底层的思想非常的基本，它可以被压缩成为三个步骤：
1. 需要一个方法来识别哪个UI元素被绑定了相应的属性 
2. 监视属性和UI元素的变化 
3. 将所有变化传播到绑定的对象和元素

实现方式：
* 发布者-订阅者模式（backbone.js）

    一般通过sub, pub的方式实现数据和视图的绑定监听，更新数据方式通常做法是 `vm.set('property', value)`
    这种方式现在毕竟太low了，我们更希望通过 `vm.property = value` 这种方式更新数据，同时自动更新视图，于是有了下面两种方式

* 脏值检查（angular.js） 

    数据发生变更后，对于所有的数据和视图的绑定关系进行一次检测，识别是否有数据发生了改变，有变化进行处理，可能进一步引发其他数据的改变，所以这个过程可能会循环几次，一直到不再有数据变化发生后，将变更的数据发送到视图，更新页面展现。如果是手动对 ViewModel 的数据进行变更，为确保变更同步到视图，需要手动触发一次“脏值检测”。

    angular.js 是通过脏值检测的方式比对数据是否有变更，来决定是否更新视图，最简单的方式就是通过 setInterval() 定时轮询检测数据变动，当然Google不会这么low，angular只有在指定的事件触发时进入脏值检测，大致如下：
    - DOM事件，譬如用户输入文本，点击按钮等。( `ng-click `)
    - XHR响应事件 (` $http `)
    - 浏览器Location变更事件 (` $location `)
    - Timer事件(`$timeout , $interval`)
    - 执行` $digest()` 或` $apply()`

* 数据劫持（vue.js）

    vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过 `Object.defineProperty()` 来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
    
    监控对数据的操作，从而可以自动触发数据同步。并且，由于是在不同的数据上触发同步，可以精确的将变更发送给绑定的视图，而不是对所有的数据都执行一次检测
    - `Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象
        ```js
        //语法
        Object.defineProperty(obj, prop, descriptor)

        //例子
        Object.defineProperty(obj, "key", {
            enumerable: false,
            configurable: false,
            writable: false,
            value: "static"
        });

        var obj = {};
        Object.defineProperty(obj, 'hello', {
            get: function() {
                console.log('get val:'+ val);
                return val;
        　 },
        　　set: function(newVal) {
                val = newVal;
                console.log('set val:'+ val);
            }
        });
        obj.hello='chaoran';
        obj.hello;
        ```
        ![mvc](/img/in-post/post-web-fragment/define.png)
        
        更多：[了解 defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

**实现 MVVM 双向绑定**
* 实现一个数据监听器Observer

    能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者
* 实现一个指令解析器Compile

    对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数
* 实现一个Watcher

    作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图
* mvvm入口函数，整合以上三者
![mvvm](/img/in-post/post-web-fragment/mvvm-back.png)

* 第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter和getter
这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化
* 第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图
* 第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
    - 在自身实例化时往属性订阅器(dep)里面添加自己
    - 自身必须有一个update()方法
    - 待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。

* 第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者
    - Observer来监听自己的model数据变化
    - Compile来解析编译模板指令
    - Watcher搭起Observer和Compile之间的通信桥梁
    
    达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

参考：
* [剖析Vue原理&实现双向绑定MVVM](https://segmentfault.com/a/1190000006599500)
* [Vue 双向数据绑定原理分析](https://www.jianshu.com/p/d3a15a1f94a0)

#### 3.5. 框架对比
**angular 与 react**
* React 和 Angular 之间的巨大差异是 单向与双向绑定
* React 和 Vue 都使用了虚拟 DOM —— 不必在每个元素每次变化时重新渲染整个巨大的table
* 如果应用时常要处理大量的动态数据集，并以相对简便和高性能的方式对大型数据表进行显示和变更，由于双向数据绑定需要监听每一个可变元素, 数据量变大就会带来显著的性能问题，React是相当不错的选择。但是React不像AngularJS那样包含完整的功能，举例来说，React没有负责数据展现的控制器

**vue 与 angular**
* AngularJS 使用双向绑定，Vue 在不同组件间强制使用单向数据流。这使应用中的数据流更加清晰易懂
* vue 运行时性能更好
    - 在 AngularJS 中，当 watcher 越来越多时会变得越来越慢
    
        因为作用域内的每一次变化，所有 watcher 都要重新计算。并且，如果一些 watcher 触发另一个更新，脏检查循环 (digest cycle) 可能要运行多次

**vue 与 react**
* 使用 Virtual DOM
* 提供了响应式 (Reactive) 和组件化 (Composable) 的视图组件
* 将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库

不同
* react 社区庞大
* 开发模式：

    - React 在 view 层侵入性还是要比 Vue 大很多的,React 严格上只针对 MVC 的 view 层
    - Vue 则是 MVVM 模式的一种实现

* 数据绑定：

    - Vue有实现了双向数据绑定
    - React数据流动是单向的
* 数据渲染：

    对于大规模数据渲染，React要比Vue更快，渲染机制启动时候要做的工作比较多；
* 数据更新方面：

    - React 应用中，当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树

        - 需要在所有可能的地方使用 PureComponent，或是手动实现 shouldComponentUpdate 方法
        - 需要保证该组件的整个子树的渲染输出都是由该组件的 props 所决定的。如果不符合这个情况，那么此类优化就会导致难以察觉的渲染结果不一致

    - Vue 应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染
        - 可以理解为每一个组件都已经自动获得了 shouldComponentUpdate，并且没有上述的子树问题限制。
    - Vue 由于采用依赖追踪/数据劫持，默认就是优化状态：你动了多少数据，就触发多少更新，不多也不少。
        
        React在复杂的应用里有两个选择:
        - 手动添加 shouldComponentUpdate 来避免不需要的 vdom re-render。  
        - Components 尽可能都用 pureRenderMixin，然后采用 redux 结构 + Immutable.js；
* 开发风格的偏好：

    - React 推荐的做法是 JSX + inline style，也就是把 HTML 和 CSS 全都写进 JavaScript 了，即”all in js”
    - Vue 进阶之后推荐的是使用 webpack + vue-loader 的单文件组件格式，即 html, css, js 写在同一个文件
* 使用场景：

    - React 配合 Redux 架构适合超大规模多人协作的复杂项目;
    - Vue 则适合小快灵的项目。对于需要对 DOM 进行很多自定义操作的项目，Vue 的灵活性优于 React；




优化


#### 3.6. 软件架构
> 模式之间不同  主要是  M与V  的数据传递的流程不同

##### 3.6.1. mvc
![mvc](/img/in-post/post-web-fragment/mvc.png)
* View 传送指令到 Controller
* Controller 完成业务逻辑后，要求 Model 改变状态
* Model 将新的数据发送到 View，用户得到反馈

MVC 可以分成两种方式：
* 通过 View 接受指令，传递给 Controller
* 直接通过controller接受指令

##### 3.6.2. MVP
![mvp](/img/in-post/post-web-fragment/mvp.png)
* 各部分之间的通信，都是双向的。
* View 与 Model 不发生联系，都通过 Presenter 传递。
* View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

##### 3.6.3. MVVM
![mvvm](/img/in-post/post-web-fragment/mvvm.png)
* 用**双向数据绑定**的形式让数据更新的事件不需要开发人员手动去编写特殊用例，而是自动地双向同步。
* 数据绑定可以认为是Observer模式或者是Publish/Subscribe模式，原理都是为了用一种统一的集中的方式实现频繁需要被实现的数据更新问题。
* MVVM不仅简化了业务与界面的依赖关系，还优化了数据频繁更新的解决方案

#### 3.7. restful架构
> URI 定位资源，用HTTP动词（GET,POST,DELETE,DETC）描述操作

RESTful可以通过一套统一的接口为 Web，iOS和Android提供服务

Fielding将他对互联网软件的架构原则，定名为REST，即Representational State Transfer的缩写。我对这个词组的翻译是"资源的表现层状态转化"。
* 所谓"资源"，就是网络上的一个实体，或者说是网络上的一个具体信息。
* 我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）
* 如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。（HTTP）


**restful 架构**
* 每一个URI代表一种资源；

* 客户端和服务器之间，传递这种资源的某种表现层；

* 客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

## 4. js
#### 4.1. js垃圾回收与内存管理
> 各大浏览器通常用采用的垃圾回收有两种方法：标记清除、引用计数

##### 4.1.1. 垃圾回收
自动垃圾回收机制(GC:Garbage Collecation)，也就是说，执行环境会负责管理代码执行过程中使用的内存
垃圾收集器会定期（周期性）找出那些不在继续使用的变量，然后释放其内存
* 标记清除
    1. 垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记
    2. 然后，它会去掉环境中的变量以及被环境中的变量引用的标记
    3. 而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了
    4. 最后,垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间

* 引用计数

    跟踪记录每个值被引用的次数
    当声明了一个变量并将一个引用类型赋值给该变量时，则这个值的引用次数就是1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数就减1，释放那些引用次数为0的值所占的内存。

    ```js
    function problem() {
        var objA = new Object();
        var objB = new Object();

        objA.someOtherObject = objB;
        objB.anotherObject = objA;
    }
    ```

    这个方式存在一个比较大的问题就是循环引用
    可以手动切断他们的循环引用
    ```js
    myObj.element = null;
    element.someObject =null;
    ```

##### 4.1.2. 减少JavaScript中的垃圾回收
* 在初始化的时候新建对象，然后在后续过程中尽量多的重用这些创建好的对象。
* 另外还有以下三种内存分配表达式（可能不像new关键字那么明显了）：
    - {} （创建一个新对象）
    - [] （创建一个新数组）
    - function() {…} (创建一个新的方法，注意：新建方法也会导致垃圾收集！！)

##### 4.1.3. 优化
1. 对象object优化
    * 避免使用new/{}来新建对象
    * cr.wipe(obj)—遍历此对象的所有属性，并逐个删除，最终将对象清理为一个空对象  
2. 数组array优化
    ```js
    arr = [];     //将原数组变成一小片内存垃圾
    arr.length = 0    //清空数组
    ```

#### 4.2. 闭包
**特点：**
* 函数
* 能访问另外一个函数作用域中的变量

ES 6之前，Javascript只有函数作用域的概念，没有块级作用域。即外部是访问不到函数作用域中的变量。

**总结**
* 可以访问外部函数作用域中变量的函数
* 被内部函数访问的外部函数的变量可以保存在外部函数作用域内而不被回收---这是核心，后面我们遇到闭包都要想到，我们要重点关注被闭包引用的这个变量

#### 4.3. 作用域链
为什么闭包就能访问外部函数的变量呢

Javascript中有一个执行环境(execution context)的概念，它定义了变量或函数有权访问的其它数据，决定了他们各自的行为。每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中

当访问一个变量时，解释器会首先在当前作用域查找标示符，如果没有找到，就去父作用域找，直到找到该变量的标示符或者不再存在父作用域了，这就是作用域链。

作用域链的顶端是全局对象。对于全局环境中的代码，作用域链只包含一个元素：全局对象

**作用域链和原型继承：**
有点类似，但又有点小区别：
* 如果去查找一个普通对象的属性时，在当前对象和其原型中都找不到时，会返回undefined
* 查找的属性在作用域链中不存在的话就会抛出ReferenceError

更多了解：
* [闭包中的this作用域](https://www.cnblogs.com/nuanriqingfeng/p/5789003.html?_blank)

**闭包的运用**
* 匿名自执行函数

    有的函数只需要执行一次，其内部变量无需维护，执行后释放变量
* 实现封装/模块化代码

    变量作用域为函数内部，外部无法访问  
* 实现面向对象中的对象

    这样不同的对象(类的实例)拥有独立的成员及状态，互不干涉

**优点：**
* 可以让一个变量常驻内存 (如果用的多了就成了缺点
* 避免全局变量的污染
* 私有化变量

**缺点：**
* 因为闭包会携带包含它的函数的作用域，因此会比其他函数占用更多的内存
* 引起内存泄露

```js
// 采用函数引用方式的setTimeout调用
function callLater(paramA, paramB, paramC) {  
    /*使用函数表达式创建并放回一个匿名内部函数的引用*/  
    return (function () {  
        /* 
        这个内部函数将被setTimeout函数执行； 
        并且当它被执行时， 
        它能够访问并操作外部函数传递过来的参数 
        */  
        paramA[paramB] = paramC;  
    });  
}  

/* 
调用这个函数将在它的执行上下文中创建，并最终返回内部函数对象的引用 
传递过来的参数，内部函数在最终被执行时，将使用外部函数的参数 
返回的引用被赋予了一个变量 
*/  
var funcRef = callLater(elStyle, "display", "none");  
/*调用setTimeout函数，传递内部函数的引用作为第一个参数*/  
hideMenu = setTimeout(funcRef, 500);
```


#### 4.4. 事件委托和this
##### 4.4.1. 事件委托
由其它元素而非事件目标元素来响应事件产生的行为的思想。如用ul元素来处理其子元素li的事件。

**事件冒泡：** `stopPropagation、stopImmediatePropagation、preventDefault`

**订阅发布**
优点：减少监听器数量，改善性能
缺点：父容器的侦听器可能需要检查事件来选择正确的操作
##### 4.4.2. this
> this 关键字在JavaScript中的一种常用方法是指代码当前上下文

* 默认指向全局对象，其通常是window
* this总是代表它的直接调用者(js的this是执行上下文), 例如 obj.func ,那么func中的this就是obj
* 在严格模式下,没有直接调用者的函数中的this是 undefined
* 使用call,apply,bind绑定的,this指的是 绑定的对象

在异步编程中，this可以很容易改变过程中一个功能操作。保持处理程序上下文的一个小技巧是将其设置到闭包内的一个变量，当在上下文改变的地方调用一个函数时，如setTimeout，你仍然可以通过该变量引用需要的对象。

**箭头函数中的this**
* 箭头函数没有自己的this, 它的this是继承而来
* 默认指向在定义它时所处的对象(宿主对象),而不是执行时的对象, 定义它的时候,可能环境是window
* 箭头函数可以方便地让我们在 setTimeout ,setInterval中方便的使用this


