---
layout    : post
title     : "watchOS apps"
subtitle  : " \"Apple Watch基本概念与介绍\""
date      : 2023-11-15
author    : "heliang"
header-img: "img/contact-bg.jpg"
catalog   : true
tags      : 
    - widget
---

### The watchOS app

主应用程序是你watchOS 应用程序体验的基础，任何人可以直接打开您的应用程序并与之交互。但是，应用程序界面不一定是用户与您的应用程序交互的主要方式。用户可能更喜欢通过复杂功能，或者通知进行交互，并且可能永远不会明确启动您的应用程序。

### Complications
复杂功能可以让用户直接在表盘上一睹应用程序的数据。用户可以为大多数表盘添加复杂功能。但是它的空间是有限的。设置复杂功能的目的就是展示及时性、最新、有用的信息。

### Notifications
和iOS一样，分为本地通知和远程通知。

### Siri
可以使用SiriKit, 增加app的交互性

### Health and fitness
为watchOS创建健康与健身应用。可以使用HealthKit

- 配置healthKit
- 授权访问 health data
- 保存数据到healthKit
- 从healthKit中读取数据
- 用watchOS创建健身应用

### Runtime management
- [Background execution]('https://developer.apple.com/documentation/watchkit/background_execution')
- [Life cycles]('https://developer.apple.com/documentation/watchkit/life_cycles')
- [Using extended runtime sessions]('https://developer.apple.com/documentation/watchkit/using_extended_runtime_sessions')
  当用户放下手腕时候，watchOS通常会进入后台或者挂起状态。这时候，如果你不想让程序挂起，你可以使用 后台任务和 extented runtime sessions 来保活

  后台任务主要是指监控锻炼、追踪用户位置，播放音频文件。
  拓展会话支持一下任务类型
  - Self care
    引导用户完成相对简短的活动。这些活动关注用户的情绪健康或健康，例如刷牙
  -  Mindfulness(正念)
  -  Physical therapy
  -  Smart alarm
    安排一个时间窗口来监测用户的心率和运动。该应用程序使用此信息来确定播放闹钟的最佳时间，通常是将用户从睡眠中唤醒

    * 苹果强调，为了保持apple watch 的高性能，要求开发者限制延长运行时会画期间执行的工作量，如果app 长时间保持了较高的cpu使用率，系统会取消的延长后台会话。

- app在后台时候使用蓝牙刷新

### Network request


### Unit tests

[参考链接]('https://developer.apple.com/documentation/watchos-apps/')
