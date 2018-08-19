---
title: 元素居中的问题
layout: default
categories: css
permalink: /:categories/
---

## 垂直居中（我们外层一定有一个 div，这个 div 有高宽）

### 第一种情况

- 内部元素是一个 div  
  ```
    <div class="outer">
      <div class="inner">vertical</div>
    </div>
  ```  
  那么我们只需要给 inner 一个与 outer 高度相等的 line-height 就可以实现：  
  ```
    .outer { 
      height: 60px; 
      width: 600px; 
      background-color: yellow; 
    } 
    .inner { 
      line-height: 60px; 
    }
  ```  
- 内部元素是一个 span    
  ```
    <div class="outer">
      <span class="inner">vertical</span>
    </div>
  ```   
  跟内部是一个div实现垂直居中的方式是一毛一样的。
