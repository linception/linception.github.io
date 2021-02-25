---
title: JavaScript - 基本类型
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 基本类型

有 6 种简单类型（也称原始类型）：

- Undefined：只有一个值 `undefined`
- Null：只有一个值 `null`
- Boolean：只有 `true` 和 `false`
- Number
- String
- Symbol

1 种复杂数据类型：

- Object

## `typeof`

- `null` 认为是空对象，所以 `typeof(null)` 返回 `object`，其他都返回对应小写开头的数据类型
- 另外函数严格来讲是 Object，但是会返回 `function`

- `typeof` 声明未赋值和**未声明**的变量都返回 `undefined`

## `undefined` 和 `null`

`undefined` 是 `null` 派生来的，所以

```js
undefined == null // true
undefined === null // false
```

## Boolean 转换规则

-   非空字符串为 `true`
-   非零数值（包括无穷）为 `true`
-   非 `null` 对象为 `true`
-   其他都为 `false`

## Number 的转换规则

-   布尔值，`true` 为 1，`false` 为 0
-   `null` 为 0
-   `undefined` 为 `NaN`
-   字符串
    -   空字符串返回 0
    -   数值 `0x` 开头十六进制，否则十进制
    -   包含其他字符 `NaN`
-   对象调用 `valueOf`，再转换