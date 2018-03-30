---
layout:     post
title:      "About Array and String"
subtitle:   "learn from blogs"
date:       2018-03-19 19:55:00
author:     "Chaoran"
header-img: "img/post-bg-array.jpg"
noToc:      true
tags:
    - 前端开发
    - js
---

> “To be is to be perceived. ”

* 目录
{:toc #toc}

## 1. 数组方法
#### 1.1. 改变原数组的
* shift：将第一个元素删除并且返回删除元素，空即为undefined
* unshift：向数组开头添加元素，并返回新的长度
* pop：删除最后一个并返回删除的元素
* push：向数组末尾添加元素，并返回新的长度
* reverse：颠倒数组顺序
* sort：对数组排序
* splice:splice(start,length,item)删，增，替换数组元素，返回被删除数组，无删除则不返回

#### 1.2. 不改变原数组的：
* concat：连接多个数组，返回新的数组
* join：将数组中所有元素以参数作为分隔符放入一个字符
* slice：slice(start,end)，返回选定元素
* map,filter,forEach,some,every等不改变原数组

## 2. 必知的数组方法
* `Array.forEach()`
    能够方便的遍历数组里的每个元素，可以在回调函数里对每个元素进行操作
    该方法**没有返回值**，不需要在回调函数里写return，这是无意义的
    ```js
    //forEach
    var animals = ['dog', 'cat', 'mouse'];
    animals.forEach(function(item){
        console.log(item);
    });
    ```

* `Array.map()`
    > 如果你想修改数组里的每个元素，然后将修改后的数组存入新的数组，那使用 .map() 方法最方便。

    .map() 方法能够遍历整个数组，然后 返回一个新数组，这个新数组里的元素是经过了指定的回调函数处理过的
    ```js
    //map
    var numbers = [2, 4, 6, 8];
    var doubleNums = numbers.map(function(element) {
        return element * 2;
    });

    console.log('doubleNums: ', doubleNums)  //[4, 8, 12, 16]
    ```

* `Array.filter()`
    .filter() 方法能够过滤掉数组中的某些元素，可以在回调函数里设定条件，不符合条件的元素都会排除在外
    ```js
    var scores = [3, 12, 5, 23, 19, 7];

    var topScores = scores.filter(function(item){
        if (item > 10){
            return true;
        } else {
            return false;
        }
    });

    console.log('topScores: ', topScores);   // [12, 23, 19]
    ```

* `Array.indexOf()`
    indexOf() 能够告诉你 某个元素在数组中的位置，它返回的是索引值，如果数组里有重复的元素，它会返回第一个元素的位置
    ```js
    var a = [2, 9, 9, 18];

    var i = a.indexOf(9);

    console.log('i: ', i);

    /*
    if (a.indexOf(7) === -1) {
    // 数组中没有这个元素
    }*/
    ```

* `Array.every()`
    > 如果你想知道数组中的所有元素都是否符合某种条件，使用 .every() 最方便

    .every() 方法的作用是用指定的回调函数去检查数组中的每个元素，如果对于每个元素，这个回调函数都返回true，则.every()返回true。否则，.every() 返回false

    ```js
    var ages = [23, 19, 32, 44];

    var olderThan18 = ages.every(function(element) {
        return element > 18;
    });

    console.log('olderThan18: ', olderThan18);   // olderThan18:  true
    ```

参考：
* [每个JavaScript程序员都需要知道的5个数组方法](http://www.webhek.com/post/5-array-methods-all-javascript-beginners-should-know.html)
* [是否改变原数组的常用方法归纳](http://blog.csdn.net/cristina_song/article/details/77917404)

## 字符串
> 属性 length

#### 实例方法
##### ---对象通用方法
> String类型是与字符串对应的包装类型，继承了Object对象的通用方法
作用：
返回string 的原始字符串值

* toString()
* toLocaleString()
* valueOf()

##### ---访问字符
* chartAt()

    charAt()方法涉及到Number()函数的隐式类型转换，如果转换为数值，则按照上述规则输出字符串；如果转换为NaN，则输出第0个字符
* 中括号[]

    参数超出范围或是NaN时，则输出undefined；没有参数时，会报错；该方法没有Number()转型函数的隐式类型转换，但参数为单数值数组时可转换为数值
    ```js
    var str = "hello";
    console.log(str[0]);//h
    console.log(str[[1]]);//e
    console.log(str[false]);//undefined
    ```

* charCodeAt()

    类似 charAt
    指定位置的字符16位Unicode编码。返回值是一个16位的整数
    ```js
    var str = "hello";
    console.log(str.charCodeAt());//104
    console.log(str.charCodeAt(0));//104
    ```

* fromCharCode()

    接收一个或多个字符编码，然后把它们转换成一个字符串
    ```js
    console.log(String.fromCharCode(104,101,108,108,111));//'hello'
    console.log(String.fromCharCode(0x6211,0x662f,0x5c0f,0x706b,0x67f4));//'我是小火柴'
    ```

##### ---查找
> 同访问字符方法charAt()和中括号[]方法有相反的地方
一个通过字符串查找位置
一个则是通过位置查找字符

* indexOf()

    `indexOf(searchString,start)`
    - 返回searchString首次出现的位置，如果没有找到则返回-1
    - 隐式调用String()转型函数，将searchString非字符串值转换为字符串

* lastIndexOf()

    `lastIndexOf(searchString,start)`
    - 返回searchString第一次出现的位置，如果没有找到则返回-1
    - 从右向左查找

##### ---字符串拼接
* concat()

    - 将一个或多个字符串拼接起来，返回拼接得到的新字符串，而原字符串不发生改变。
    - 若参数(第一个参数除外)不是字符串，则通过String()方法隐式转换为字符串，再进行字符串拼接
        ```js
        var stringValue = 'hello ';
        var result = stringValue.concat('world','!');
        console.log(result);//'hello world!'
        console.log(stringValue);//'hello'
        ```
        **第一个参数只能是字符串，如果是其他类型(数组除外)则报错**

        参数会按照首先出现的参数是数组还是字符串来决定如何转换
* 加号+

    当操作数其中一个是字符串，或者对象转换为字符串时，才进行字符串拼接

##### ---创建子字符串
* slice()

    `slice(start,end)`
    返回子串
    为负数时从后往前数
* substring()

    `substring(start,end)`
    - 如果任一参数是NaN或负数，则被0取代
    - 如果任一参数大于字符串长度，则被字符串长度取代
    - 如果start 大于 end，则交换它们的值
* substr()

    `substr(start,length)`
    - start和end无法交换位置
    - [注意]该方法不是ECMAScript标准，已经被弃用

##### ---大小写转换
* toLowerCase()
* toLocaleLowerCase()

    (针对地区)
* toUpperCase()
* toLocaleUpperCase()

    (针对地区)

**[注意]在不知道自己的代码将在哪个语言环境中运行的情况下，使用针对地区的方法更稳妥**

这4种方法均不支持String()隐式类型转换，只支持字符串类型
```js
(true).toLowerCase();//报错
(2).toLocaleLowerCase();//报错
({}).toUpperCase();//报错
([]).toLocaleUpperCase();//报错
```

##### ---匹配方法
* match()

    - 只接受一个为正则或字符串的参数，并以数组的形式返回匹配的内容
    - 若不设置全局标志，match()方法和exec()方法结果相同
    - 若不设置全局标志，具有index和input属性

    ```js
    var str = 'ere333',
        reg = /e/,
        regg = /e/g

    reg.exec(str)  //['e']
    str.match(reg) //['e']
    str.match(regg) //['e','e']

    str.match(reg).index // 0
    str.match(reg).input //'ere333'
    ```

* search()

    - 返回匹配的内容在字符串中首次出现的位置
        
        类似于不能设置起始位置的indexOf，找不到返回-1
    - search()方法不执行全局匹配，忽略全局标志g
    - 也会忽略RegExp对象的lastIndex属性，总是从字符串的开始位置开始搜索

* replace()

    - 替换一个或多个子字符串
    - 接收两个参数：第一个是正则表达式或字符串，表示待查找的内容；第二个是字符串或函数，表示替换内容
    - 返回替换后的字符串
    - 短属性名         说明
        - $&              最近一次的匹配项
        - $`              匹配项之前的文本
        - $'              匹配项之后的文本
        - $1,$2...        表示第N个匹配捕获组

        ```js
        var string = 'cat-bat-sat-fat';
        console.log(string.replace(/(.)(at)/g,'$&'));//'cat-bat-sat-fat'
        console.log(string.replace(/(.)(at)/g,'$`'));//'-cat--cat-bat--cat-bat-sat-'
        console.log(string.replace(/(.)(at)/g,"$'"));//'-bat-sat-fat--sat-fat--fat-'
        console.log(string.replace(/(.)(at)/g,'$1'));//'c-b-s-f'
        console.log(string.replace(/(.)(at)/g,'$2'));//'at-at-at-at'
        ```
   
    - replace()方法的第二个参数可以是函数

        如果在只有一个匹配项的情况下，该方法会向这个函数传递3个参数：模式的匹配项、模式匹配项在字符串中的位置、原始字符串
        ```js
        // 首字母大写
        var text = 'one two three';
        var result = text.replace(/\b(\w+)\b/g,function(match,m1,pos,originalText){
            return m1.charAt(0).toUpperCase()+m1.substring(1); 
        })
        console.log(result);
        ```
        ```js
        // HTML 转义
        function htmlEscape(text){
            return text.replace(/[<>"&]/g,function(match,pos,originalText){
                switch(match){
                    case '<':
                    return '&lt;';
                    case '>':
                    return '&gt;';
                    case '&':
                    return '&amp;';
                    case '\"':
                    return '&quot;';
                }
            });
        }
        console.log(htmlEscape('<p class=\"greeting\">Hello world!</p>'));
        //&lt;p class=&quot; greeting&quot;&gt;Hello world!&lt;/p&gt;
        console.log(htmlEscape('<p class="greeting">Hello world!</p>'));
        //同上
        ```
        ```js
        // 找出重复项最多的字符和个数
        var str = 'aaaaabbbbbdddddaaaaaaaffffffffffffffffffgggggcccccce';
        var pattern = /(\w)\1+/g;
        var maxLength = 0;
        var maxValue = '';
        var result = str.replace(pattern,function(match,match1,pos,originalText){
            if(match.length > maxLength){
                maxLength = match.length;
                maxValue = match1;
            }
        })
        console.log(maxLength,maxValue);//18 "f"
        ```

* split()

    - 基于指定的分隔符将一个字符串分割成多个字符串，并将结果放在一个数组中，分隔符可以是字符串，也可以是一个RegExp
    - 可以接受第二个参数(可选)用于指定数组的大小
    
        如果第二个参数为0-array.length范围内的值时按照指定参数输出，其他情况将所有结果都输出

##### ---去除首尾空格
* trim()

    创建一个字符串的副本，删除前置及后缀的所有空白字符，然后返回结果
    ```js
    // 判断输入字符是否为空
    if(usename.trim().length){
        alert('correct');
    }else{
        alert('error');
    }
    ```

##### ---字符串比较
* localeCompare()

    - 如果字符串在字母表中应该排在字符串参数之前，则返回一个负数(大多数情况下为-1)
    - 如果字符串等于字符串参数，则返回0
    - 如果字符串在字母表中应该排在字符串参数之后，则返回一个正数(大多数情况下为1)

## 正则
#### 书写方式
* 构造器

    `var regex = /\w+/`
* 字面量

    ```js
    var regex = new RegExp('\\w+')

    // '\' 需要转义 ---> \\
    ```
