---
english_title: udp-test
title: 测试UDP转发
date: 2018-04-20 12:34:56
---

测试 Android 的代理是否转发了 UDP

<!-- more -->

- Android 客户端，采用 UDP 将字符串发送到服务地址，等待回复
- Server端，监听 UDP，获取字符串，把字符串原样发回去，并加上客户端的地址

代码地址：

[Android client](https://gitee.com/oddcn/udp-test-android-client)

[Go server](https://gitee.com/oddcn/udp-test-go-server)