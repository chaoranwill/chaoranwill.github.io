---
layout:     post
title:      "mp - Voice stream processing"
subtitle:   "Voice stream reception and processing"
date:       2018-07-06 22:00:00
author:     "Chaoran"
header-img: "img/post-bg-php-basic.jpg"
noToc:      true
tags:
    - 前端开发
    - 小程序
---

> “To be a better girl ”

* 目录
{:toc #toc}
## 小程序语音流
**小程序录音处理 api**

使用 `wx.getRecorderManager()` ，获取全剧唯一的录音管理器`recorderManager`，可以对录音设备做操作
[wx.getRecorderManager()](https://developers.weixin.qq.com/miniprogram/dev/api/getRecorderManager.html)

**语音流**
![frame](/img/in-post/post-mp-audio/frame.jpg)

**录音配置**
![frame](/img/in-post/post-mp-audio/frame-set.jpg)

* duration

    录音时长，在本次需求中，产品要求是录音不超过30s

* frameSize

    实现流式识别的关键配置，指定帧大小，使得录音到指定的帧大小时，调用onFrameRecorded函数。

* onFrameRecorded函数

    利用这个回调函数，微信小程序可以使用帧大小间隔，发送请求，实现流式识别
    - 返回格式 —— ArrayBuffer

*小程序不支持Blob，发送请求无法兼带ArrayBuffer与其他类型的字段，需要将语音片段转换成base64*

* [wx.arrayBufferToBase64(arrayBuffer)](https://developers.weixin.qq.com/miniprogram/dev/api/api-util.html)
* [wx.base64ToArrayBuffer(base64)](https://developers.weixin.qq.com/miniprogram/dev/api/api-util.html)
![base64](/img/in-post/post-mp-audio/base64.png)

