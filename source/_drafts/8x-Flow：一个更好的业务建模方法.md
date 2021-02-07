---
title: 8x Flow： 一个更好的业务建模方法
abbrlink: "2932e594"
categories:
  - 软件工程实践
tags:
  - 业务建模
  - 领域驱动设计
  - 8x Flow
  - 事件风暴
---

## 前言

最近两年，以“事件风暴（Event Storming）”为代表的“领域驱动设计（Domain Driven Design，以下简称DDD）”分析建模方法红遍大江南北。**伴随着按照DDD思想指导微服务拆分的流行，“搞微服务必用DDD，用DDD必做事件风暴，写代码必用六边形架构”的做法已几乎成为了某种所谓的“最佳实践”。**

**虽然我们一边反复强调“DDD不是银弹，事件风暴也不是DDD”，但是还是眼睁睁的看着DDD被用成了银弹，用了事件风暴也被等同于做了DDD。**

这两年，我也做了不少DDD的实践和咨询服务，也写过一些文章和组织过工作坊。但是在持续的解决不同的客户需求的过程中，确实经历了一个从“忽视到真香，再从真香到疑惑”的过程。其中在使用DDD和事件风暴的过程中，经常困惑的一些典型案例（也是经常被问到的问题）包括：

- 数据类应用的设计和开发如何应用DDD思想？
- 客户交易系统和GIS这样的系统，DDD应用上有何区别？
- 很明显的流程类功能或系统适合DDD吗？还是用个工作流引擎就完了？
- 以上这些系统的分析建模都能应用事件风暴吗？还是说可以用其它方法？

在这个过程中，我感觉到DDD中存着某种非常模糊难以说清的东西，阻碍了以上问题的边界识别和清晰回答——总的来说呢，DDD的战略和战术设计，以及通过事件风暴来进行分析和建模的方法，更让我感受到所谓DDD是“OO Done Right”这句话，更像是说“我们在原有的面向对象方法之上，从一个人拍脑袋，变成了大规模协作式拍脑袋，反正依然是拍脑袋”。

换句话说，DDD当前的实践，尤其是基于事件风暴和领域建模方法，更像是一套过程炫酷的头脑风暴法，归根到底，其本质是头脑风暴，所以以上问题也就不能期待有什么清晰解答了，一切都是“By Experience（凭经验）”。

[一切跟着感觉走.png]()

幸运的是，在和**ThoughtWorks中国区CTO徐昊**一起推动本公司工程效能变革的过程中，我了解并学习到了一套**基于徐昊对于软件工程和架构设计多年的实践和思考，由他总结沉淀的，从“四色建模”所发展出来的，被称之为“8x Flow”的业务建模方法**，有效的解答了我之前对于DDD和事件风暴的困惑。

在此，我将利用一系列文章，将相关的思想、方法和配套的实践分享给大家，希望能够对大家有所帮助，同时也希望得到更多的碰撞和反馈。

<!-- more -->

## 8x Flow核心思想

在介绍基于8x Flow的业务建模过程之前，大家需要先了解8x Flow背后的关键思想。有关于徐昊对于这些思想的说明，以及他从四色建模开始的文章和视频，我作为参考资料附在了文章结尾，欢迎大家参阅。在此，我更多的是基于我的理解来向大家予以介绍。

### 领域逻辑 vs 业务逻辑

![领域逻辑 vs 业务逻辑](https://huhao-dev.oss-cn-beijing.aliyuncs.com/domain-and-business-2021-02-07-17-27-09.png)

![医院门诊就诊流程](https://huhao-dev.oss-cn-beijing.aliyuncs.com/医院门诊就诊流程-2021-02-07-23-02-25.png)

![医院门诊就诊-事件风暴](https://huhao-dev.oss-cn-beijing.aliyuncs.com/医院门诊就诊流程-事件风暴-2021-02-07-23-02-37.png)

![医院门诊就诊-业务与领域识别](https://huhao-dev.oss-cn-beijing.aliyuncs.com/医院门诊就诊流程-业务与领域识别-2021-02-07-23-02-48.png)

![医院门诊就诊-业务流程](https://huhao-dev.oss-cn-beijing.aliyuncs.com/医院门诊就诊流程-业务流程-2021-02-07-23-03-00.png)

### 业务即履约过程

## 8x Flow过程简介

（由于8x Flow的分析建模过程较长，所以这里仅给大家做关键内容的简介，便于快速了解8x Flow。关于具体的过程及操作方法，我会从下一篇文章开始，分步骤做详细介绍。）

![8x Flow - 业务建模基准图例](https://huhao-dev.oss-cn-beijing.aliyuncs.com/8xFlow基准图例-2021-02-07-19-04-33.png)

### 业务凭证分析

![8x Flow - 业务凭证分析](https://huhao-dev.oss-cn-beijing.aliyuncs.com/业务凭证分析-2021-02-07-18-59-59.png)

### 相关元素分析

![8x Flow - 相关元素分析](https://huhao-dev.oss-cn-beijing.aliyuncs.com/相关元素分析-2021-02-07-19-05-21.png)

### 角色分析和抽象

![8x Flow - 角色分析和抽象](https://huhao-dev.oss-cn-beijing.aliyuncs.com/角色分析和抽象-2021-02-07-19-05-30.png)

### 上下文识别和划分

![8x Flow - 上下文边界识别](https://huhao-dev.oss-cn-beijing.aliyuncs.com/上下文边界识别-2021-02-07-19-05-43.png)

### 后续工作

## 总结

### 8x Flow 仅适用于业务建模

## 参考资料

- [《运用四色建模法进行领域分析》（作者：徐昊）](https://www.infoq.cn/article/xh-four-color-modeling)
- [《八叉说 - 我们到底要微服务还是业务能力？》（作者：徐昊）](https://www.bilibili.com/video/BV1Rf4y1Q7Y4)
- [《八叉说DDD - 领域驱动还是业务模型驱动？》（作者：徐昊）](https://www.bilibili.com/video/BV1MT4y1M7Kv)
- [《八叉说DDD - 统一语言的坏味道》（作者：徐昊）](https://www.bilibili.com/video/BV1Rz4y1S7oW)
- [《八叉说DDD - 为什么说《领域驱动设计》已经过时了》（作者：徐昊）](https://www.bilibili.com/video/BV1mf4y1k75k)
- [《八叉说 - 当DDD遇到业务系统，还是最佳实践吗？》（作者：徐昊）](https://www.bilibili.com/video/BV1Ep4y1W7Ku)