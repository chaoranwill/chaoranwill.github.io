---
layout:     post
title:      "HTMLCollection & NodeList "
subtitle:   "thought from interview"
date:       2018-03-15 19:55:00
author:     "Chaoran"
header-img: "img/post-bg-fe-topics.jpeg"
noToc:      true
tags:
    - 前端开发
---

> “To be is to be perceived. ”

* 目录
{:toc #toc}

## 前言
* 相同：
    HTMLCollection与NodeList都是DOM节点的集合，两者都属于Collections范畴
* 区别：
    - HTMLCollection比NodeList多了一个namedItem方法，其他方法保持一致
    - 包含节点类型不同：NodeList可以包含任何节点类型，HTMLCollection只包含元素节点（ElementNode）

![collections](/img/in-post/post-html-nodes/collections.png)


## 1. HTMLCollection
> 接口表示一个包含了元素（元素顺序为文档流中的顺序）的通用集合（generic collection），还提供了用来从该集合中选择元素的方法和属性。
HTML DOM 中的 HTMLCollection 是即时更新的（live）；当其所包含的文档结构发生改变时，它会自动更新

* 属性
    - HTMLCollection.length 只读
    返回集合当中子元素的数目
* 方法
    - `HTMLCollection.item()`
根据给定的索引（从0开始），返回具体的节点。如果索引超出了范围，则返回 null。
    - `HTMLCollection.namedItem()`
    根据 Id 返回指定节点，或者作为备用，根据字符串所表示的 name 属性来匹配。根据 name 匹配只能作为最后的依赖，并且只有当被引用的元素支持 name 属性时才能被匹配。如果不存在符合给定 name 的节点，则返回 null。

## 2. NodeList
> NodeList 对象是一个节点的集合，是由 `Node.childNodes` 和 `document.querySelectorAll` 返回的.

* 属性
    - length
        NodeList 对象中包含的节点个数.
* 方法
    - items( idx )
        返回NodeList对象中指定索引的节点,如果索引越界,则返回null.等价的写法是nodeList[idx], 不过这种情况下越界访问将返回undefined

* 有时实时
    - Node.childNodes 是实时的
    - document.querySelectorAll 返回一个静态的 NodeList

**将 NodeList 转换为 Array**
```js
var div_list = document.querySelectorAll('div'); // 返回 NodeList
var div_array = Array.prototype.slice.call(div_list); // 将 NodeList 转换为数组

//ES6 - Array.from();
var div_array_from = Array.from(div_list); //将 NodeList 转换为数组
```

参考：
[HTMLCollection vs. NodeList](https://www.jianshu.com/p/f6ff5ebe45fd)