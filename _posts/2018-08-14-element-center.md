---
title: 元素居中的问题
layout: default
categories: css
permalink: /:categories/
---

## 垂直居中（我们外层一定有一个 div，这个 div 有高宽）  
```
  // html
  <div class="outer">
    <div class="children-elements"></div>
  </div>

  // css
  .outer { 
      height: 60px; 
      width: 600px; 
      background-color: yellow; 
  } 
```  

### 第一种情况，内部只有一个子元素

- 内部元素是一个 div  
  
  ```
    <div class="outer">
      <div class="inner">vertical</div>
    </div>
  ```  
  那么我们只需要给 inner 一个与 outer 高度相等的 line-height 就可以实现： 

  ```
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

### 第二种情况，内部有两及以上子元素，我们以希望内部元素在同一行并且相对父元素垂直居中  

```
  <div class="outer">
    <div class="inner">vertical</div>
    <div class="inner">vertical</div>
  </div>
```  

那么首先我们需要让子元素放在一行，由于`div`是一个block元素，所以默认会换行，所以我们改变`div`的`display`属性，然后再给这两个`div`一个`line-height`的值即可：  

```
  .inner { 
    display: inline-block;
  }
```  