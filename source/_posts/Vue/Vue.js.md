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

## 快速开始

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<div id="app">
  {{ message }}
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

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

<img src="https://cn.vuejs.org/images/lifecycle.png" style="zoom:50%;" />

## 模板语法

### 文本插值

文本插值，html 会被转义，可以使用 JavaScript 表达式，支持 [全局变量的一个白名单](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9)

```html
{{ 表达式 }}
```

插入 html 可以用 `v-html` 指令，属性用 `v-bind` 指令

### 指令

```html
<!-- 动态参数 -->
<a v-bind:[attributeName]="url"> ... </a>
<!-- 修饰符 -->
<form v-on:submit.prevent="onSubmit">...</form>
```

### 简写指令

-   `v-bind:` 简写为 `:`
-   `v-on:` 简写为 `@`

## 计算属性

```js
// 默认 getter
computed: {
  fullName: function () {
    return this.firstName + ' ' + this.lastName
  }
}
// 可以指定 getter 和 setter
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```

>   计算属性会缓存，如果依赖的属性不变不会重新计算

## 监听器

```js
watch: {
  // 如果 foo 发生改变，这个函数就会运行
  foo: function (newValue, oldValue) {
  }
}
```

