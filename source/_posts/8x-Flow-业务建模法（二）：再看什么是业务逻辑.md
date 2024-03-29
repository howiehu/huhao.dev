---
title: 8x Flow 业务建模法（二）：再看什么是业务逻辑
abbrlink: a7c771dd
date: 2021-04-04 17:42:01
categories:
  - 软件工程实践
tags:
  - 业务建模
  - 8x Flow
  - 业务逻辑
---

## 前言

在上一篇文章[《8x Flow 业务建模法（一）：你能分清业务和领域吗？》](/posts/2932e594/)中，向大家介绍了8x Flow背后的关键思想，即“业务逻辑和领域逻辑”分离，并介绍了业务逻辑和领域逻辑的区别。

从本篇文章开始，我将逐步为大家介绍8x Flow从分析、建模、架构再到实现的具体方法。

原计划这次讲一讲如何基于“合约上下文”进行业务分析和业务逻辑提取，但是因为收到了很多读者的反馈，希望能够更多的讲讲业务逻辑是什么意思，以便更好的“分离业务和领域”。

所以在开始进行业务分析之前，我们需要再来一篇多聊一聊：**到底什么是业务？**

<!-- more -->

## 什么是业务

在上一篇文章中，我们对于业务逻辑的定义是：

> 业务逻辑：源自业务运营的逻辑，是领域中立且运营特定的，其复杂度来自于流程本身，关注的是如何盈利和成本结构（或者可以理解为对外体现为利润或现金，对内体现为成本和绩效承诺），常见于：合同、法务、会计、审计等。

这个一眼看上去还是会比较抽象，尤其是对经验较少的人来说。

