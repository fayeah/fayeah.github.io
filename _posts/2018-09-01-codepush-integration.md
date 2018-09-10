---
title: Codepush集成IOS
layout: default
categories: codepush-integration
permalink: /:categories/
---

## Codepush集成IOS

 如果是RN的，尽量不要使用RN的方式添加sdk，因为单纯用native会比较简单。


----------
1. 新建一个ios的app（[https://appcenter.ms/apps](https://appcenter.ms/apps)）；
2. 在“Getting Started”页面按照步骤添加，做的非常人性化，app的secret都写上来了，直接copy and paste；
3. 我这次集成主要为了查看app crash的日志，需要在“diagnositics”的子目录“symbol”里面上传一个zip文件，这个文件是由dSYMs压缩而来；


----------
dSYMs在archive的时候生成的，找到该文件夹的方法如下：
1. Chose Window > Organizer in Xcode.
2. Select the tab Archives.
3. Select your app in the left sidebar.
4. Right-click on the latest archive and select Show in Finder.
5. Right-click the .xcarchive in Finder and select Show Package Contents.
6. You should see a folder named dSYMs which contains your dSYM bundle. If you use Safari, just drag this file from Finder and drop it on to the corresponding drop zone in HockeyApp. If you use another browser, copy the file to a different location, then right-click it and choose Compress YourApp.dSYM. The file will be compressed as a .zip file. Drag & drop this file to HockeyApp.
