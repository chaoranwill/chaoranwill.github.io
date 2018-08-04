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

最近在做语音识别的小程序，关于语音传输，目前有两种解决方案
* 录音后上传整个文件
* 分片上传——边录音边上传

关于录音管理，要从 [recorderManager](https://developers.weixin.qq.com/miniprogram/dev/api/getRecorderManager.html) 说起
![recorderManager](/img/in-post/post-mp-audio/recorderManager.png)

#### 1. 整个文件上传
默认录音是不分片的，需要监听录音的结束事件，获取录音结果存储的默认路径，调用 upload 函数上传

```js
// 新建 recorderManager 对象
this.recorderManager = wx.getRecorderManager();

// 监听 recorderManager 对象的录音结束事件
this.recorderManager.onStop((res) => {
    this.myRecordsrc = res.tempFilePath;
    this.recordAudio.src = res.tempFilePath;

    // tempFilePath 为录音文件的默认存储路径
    wx.uploadFile({
        url: url,
        filePath: res.tempFilePath,
        name: name,
        // header: {}, // 设置请求的 header
        // formData: {}, // HTTP 请求中其他额外的 form data
        success: function(res) {
            // success
            resolve(res)
        },
        fail: function() {
            // fail
        },
        complete: function() {
            // complete
        }
    })
})
```

#### 2. 小程序语音流获取
**小程序录音处理 api**

依旧是使用 `wx.getRecorderManager()` ，获取全剧唯一的录音管理器`recorderManager`，可以对录音设备做操作
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

#### 3. base64 转码
*小程序不支持Blob，发送请求无法兼带ArrayBuffer与其他类型的字段，需要将语音片段转换成base64*

* [wx.arrayBufferToBase64(arrayBuffer)](https://developers.weixin.qq.com/miniprogram/dev/api/api-util.html)
* [wx.base64ToArrayBuffer(base64)](https://developers.weixin.qq.com/miniprogram/dev/api/api-util.html)

![base64](/img/in-post/post-mp-audio/base64.png)

#### 4. onFrameRecorded 最后一帧监听
* onFrameRecorded

    取到指定的帧大小后就会被调用
* duration

    如果设置 30s
![duration](/img/in-post/post-mp-audio/duration.jpg)

**问题**

到达30秒自动结束的时候并不会触发onFrameRecorded，就会造成最后一个onFrame丢失

**解决**

将duration设为31s，并在开始录音时，引入一个30秒的倒计时，到30s时手动触发stop()方法，因为手动触发stop()方法，onFrameRecorded是会自动被调用的

#### 5. 最后一帧
> 请求顺序问题

**需求**

判断当前响应是否为最后一个到达，响应包中的is_end字段

**问题**

由于手动停止了录音，最后一个语音包小于等于其他语音包，有可能我们收到最后一个请求的响应包时，上一个请求还在发送的路上或者解析中，这时候isend字段无法准确判断

**解决**

通过对比请求量与返回值的量 `reqNum == respNum && is_end == 1`


