---
title: Canary Release
layout: default
categories: canary-release
permalink: /:categories/
---

## Canary Release

没有搜到Martin Fowler这篇关于金丝雀部署（Canary Release）的翻译，我斗胆试着译一下，若以后有人想迅速了解金丝雀部署又不喜欢英文，我也算是给技术界做过知识分享的人了。

原文地址：[Canary Release by Martin Fowler](https://martinfowler.com/bliki/CanaryRelease.html)

**金丝雀发布**是一项关于软件新版本发布的技术，先将新版本发布给小部分用户，逐渐发布整体架构并且将新版本发布给所有用户，以此方式来降低发布的风险。

与蓝绿发布（BlueGreenDeployment）相似，先将要发布的新版本部署到基础架构的子集中，此时，这个子集没有用户使用。

![canary-release-1]({{ "/assets/canary-release/canary-release-1.png" | absolute_url }})

当你觉得新版本没有什么问题，就可以将新版本路由给部分用户。对于哪些用户能看到新版本有集中策略：比较简单的策略是使用随机样本；一些公司在对外发布之前选择内部用户和员工来先使用新版本；另外一个更为复杂的方法是通过用户信息和统计数据来选择测试用户。

![canary-release-2]({{ "/assets/canary-release/canary-release-2.png" | absolute_url }})

当你对新版本获得更多信心的时候，就可以发布到更多的服务并路由给更多的用户了。一个好的实践是使用PhoenixServers通过修改已存的架构来部署新版本，或者使用 ImmutableServers来提供一个新的架构并且关掉旧的架构。

金丝雀发布是一个ParallelChange的应用，集成阶段会持续到所有用户全部都路由到了新版本。那个时候，就可以关掉旧的架构。一旦新版本出现了什么问题，只需要使用回滚策略将用户路由到旧版本，知道新版本的问题修复。

![canary-release-3]({{ "/assets/canary-release/canary-release-3.png" | absolute_url }})


