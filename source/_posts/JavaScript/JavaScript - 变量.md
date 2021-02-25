---
title: JavaScript - 变量
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 变量

## `var` 与 `let` 的区别

- `var` 存在作用域提升，`let` 没有
- `var` 可以重复声明，`let` 不能
- `var` 为函数作用域，`let` 为块作用域
- 全局作用域中声明时，`var` 会成为 `window` 的属性，`let` 不会

## `for` 循环中的 `var` 与 `let`

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

> **理解：**因为 lambda 表达式会对 `let` 记录一个当时的值，`var` 只会记录这个变量