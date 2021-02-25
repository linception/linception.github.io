---
title: JavaScript - 对象
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 对象

## `new` 内部过程

1. 在内存中创建一个新对象
2. 这个新对象内部的 [[Prototype]] 特性被赋值为构造函数的 prototype 属性
3. 构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）
4. 执行构造函数内部的代码（给新对象添加属性）
5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象

## 原型

- Object.setPrototypeOf() 可以设置原型对象，影响代码性能
- Object.getPrototypeOf()
- Object.create() 创建时指定原型对象
- Object.hasOwnProperty() 是否本身属性，`in` 包括原型

### 原型链

![UfXRZ](JavaScript - 继承/UfXRZ.png)

[\_\_proto\_\_ VS. prototype in JavaScript](https://stackoverflow.com/questions/9959727/proto-vs-prototype-in-javascript)