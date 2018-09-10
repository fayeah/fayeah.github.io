---
title: APP Integrate with tingyun
layout: default
categories: tingyun-integration
permalink: /:categories/
---

## APP Integrate with tingyun

在做这件事的时候遇到了不少坑，一个是我自己对native不熟悉，另外一个文档写的略有出入，这里我就分享下自己趟过的坑，说不定我3.5天做到的事情，大家一个上午就做好了。  

【Android】

- 首先保证在做集成之前app是能够正常build的，MBB是用的RN，所以build的方式有多种，这里不建议用AS（Android Studio）去build，因为可能会遇到一些依赖没安装或者比较奇怪的异常比如':app:recordFilesBeforeBundleCommandDebug'，解决起来甚是耗费时间，我们的重点在于只要能build成功即可，不管啥方式（react 目录下run `react-native run-android`,Android目录下run`./gradlew installDev`, apk目录下run`adb install`/`add -s simulatorId install apk`,选择一种即可）。
- 查看官方帮助文档，我们用的是Android with gradle，所以参考[http://doc.tingyun.com/app/html/Android-Gradle.html](http://doc.tingyun.com/app/html/Android-Gradle.html)即可，只要一步一步跟着文档走。
- 文档中涉及到混淆/Proguard的内容我都一头雾水，直到我后来知道混淆是怎么回事并且MBB也没有用到混淆，所以主要涉及到混淆的地方我们直接忽略即可。（混淆是为了保证我们app的安全性以及资源压缩的一种打包流程之一,gradle的配置去搜索`enableProguardInReleaseBuilds`值是否为false）。
- 当嵌码成功，我们的工作基本上就完成了99%，最后一步就是验证tingyun采集的数据（每一分钟更新一次），当我用我们的huawei测试机测试的时候，一直出现"error code -1”的情况，并没有显示connect success，后来非常tricky的是，我用twdata和twguest都连接不上，只有用我的4G才可以，客户现场的wifi也可以，所以至今不知道原因，我们可以问下tingyun的support。至此，Android integrate tingyun成功。

【IOS】

- 同样地，保证用Xcode能够成功build，这里说一下simulator的build比较简单不需要certification，但是如果要在真机上测试，xCode要用自己的appleId，但有时候用自己的appleId,signing的时候也会出现’push notification’的error，我们需要在‘general’里面的’push notification’给off掉，就可以使用自己的appleId了。如图：
![tingyun-ios]({{ "/assets/tingyun/ios.png" | absolute_url }})  

- ios也有自己的帮助文档，但是我不建议看basic的http://doc.tingyun.com/app/html/iOSplatform.html，最好在自己新建的app，有一个’现在嵌码’的链接，这里的文档比basic的要详细一些，同样地，按步骤来。
- 我们用的是swift，加NBSAppAgent.startWithAppID("appId");是在AppDelegate.swift文件里面，但是build的时候仍然会说’NBSAppAgent’不可以identity，通过google我才知道我们需要在’BridgingHeader.h'文件里面引入’NBSAppAgent’，` #import <tingyunApp/NBSAppAgent.h>`，当然文档里面没有说明。
- 当我们在给pch文件在build setting里面对prefix Header进行设置的时候，只要写pch文件名即可，不需要写工程名，否则是找不到pch文件的。
- 有时候发现`pod install`不work，报个错误，是因为我们从Sierra升级到High Sierra的时候对ruby环境做了某种改变，这时候我们要做的就是` brew uninstall cocoapods; brew install cocoapods`即可，简单粗暴。
- 还学到一个技能，原来真机上在我们的debug的app摇一摇就能看到debug设置。

最后，当然这是我自己的一些实践，可能因为我们环境的不同，语言的不同，构建工具的不同，也有可能出现其他的问题，只是做个小小的总结。