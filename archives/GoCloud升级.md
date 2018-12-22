---
english_title: gocloud-new-arch
title: GoCloud：模块化和可扩展性
date: 2018-06-11 12:34:56
---

开发了一个 IntelliJ IDEA / GoLand 插件

<!-- more -->

# 旧的问题

GoCloud 支持多个云服务提供商，每一个云服务都有多个模块，之前的代码是，所有云服务对象都要实现一个共同的 `interface`，这就导致了

假设 A B C 云服务提供商支持 a b c d e 5种功能服务

- 当我们要实现 D 提供商，它不支持 e 服务，这时扔需要给 D 假装实现 e 接口，用户在调用的时候就会被提示 D 不支持 e ；
- 假设我们需要为 A 实现一个新的功能服务 f ，但 B C D 都不支持 f ，那我们仍要假装实现；

这对于用户和我们自己的开发来说，都是极其糟糕的

# 新的解决

将接口模块化，使得

- 用户模块化调用
- 我们模块化开发
- 仍然可以保证 GoCloud 的初衷：提供统一的 API

我将 `GoCloud 提供统一的 API` 化解为了 `GoCloud 的每个模块都提供统一的 API`

现在，GoCloud 可以这样调用了

```
gocloud.AmazonProvider().MachineLearning().CreateMLModel()
```

medium 推文

https://medium.com/gocloud/gocloud-modular-scalable-db61160138aa

代码实现

https://github.com/cloudlibz/gocloud/pull/101



