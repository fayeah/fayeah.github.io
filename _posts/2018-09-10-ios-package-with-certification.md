---
title: IOS打有证书的包
layout: default
categories: ios-package
permalink: /:categories/
---

## IOS打有证书的包

1. target下拉列表选择edit scheme，build configuration选择release，close。
2. device选择“Generic iOS Device”。
![generic]({{ "/assets/ios-package/generic.png" | absolute_url }})  
3. archive
![archive]({{ "/assets/ios-package/archive.png" | absolute_url }})  
4. 保证证书导入正确：
![import]({{ "/assets/ios-package/import.png" | absolute_url }})  
**NOTE:** 如果飘红，将Daimler_broadcast解压导入，qa和uat不用管
![certification-file]({{ "/assets/ios-package/certification-file.png" | absolute_url }})  
5.  archive成功之后export为enterprise
![export]({{ "/assets/ios-package/export.png" | absolute_url }})  
6. app Thinning选择一个机型, 一路next到export就可以了.
