---
title: Vue组件之间的通讯方式
layout: default
categories: VueCommunication
permalink: /:categories/
---

## Vue组件之间的通讯方式

组件之间需要相互的通讯，父与子，同级组件，隔代的组件之间都有可能用到，掌握这些通讯方式能很好地帮助我们实现业务，优化代码。

- props，最常见的父传数据给子之间的通讯方式，可以给定类型、默认值、是否required等，是响应式的；

  ```sh
  props: {
      msg: String
    },
  ```

- emit，子组件传递数据给到父组件，响应式的；

  ```sh
  this.$emit('eventName', arg1, arg2...)
  ```

- parent/children，可以使用`this.$parent`直接访问该组件的父组件的实例，需要有节制地使用；

- $attrs/$listners，包含了所有不被props所识别的attribute绑定，当不确定外部使用该组件时会传什么样的数据，使用$attrs是非常有用的。但是默认子组件会继承该attr，所以使用`inheritAttrs: false`来避免不必要的继承。主要在开发高级组件使用。

  ```sh
  // child comp
  <input value="value" v-bind="$attrs">
  // parent comp， 该placeholder会自动应用到input标签上
  <KInput v-model="model.username" placeholder="请输入用户名"></KInput>
  ```

 **前面都在讲父子组件，那么如果隔代组件之间需要通信有几种方式**

- vuex，状态管理，这个好理解，全局的，任何组件之间都可以相互通信；
- provide/inject，类似于react的context，主要在开发高级组件使用。其中也有很多配置项

```sh
// 父组件提供provide
provide: {
    foo: 'bar'
  },
  // 子组件注入`foo`，便可直接使用
  inject: ['foo'],
```

- event bus, 事件总线，实际上是一个Vue实例。各个组件之间都可以使用

```sh
// 创建一个event bus， 在任何文件中
export const bus = new Vue();
// 在a组件中emit一个event，需要导入bus
bus.$emit('changeIt', 'changed header');
// 在b组件中监听该event
bus.$on('changeIt', (data) => {
      this.header = data;
    })
// 可手动销毁event bus
bus.$off();
```

以上，是今天总结的关于组件之间通讯的方式。些许简陋，但是基本涵盖了集中方式及其使用。
