---
title: JavaScript 总结
date: 2021-02-20
category: JavaScript
tag: JavaScript
---

# JavaScript 总结

## 参考

- 《JavaScript 高级程序设计（第4版）》[^1]

[^1]: 源码地址：https://www.ituring.com.cn/book/2472

## js 的加载

### `defer` 和 `async` 的区别

- `defer` 保证顺序，`async` 无序
- `defer` 保证在 `DOMContentLoaded` 事件前加载完毕

![](https://gitee.com/sharonlee/images/raw/master/20210220233046.png)

参考：

- [defer和async的区别](https://segmentfault.com/q/1010000000640869)

### 动态加载

```js
let script = document.createElement('script'); 
script.src = 'gibberish.js'; 
script.async = false; 
document.head.appendChild(script);
```

## 变量声明

### `var` 与 `let`

- `var` 存在作用域提升，`let` 没有
- `var` 可以重复声明，`let` 不能
- `var` 为函数作用域，`let` 为块作用域
- 全局作用域中声明时，`var` 会成为 `window` 的属性，`let` 不会

### `const`

`const` 类似 `let`，声明时必须赋值，当然不可修改

### `for` 循环中的 `var` 与 `let`

```js
for (var i = 0; i < 5; ++i) {
	setTimeout(() => console.log(i), 0)
}
// 输出：5 5 5 5 5

for (let i = 0; i < 5; ++i) {
	setTimeout(() => console.log(i), 0)
}
// 输出：0 1 2 3 4
```

> **我的理解：**因为 lambda 表达式会对 `let` 记录一个当时的值，`var` 只会记录这个变量

## 数据类型

### 分类

有 6 种简单类型（也称原始类型）：

- Undefined：只有一个值 `undefined`
- Null：只有一个值 `null`
- Boolean：只有 `true` 和 `false`
- Number
- String
- Symbol

1 种复杂数据类型：

- Object

### `typeof`

- `null` 认为是空对象，所以 `typeof(null)` 返回 `object`，其他都返回对应小写开头的数据类型
- 另外函数严格来讲是 Object，但是会返回 `function`

- `typeof` 声明未赋值和**未声明**的变量都返回 `undefined`

### `undefined` 和 `null`

`undefined` 是 `null` 派生来的，所以 `undefined == null` 为 `true`

### Boolean

**转换规则：**

![image-20210221012000316](https://gitee.com/sharonlee/images/raw/master/image-20210221012000316.png)

### Number

**转换规则：**

![image-20210221013656546](https://gitee.com/sharonlee/images/raw/master/image-20210221013656546.png)

### Symbol



## 标签函数

```js
let ret = tagFun`${a} + ${b} = ${a + b}`
function tagFun(strings, ...expressions) {
  // strings 为 ${} 分割的字符串数组
  // expressions 为 ${} 中的每个表达式的值
}
```

**用标签函数实现不用标签函数拼接字符串的功能：**

```js
function noTag(strings, ...expressions) { 
  return strings[0] + expressions.map((e, i) => `${e}${strings[i + 1]}`).join(''); 
}
```

## 操作符

