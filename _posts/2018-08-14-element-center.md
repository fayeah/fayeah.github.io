---
title: 元素居中的问题
layout: post
categories: css
permalink: /:categories/
---

## 垂直居中（我们外层一定有一个div，这个div有高宽）
  #### 第一种情况
    - 内部元素是一个div
      `
        <div class="outer">
          <div class="inner">vertical</div>
        </div>
      `
      那么我们只需要给inner一个与outer高度相等的line-height就可以实现：
      `
        .outer {
          height: 60px;
          width: 600px;
          background-color: yellow;
        }
        .inner {
          line-height: 60px;
        }
      `
    - 内部元素是一个span
      `
        <div class="outer">
          <span class="inner">vertical</span>
        </div>
      `
      跟内部是一个div实现垂直居中的方式是一毛一样的。