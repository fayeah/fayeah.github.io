---
title: Git Submodule
layout: default
categories: git-submodule
permalink: /:categories/
---

## Git Submodule

设想这么一种场景，多个projects想要使用一个common的feature，这个feature想要另外一个角色或者团队独立维护，是可以customize的，那么我们应该怎么做呢？可能会作为npm dependency（对node来说），也可能会采用copy这个common的code到各自的project里面。

当然这两种方法不是不可以，但是会造成一些问题，比如同步比较麻烦，因为那个library也一直在更新，也难以deploy，因为每一个project都必须保证该library是available的。

针对这种情况，GIT就提供了一种很方便的工具，git submodule。
