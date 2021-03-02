---
title: Vue.js
date: 2021-03-01
category:
  - 前端
  - Vue.js
tag: Vue.js
---

# Vue.js

## 知识体系

{% markmap %}

-   Vue 实例

    -   生命周期

-   模板语法

    -   插值

    -   指令

        -   动态参数

        -   修饰符

        -   简写

-   计算属性

-   监听器

-   class

-   style

-   条件渲染

-   列表渲染

-   事件处理

-   输入绑定

-   组件

-   动画

-   路由

{% endmarkmap %}

## Vue 实例

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的响应式系统中

```js
let obj = {
  foo: 'bar'
}

let vm = new Vue({
  el: '#app',
  data: obj
})

// vm.foo == obj.foo
// 创建之后添加的数据不会绑定
// 另外实例的一些内置属性加了$，比如vm.$data === obj
```

>   不要在属性的函数传参上使用箭头函数，因为箭头函数的 `this` 问题

### 生命周期

![](Vue.js/lifecycle.png)

