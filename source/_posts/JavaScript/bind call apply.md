---
title: bind call apply
date: 2021-02-18
category:
  - 前端
  - JavaScript
tag: JavaScript
---



# bind call apply

只有函数对象 `Function.prototype` 才有的方法

## [`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

`bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

**语法：**

```js
function.bind(thisArg[, arg1[, arg2[, ...]]])
```

**返回值：**

返回一个原函数的拷贝，并拥有指定的 **`this`** 值和初始参数。

## [`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

`call()` 方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

> **注意：**该方法的语法和作用与 `apply()` 方法类似，只有一个区别，就是 `call()` 方法接受的是**一个参数列表**，而 `apply()` 方法接受的是**一个包含多个参数的数组**。

**语法：**

```js
function.call(thisArg, arg1, arg2, ...)
```

## [`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

**`apply()`** 方法调用一个具有给定`this`值的函数，以及以一个数组（或[类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)）的形式提供的参数。

> **注意：**`call()` 方法的作用和 `apply()` 方法类似，区别就是`call()`方法接受的是**参数列表**，而`apply()`方法接受的是**一个参数数组**。

**语法：**

```js
function.apply(thisArg, [argsArray])
```

## 区别

- `call()` 和 `apply()` 就传参方式不一样，似乎没有本质区别
- `bind()` 感觉是对 `call()` 的加强，可以缓存 `this`，后续再调用

## 应用

### 伪数组转换为数组

可以通过 `Array.prototype.slice.call(likeArray)` 将伪数组转换为数组，其中伪数组是：

- 能通过下标访问元素 `likeArray[i]`
- 有 `length` 属性

比如 `DOM`、`arguments`、`{0: 'foo', length: 1}` 等

> 原理是大致是因为 `splice` 会新建一个数组，然后遍历 `push`

### 获取对象类型

```js
function type (obj) {
   return Object.prototype.toString.call(obj);
}
```

### 用于继承

## 手动实现 `call()` 和 `apply()`

临时构造一个对象，让 `call()` 和传入的参数都在里面，这时候调用 `call()`，`this` 指针不就指向被调用的参数了

```js
Function.prototype.myCall = function (context) {
    // 赋值作用域参数，如果没有则默认为 window，即访问全局作用域对象
    context = context || window    
    // 绑定调用函数（.call之前的方法即this，前面提到过调用call方法会调用一遍自身，所以这里要存下来）
    context.invokFn = this    
    // 截取作用域对象参数后面的参数
    let args = [...arguments].slice(1)
    // 执行调用函数，记录拿取返回值
    let result = context.invokFn(...args)
    // 销毁调用函数，以免作用域污染
    Reflect.deleteProperty(context, 'invokFn')
    return result
}

Function.prototype.myApply = function (context) {
    // 赋值作用域参数，如果没有则默认为 window，即访问全局作用域对象
    context = context || window
    // 绑定调用函数（.call之前的方法即this，前面提到过调用call方法会调用一遍自身，所以这里要存下来）
    context.invokFn = this
    // 执行调用函数，需要对是否有参数做判断，记录拿取返回值
    let result
    if (arguments[1]) {
        result = context.invokFn(...arguments[1])
    } else {
        result = context.invokFn()
    }
    // 销毁调用函数，以免作用域污染
    Reflect.deleteProperty(context, 'invokFn')
    return result
}
```

## 手动实现 `bind()`

> **TODO**

## 体会

**关于面向对象：**

`this` 指针其实是面向对象的概念，比如 Java。把定义的函数和数据圈起来，把这个圈叫类，函数叫方法，数据叫属性，再弄个继承关系，把属性隐藏起来，整个动态函数调用，就叫面向对象了。其中 `this` 指针就永远指向整个类的实例，不能改变。

JavaScript 是基于对象的语言，它也是有面向对象的思想在里面，但是没有限制整个圈里的东西，甚至根本没有圈，`this` 也想指向谁就指向谁，你可以自己画圈去实现面向对象的大部分功能，也可以随时跳出圈外，为所欲为。

**关于实现原理：**

刨根问底式的学习不一定可取和切合实际，但是，虽然我不去看原理，可能没时间、没必要或水平不够，但是不要把这些都看成黑盒，代码都是一行一行敲出来的，即便再底层的东西，它也是实实在在的代码，最多不过0和1，不要求我弄懂所有源码，但是基本的思想还是可以去查一些相关资料了解一下的，了解了基本原理学起来才事半功倍，甚至不学胜有学，因为你无非就是那样去实现的。

## 参考

- [JavaScript 参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference)

- [javascript中call()、apply()、bind()的用法终于理解](https://www.cnblogs.com/Shd-Study/p/6560808.html)
- [让你弄懂 call、apply、bind的应用和区别](https://juejin.cn/post/6844903567967387656)

- [如何理解和熟练运用 JS 中的 call 及 apply？](https://www.zhihu.com/question/20289071/answer/93261557)

- [call、apply、bind的原理剖析及实现](https://www.cnblogs.com/zhazhanitian/p/11400898.html)