---
title: JavaScript - 变量
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 变量

## `var`

-   函数作用域
-   变量提升，声明提升到最前面，未声明时使用为 `undefined`

## `let`

-   块作用域
-   暂时性死区，未声明时使用报错。区别于 `var` 的作用域提升

### `var` 与 `let` 的区别

| 区别           | var                   | let                  |
| -------------- | --------------------- | -------------------- |
| 作用域         | 函数                  | 块                   |
| 声明前使用     | 作用域提升，undefined | 暂时性死区，报错     |
| 重复声明       | 覆盖                  | 报错                 |
| 全局作用域声明 | 成为 window 属性      | 不会成为 window 属性 |

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

> **理解：**因为 lambda 表达式会对 `let` 记录一个当时的值，`var` 只会记录这个变量

## `const`

-   和 `let` 类似，但是不能修改值，可以修改引用内的值
-   引用内的值也不想修改时，用 `Object.freeze`

## 使用建议

1.  不使用 `var`
2.  `const` 优先，`let` 次之