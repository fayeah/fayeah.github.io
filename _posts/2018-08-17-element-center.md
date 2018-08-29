---
title: 元素居中的问题
layout: default
categories: css17
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

- 内部元素是一个`div`

  1. 方法一

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

  当一行的文本小于等于父元素的宽度时，用`line-height`来实现时没有太大问题的，但是，如果超出这行会发生什么（下图是当我把`outer`宽度改为`60px`，`inner`的文本改长一点时`abc1艰苦奋斗`的情况）：

  ![inner-image-too-long]({{ "/assets/inner-text-too-long.png" | absolute_url }})  

  折行的文本被挤下来了，这个时候我们该怎么办呢？
  首先介绍下`line-height`是啥，  
  > line-height CSS 属性用于设置多行元素的空间量，比如文本。该属性值最好用数字，否则可能会产生不确定值。  

  具体定义参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)。  
  也就是说`line-height`的存在并非是让我们用来垂直居中的，只是偶然巧合我们可以利用它来实现。来讲第二种方式。


  2. 方法二

  使用`top: 50%`来实现，但是这个时候需要给子元素一个`absolute`的位置属性值，同时也要给其父元素一个`relative`的位置属性值，否则该子元素会相对于最近的拥有`relative`的属性值的元素垂直居中，注意，最后要给子元素一个 translateY 的`-50%`，因为 top 只是将文本的顶部做top的计算而不是本身；  

  ```
    .outer {
        height: 60px;
        width: 60px;
        background-color: yellow;
        position: relative;
    }
    .inner {
      position: absolute;
      top: 50%;
      -webkit-transform: translateY(-50%);
      transform: translateY(-50%);
    }
  ```  
  但这个方法有一个问题，就是如果行数超过了父元素的高度，怎么办，一般是在最后一行`ellipsis`，网上一般都有实现，这里就不再赘述。

- 内部元素是一个`span`

  ```
    <div class="outer">
      <span class="inner">vertical</span>
    </div>
  ```

  跟内部是一个 div 实现垂直居中的方式是一毛一样的，如果多行跟`div`几乎是一样的效果和实现。  

  3. 方法三
    W3C给出了一种很简单的方法，是在父元素没有高宽的情况下，给子元素上下`padding`来撑开，当然针对块级元素，如果是行内元素，需要改变其`display`属性值为`inline-block`；  

    ```
      .inner {
        padding: 20px 0;
      }
    ```  

  4. 方法四
   当然，还有一个比较粗暴的方法是用table，父元素的`display`为`table`，子元素的`display`为`table-cell`，并且给子元素一个`vertical-align: middle;`也可以实现：

  ```
    .outer {
      height: 60px;
      width: 600px;
      background-color: yellow;
      display: table;
    }
    .inner {
      padding: 20px 0;
    }
  ```  