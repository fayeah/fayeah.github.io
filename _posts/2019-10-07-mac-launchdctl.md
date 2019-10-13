---
title: Mac Launchdctl
layout: default
categories: mac-launchdctl
permalink: /:categories/
---

## Mac Launchdctl

一个build mahichine必须要有build所需要的所有的denpendencies，有些dependency是install之后就可以直接用的，但是，有一些需要该machine启动时boot up的，比如VPN或一些build agents，那我们又不想每次machine启动的时候手动去start这些依赖，所以machine本身提供了一些工具帮助我们自动地管理所需要的依赖，Lunux使用的是Systemctl，那么Mac则是用Launchdctl。

一般来讲，build的过程是在Linux机器上运行的，但是但凡涉及到IOS的build就必须要在Mac的OS上进行，所以这个时候我们也需要做Mac的Daemons/Agents管理。

Note：

1. 创建一个User来launch Daemons/Agents当然也是可以的，但是后来发现，在build app的时候会遇到许许多多的权限问题，所以我个人认为实际上不需要创建用户，直接在主用户的系统上run即可，减少很多不必要的麻烦。

2. 有一个很好用的工具帮我们check customized Daemons/Agents的status，也可以进行reload/unreload等操作，LaunchControl - The launchd GUI。

下面来详细介绍如何创建一个Hello World launchd job

要在launchd下面run，就必须有一个property file的配置文件。Daemons和Agents的pfile结构是一致的，只不过描述Daemons的pfile在`/Library/LaunchDaemons`，而描述Agents的pfile在`/Library/LaunchAgents`或user的相应的Library目录。

基本的hello world property file是这样的：

```bash
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.hello</string>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/local/bin/node</string>
      <string>/Users/userName/Documents/workshop/mynode.js</string>
    </array>
    <key>StandardErrorPath</key>
    <string>/var/log/myerror.log</string>
    <key>StandardOutPath</key>
    <string>/var/log/myjob.log</string>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <false/>
</dict>
</plist>
```

由于我是root在run，所以`sudo launchctl load myDeamon.plist`之前，需要改变plist file的权限，目前是`-rw-r--r--   1 root  staff   630 Oct 13 21:51 myDeamon.plist`。需要chmod root以及改为644的权限，并使用root方式来load。这不是应该学习的，我为了实践就没有管权限的东西了。应该用normal的用户来做normal的操作。

- Label：代表launchd的唯一字符串，必写；
- ProgramArguments：launchd的参数，必写；
- KeepAlive：表示按需启动还是始终在run，建议按需启动，因为不需要的时候不会占用memory，launch-on-demand是默认设置；
- StandardOutPath，for debug；

当然，实际项目中要比这个复杂的多，我们是使用launchctl+playbook来共同完成的，并且里面的param是不可以写final的，需要从外部传进来，还有一些jar包也需要进行拷贝等等。需要个人在项目中总结。
