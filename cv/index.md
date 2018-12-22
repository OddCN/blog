---
title: 简历
date: 2017-06-27 10:58:02
---

---

# 教育背景

2016年9月 - 至今　　　　　中国石油大学（华东）　　地理信息系统　　硕士

2012年9月 - 2016年6月 　　中国石油大学（华东）　　地理信息系统　　本科

# 开源经历

### GoCloud

一个 Go 语言库，为开发者提供调用云服务的能力，这些云服务来自于不同的云服务提供商。不同的云服务提供商，对于相同或相似的云服务，在调用方式、命名等方面存在差异，GoCloud 旨在隐藏这些差异，降低开发者的学习和使用成本

`Google Summer of Code 2018, 协同开发`

https://github.com/cloudlibz/gocloud

### Go Builder Generator

一款 IntelliJ IDEA 插件，用于快速生成 golang 的 Builder 模式代码

`个人`

https://github.com/OddCN/go-builder-generator-idea-plugin

### 易屏

一款 Android 应用，将 Android 手机屏幕，通过 WiFi 或热点，实时分享到其它设备的浏览器上，无需为浏览器安装插件。具有跨平台、实时、无插件的特点

`个人`

https://github.com/OddCN/screen-share-to-browser

### AndServer

AndServer 是 Android 平台的开源 web server 框架。我发现并解决了该框架中的一个 bug，该 bug 会导致应用意外崩溃

`贡献代码`

https://github.com/yanzhenjie/AndServer/pull/33

# 项目经验

### 基础设施建设管理平台

2017年10月 - 2018年3月

`项目简介`：平台为建筑企业提供服务，服务包括施工车辆实时监控、资源配置优化、成本控制等

`主要技术`：API Gateway、OpenResty、RESTful API、Docker、WebSocket、基于TCP的自定义协议、JSON Web Token、MongoDB

`主要工作`：

- 使用 Go 实现定位器管理服务，利用 goroutine 解决了单机应对大量 GPS 定位器长连接的问题 
- 使用 Python 实现车辆管理服务，管理后端与客户端的长连接，推送车辆最新数据 
- 为降低分布式系统中身份验证的开销，采用 JWT 的方式实现微服务的身份验证 
- 实现 API 网关，配合 Lua 脚本，对请求进行验证和转发，并聚合后端 API，降低了前端调用 API 的频率、并简化了前端获取数 据的过程 
- 使用 Docker 部署各后端微服务，设计和开发 Android 客户端 

### 城市管理服务平台

2017年5月 - 2017年9月

`项目简介`：平台面向政府和公众，由公众和城管上报城市问题，政府工作人员处理问题

`主要技术`：RESTful API、Django、Android MVVM、RxJava2

`主要工作`：

- 为提高开源的图片选择器和应用的契合性，修改了图片选择器源码
- 采用 REST 风格开发后端 API，一套 API 同时服务移动端和 Web 端
- 主导客户端 UI 的全面升级，并添加必要功能，使用户体验大幅改善
- 解决平台地理坐标系的转换问题，开发 Android 客户端

### 地质模型在线浏览

2017年2月 - 2017年4月

`项目简介`：项目以教学为目的，满足用户在 Web 端无插件化浏览三维地质模型的需求

`主要技术`：Nginx、Google draco、three.js、Bootstrap

`主要工作`：

- 使用编码压缩技术，缩小三维模型文件的体积，使文件在网络中的传输效率提高了 30 ~ 50倍
- 编写脚本批量化编码和压缩大体积的模型文件，极大提高了文件处理的效率
- 解决 Web 端加载、渲染大体积三维模型的问题，并实现模型的旋转、缩放等交互
- 主张采用响应式设计，设计和实现前端页面，提高了网站在不同设备上的适应能力

# 专业技能

- 熟悉 TCP/IP、UDP、HTTP 等网络协议及相关编程
- 熟悉 Java 多线程、集合类、并发、JVM内存模型、垃圾回收
- 掌握常用的设计模式、数据结构和算法，熟悉面向对象编程
- 熟悉 Go、面向接口编程，熟悉 Web 后端开发
- 热爱开源，为开源社区贡献大量代码、PR、以及有意义的 Issue
- 熟悉微服务及 REST API 设计，了解前端、后端开发常见的架构，了解分布式系统
- 熟练使用 Git 进行团队协作、版本控制，具有良好的编码风格和文档习惯
- 熟悉 MySQL、MongoDB 数据库，熟悉 Docker、RxJava2、Android 等技术

---