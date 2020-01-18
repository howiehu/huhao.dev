---
title: 领域驱动实战思考（三）：DDD的分段式协作设计
abbrlink: 61190ae2
categories: 
  - - Domain Driven Development
tags:
  - DDD
---

## 前言

在我的[上一篇文章](https://huhao.dev/posts/58fe0824/)中，给大家介绍了我在实践中对于DDD设计过程进行梳理的思考。本篇则是向大家整体介绍一下我的“DDD分段式协作设计”的步骤和内容。

同时，该方法的基准化操作手册，也在曾经的一篇文章中[公开提供了下载](https://huhao.dev/posts/130bb570/)，可以作为更细化的内容进行参考和使用。

需要说明的是，不同的咨询师在实施DDD的设计过程中手法都不一样，我仅是从我所实施过的咨询项目出发，提供了一种经反复验证可工作的方式，仅供参考，也欢迎大家进行交流。

<!-- more -->

## DDD解决的问题和方法

在介绍分段式设计之前，让我们回顾一下DDD希望解决的问题：

> 系统核心复杂性

![DDD与传统设计方法的对比](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050456.png)

![DDD核心原则](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050540.png)

![DDD是更有套路的设计方式](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050542.png)

## DDD的分段式协作设计

### 战略设计

![事件风暴](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050210.png)

![限界上下文依赖关系](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050302.png)

![问题子域划分](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050316.png)

### 战术设计

![领域建模](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050342.png)

![业务服务划分](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050358.png)

![业务服务接口能力识别](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-15-050408.png)

### 技术实现

## 总结

## 领域驱动设计练功房

<img src="https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-16-123317.jpg" alt="领域驱动设计练功房（第一期）" style="zoom:50%;" />

---

## 参考资料