我们先来回归一下“业务（Business）”这个词的定义，在[维基百科](https://en.wikipedia.org/wiki/Business)上有着比较贴切的解释：

> Business is the activity of making one's living or making money by producing or buying and selling products (such as goods and services). Simply put, it is "any activity or enterprise entered into for profit." 业务是指通过生产或买卖产品（如商品和服务）来谋生或赚钱的活动。简单地说，它是“以盈利为目的的任何活动或企业”。

*（PS：`Business`有时候也被翻译成“商业”，但是”商业“还有另一个单词，即`Commerce`。`Commerce`一词更偏向具体的贸易、交易，而`Business`则偏向更广泛的（商业）业务。）*

结合对于以上概念解释，以下几个8x Flow对于业务逻辑的定义，就更加容易理解了：

- **业务逻辑关注的是如何盈“利”的特定运营流程**
- **“利”对外关注的是如何通过提供商品或服务盈利**
- **“利”对内关注的是如何控制成本结构和绩效**

另外，更为重要的是：**在现实中，业务活动作为企业运营的一部分，还天然的受到合同法的保护。而另外的一部分则是不涉及合同法的，这些部分往往是领域活动。**

## 业务流程即业务凭证的追溯过程

在介绍完业务一词的意思之后，我们再来看一看前面说的“特定运营流程”和“领域中立”是什么意思。

其实这个非常好理解——只需要我们往回倒退几十年，回到那个没有电子信息化辅助的年代，排除软件系统在当代对于我们的认知干扰。

让我们回想一下，如果没有软件，那个纯纸质的年代，去公对公订购或销售一件商品，那个过程是怎样的？

> 甲方：决定询价（过程） → 甲方：给出询价单（纸质凭证） → 乙方销售：决定报价（过程） → 乙方销售：给出报价单（纸质凭证） → 甲方：决定订购（过程） → 甲方：下订单或签署采购合同（纸质凭证） → 乙方销售：审验订单或采购合同（过程） → 乙方销售：订单或采购合同确认回执（纸质凭证） → 甲方财务：支付订单款项（过程） → 甲方财务：给出支付凭证（纸质凭证） → 乙方财务：核验支付记录（过程） → 乙方财务：出具收据或发票（纸质凭证） → 乙方销售：协调出库（过程） → 乙方库房：出库（过程） → 乙方库房：出库单（纸质凭证） → 乙方物流：安排运输（过程） → 乙方物流：发货单（纸质凭证）……

以上就是一个大概的不完整过程举例。

当这样一个商品的交易过程结束之后，人们怎么确认发生过这样一个交易呢？很简单，通过**追溯交易过程中所产生的凭证**：

> 甲方：询价单（纸质凭证） → 乙方销售：报价单（纸质凭证） → 甲方：订单或采购合同（纸质凭证） → 乙方销售：订单或采购合同确认回执（纸质凭证） → 甲方财务：支付凭证（纸质凭证） → 乙方财务：收据或发票（纸质凭证） → 乙方库房：出库单（纸质凭证） → 乙方物流：发货单（纸质凭证）……

如果更进一步的消除一些相关文字信息而聚焦凭证本身的话，那么就是：

> 询价单 → 报价单 → 订单或采购合同 → 订单或采购合同确认回执 → 支付凭证 → 收据或发票 → 出库单 → 发货单……

![还记得纸质凭证的样子吗？](https://huhao-dev.oss-cn-beijing.aliyuncs.com/20210404150458-2021-04-04-15-04-59.png)

**当追溯这些凭证的时候，所有的“过程”，也就是凭证是如何产生的，已经可以忽略不计了甚至记不清了（或者说不关注），这就是“领域中立”。**

**而这些可追溯凭证所串起来的流程，即“特定运营流程”，也就是“业务流程”。**

而在今天这个信息化的时代，由于软件带来的过程管理和交互的便利性，过去的相当一部分线下过程逐步被搬到了线上，所以很多时候大家都会被在线操作的众多过程记录模糊了“业务凭证”的概念和边界。

正是由于基于凭证的业务过程追溯是天然产生且客观存在的，所以我们可以说：**业务流程即业务凭证的追溯过程**。

## 业务凭证不可变且不可抛弃

既然我们现在澄清了业务流程实际上就是对于业务凭证的追溯过程，那这里不得不强调由“可追溯”所带来的一个业务凭证的特征，即：

**业务凭证具有不可变性和不可抛弃性**

什么意思呢？其实理解起来也很简单：**业务凭证代表了历史上的每一个关键业务事件的结果，历史事件一经发生，不可篡改，若篡改则是秽史；不可丢失，若丢失则不可追溯。**

拿现实中的例子来举例，例如财务记账中的开发票：

当开出一张发票后，如果发票信息有误，是不能直接作废丢纸篓的，也是不能直接修改或重开的。做出补偿的办法是先要进行“发票冲红”，即通过开具一张与原有蓝字发票一模一样的红字的“红冲发票”，来进行冲抵，然后再重新开具一张正确的蓝字发票。

（红字发票的图片太不好找了，只好找个记账的例子说明一下……）

![记账中蓝字和红字的区别](https://huhao-dev.oss-cn-beijing.aliyuncs.com/20210404154019-2021-04-04-15-40-19.png)

这个场景就是一个非常典型的“不可变”和“不可抛弃”的例子。

换句话说：**作为业务凭证，只存在创建，不存在修改和删除**（Event Sourcing也具有一样的特征，这就是“可追溯”的本质）。

**为什么我们要强调业务凭证的不可变和不可抛弃呢？因为从架构设计视角来看，如果我们给业务系统实现了CRUD（Create / Read / Update / Delete）的API，那显然就做错了，因为基于以上理论，业务系统的对外API应当只有CR，没有UD。**

如果我们不能准确的认知业务逻辑的特征，并显性的做出区分，架构上怎么能体现并满足业务的这个特点呢？从API上都无法“隔离变化”对吧？

## 业务逻辑即履约过程

在澄清了业务、业务流程、业务凭据等概念之后，让我们回到文章想要说明的关键问题上：**到底什么是业务逻辑？**

我先抛结论：

**业务逻辑，即业务的甲乙双方，基于业务合约的权责约定，进行履约的过程。在现实中，相关的履约过程在合约上下文内受法律保护。**

这句话怎么理解呢？让我们回过头来看之前的业务一词的概念，以及商品订购的那个流程：

> 业务是指通过生产或买卖产品（如商品和服务）来谋生或赚钱的活动。

> 甲方：询价单（纸质凭证） → 乙方销售：报价单（纸质凭证） → 甲方：订单或采购合同（纸质凭证） → 乙方销售：订单或采购合同确认回执（纸质凭证） → 甲方财务：支付凭证（纸质凭证） → 乙方财务：收据或发票（纸质凭证） → 乙方库房：出库单（纸质凭证） → 乙方物流：发货单（纸质凭证）……

我们会发现，所有的业务和业务凭证，都必然存在“甲乙方”，也就是“权责双方”。现实中所有的业务，都是建立在某种合约关系之上的，根据其法务严肃程度的不同，可以分为`合同（Contract）`或`协议（Agreement）`等形式，为了统一语言，我们可以统称为`合约（Contracts）`。

让我们快速脑补一下签署合同并履约的一个常见的完整过程（对于经常参与售前和投标的朋友来说应该非常熟悉）：

1. 甲方先要进行`询价（Request for Proposal，简称RFP）`，然后乙方给出`报价（Proposal）`，随后双方根据报价方案签订`合约（Contract）`。
2. 合约签订之后，双方就会根据合约中的权责条款进行逐项`履约（Fulfillment）`。
3. 每次履约实际上分成了两类，一个是`履约申请（Fulfillment Request）`，一个是`履约确认（Fulfillment Confirmation）`，分别由甲乙双方的其中一方执行，其中履约申请是一个时间段，而履约确认是一个或多个时间点（因为履约总是需要个过程，不可能瞬间完成）。

我们可以根据以上的合约签订和履约逻辑，抽象出以下的`合约上下文（Contract Context）模型`：

![合约上下文模型](https://huhao-dev.oss-cn-beijing.aliyuncs.com/合约上下文模型-2021-04-04-16-54-59.png)

**需要特别注意的是：其中的`RFP、Proposal`、`Contract`、`Fulfillment Request`、`Fulfillment Confirmation`，都是`凭证（Evidence）`，所以是需要留存和可追溯的。同时也体现了之前说的“业务流程即业务凭证的追溯过程”。**

如果以之前所说的商品订购流程来举个例子的话，其中**订单部分不完整的模型**会是这个样子：

![合约上下文不完全举例](https://huhao-dev.oss-cn-beijing.aliyuncs.com/合约上下文不完全举例-2021-04-04-17-03-01.png)

有的人可能注意到了，之前模型图上RFP和Proposal被标记为了可选的（Optional），这是因为现实业务中确实存在没有询价或报价过程的情况，例如：

- 京东、天猫等电子商城的在线商品下单，是有直接定价的，所以可被视为没有RFP，有Proposal。
- 免费的用户注册协议，没有询价和定价的过程，所以没有RFP也没有Proposal。

**是否有RFP和Proposal，必须实事求是的结合实际业务来看，我们将会在后续的文章中对此进行深入探讨。**

由于现实的业务是非常复杂的，所以通常根据甲乙方的不同，以及甲乙双方合约所处的上下文边界不同，所以相对完整的履约过程通过模型来呈现的话，大体上会呈现出类似如下的结构：

![拥有不同合约上下文的复杂业务逻辑](https://huhao-dev.oss-cn-beijing.aliyuncs.com/拥有不同合约上下文的复杂业务逻辑-2021-04-04-17-25-58.png)

但不管不同的合约上下文有多少，业务逻辑有多复杂，总是有一个关键点，那就是：

**完整的端到端业务逻辑，是不同的合约上下文的组合联系，是可以按照业务凭证的相互关系，实现完全可追溯的。**

## 结尾

在这篇文章中，我们对于什么是业务逻辑进行了更多的介绍，这将有助于了解8x Flow的后续内容。

另一方面，从本文的介绍中，我相信大家一定会意识到：

作为一名系统架构师或分析师，正确的理解什么是业务是面向业务实施系统架构设计的第一步，也是最为重要的一步。

**需要再一次特别强调的是：业务逻辑具有天然的基于合约的法律约束，这一点是现实中的客观事实。领域逻辑则往往不涉及合同法的约束。**

**而以DDD为代表的一些分析和建模理论，则天生的忽略了这一客观事实，从而易于陷入单纯的“发散-收敛”过程，忽略了清晰的问题边界。虽然DDD号称基于问题的分解来解决“核心系统复杂性”，并且事件风暴的过程比较炫酷，但实则造成了业务与领域不清，“眉毛胡子一把抓”的尴尬情况。**

**8x Flow能够识别并基于该客观事实进行分析和建模，则具有更清晰的分析和认知边界，以及更强的针对性。**

下一篇，我们将进一步利用“合约上下文”和本文最后几种“合约（Evidence）”的定义，向大家介绍如何业务进行分析并提取以凭证构成的业务逻辑，敬请期待！

> **内容声明：**“8x Flow业务建模法”为ThoughtWorks中国区CTO——徐昊先生研究并设计的原创方法论，本系列相关文章的目的是对外宣传和推广，并得到了徐昊本人的许可。文章内容为作者的个人理解和补充，如有偏差，相关权威解释以徐昊为准。

## 参考资料

- [《8x Flow 业务建模法（一）：你能分清业务和领域吗？》](/posts/2932e594/)

## 欢迎关注我的个人公众号

微信搜索：`枪炮与代码`，或者搜索公众号ID：`guns_n_code`

![枪炮与玫瑰](https://huhao-dev.oss-cn-beijing.aliyuncs.com/2020-01-20-wechat.png)
