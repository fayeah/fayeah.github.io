---
title: Azure Blob Storage
layout: default
categories: azure-blob-storage
permalink: /:categories/
---

## Azure Blob Storage

设想如果有一个加载图片的需求，你会这么设计呢？总的来说大概会有以下想法：

- build到app里，那build到app里也有不同的方式；
  - 图片放在Repository里面，build到app里；
  - 将图片以base64的形式写在代码里；（会大 800/600 size）

- 图片存放在其他地方，比如Azure blob storage；

当然，不同的需求会有不同的解决方案，比如一些icon，就只有30-40 bite，直接build到app就可以，那么对于一些需要用户自己上传的图片，比如profile avator，或者thumbnail image等，大概有的不到200k，当然上传也需要size的limit，但是总的来说build到app里就会影响包的大小，对performance是有影响的，特别是大的图片，那么这个时候就需要放在其他地方存储，需要的时候再加载。

这里我重点介绍下如何使用Azure Blob Storage来存储图片并且显示到react native的app上。

大概的设计思路是这样的：

- db加一列来存储image的相对url（"images/id.png"），在app/bff来concat azure的domain，因为不同环境的domain是不一样的;
- RN使用remote image的方式加载，这里的问题是，一个image是不够的，因为要适配不同像素的app，所以同一个image需要在azure上存三个大小的图片，那么db里面也需要存以逗号隔开的url（"images/id.png，images/id@2x.png,images/id@3x.png"），api就需要以array的方式返回(`[{uri: images/id.png, width: 128, height: 128},{uri: images/id@2x.png, width: 256, height: 256},{uri: images/id@3x.png, width: 384, height: 384}]`)；
- RN remote加载图片有一个图片缓存问题，当只改变azure的图片，url不变时，RN仍然使用缓存的图片，于是，我们在每次上传或者更新图片时都需要更新image url，给image name加了一个timestamp（"images/id-1570547748949.png，images/id-1570547748944@2x.png,images/id-1570547748966@3x.png"）；

对于创建blob storage，Azure Blob Storage提供几种资源：

1. storage account；
2. container 在storage account里面；
3. blob 存在container 里面，blob是可以有folder的；
![blob-container-relationship]({{ "/assets/blob-storage/blob-storage.png" | absolute_url }})

创建storage account和container有多种方式，我尝试过三种方式：

- 最简单的一种，使用[azure的portal](https://portal.azure.com/)来创建；
- 使用az-cli来创建，前提是需要安装az-cli；

  ```bash
  az storage blob upload --container-name customized-container --name "images/$(basename "$entry")" --file "$entry" --connection-string "${CONNECTION_STRING}"
  ```

- 使用terraform在infra的配置里面去创建；

```bash
provider "azurerm" {}

resource "azurerm_storage_account" "storage_account" {
  name                     = "${var.environment}"
  resource_group_name      = "${var.resource_group_name}"
  location                 = "${var.resource_group_location}"
  account_tier             = "Standard"
  account_replication_type = "LRS"
  account_kind             = "StorageV2"
}

resource "azurerm_storage_container" "storage_container" {
  name                  = "container"
  storage_account_name  = "${azurerm_storage_account.storage_account.name}"
  container_access_type = "blob"
}

```

所创建的storage account是public还是private取决于业务，一般来讲，会有两个storage account，一个是public，不论是否登陆用户都可以看到的图片，另外一个是private，比如想profile image这种，然后不同的account里面再创建domain相关的container。public的account使用url直接下载是不需要密钥的，但是private需要，这个我暂时还没有研究清楚，到时候清楚了会补上。

可以看到terraform是不需要connection-key的，terraform自己在创建了account之后进行了内部处理。另外，connection-key是account level的，所以container是可以随意的删除增加，没有影响。

绝大部分的工作在于保证db的url跟blob storage的image name相对应，因为目前我们使用的是static的几张图片，并没有portal给用户上传更新，所以也写了一些脚本来保持同步，当然，图片还是要存在在后端service里面的，只不过需要在CI上加一个task来upload 所需要的images。一旦有了portal，这些手动的部分也不会有了。
