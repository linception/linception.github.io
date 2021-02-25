---
title: JavaScript - 数据类型
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 数据类型

## 分类

有 6 种简单类型（也称原始类型）：

- `Undefined`：只有一个值 `undefined`
- `Null`：只有一个值 `null`
- `Boolean`：只有 `true` 和 `false`
- `Number`
- `String`
- `Symbol`

1 种复杂数据类型：

- `Object`

## `typeof` 操作符

-   除了 `null`，返回对应小写开头的数据类型

- `null` 认为是空对象，所以 `typeof(null)` 返回 `object`
- 函数严格来讲是 `Object`，但是会返回 `function`

- `typeof` **未赋值**和**未声明**的变量都返回 `undefined`

## `undefined` 和 `null` 类型

`undefined` 是 `null` 派生来的，所以

```js
undefined == null // true
undefined === null // false
```

## `Boolean` 类型

### 转换规则

| 数据类型    | 转换为 `true`    | 转换为 `false` |
| ----------- | ---------------- | -------------- |
| `String`    | 非空             | `""` 空字符串  |
| `Number`    | 非零（包括无穷） | `±0`、`NaN`    |
| `Object`    | 非 `null`        | `null`         |
| `Undefined` | -                | `undefined`    |

## `Number` 类型

### 特殊值

-   `+0`、`-0`
-   `+Infinity`、`-Infinity`
-   `NaN`

### 转换规则

-   布尔值，`true` 为 1，`false` 为 0
-   `null` 为 0
-   `undefined` 为 `NaN`
-   字符串
    -   空字符串返回 0
    -   数值 `0x` 开头十六进制，否则十进制
    -   包含其他字符 `NaN`
-   对象调用 `valueOf`，再转换

>   `Number` 只能包含数字，`parseInt` 数字开头就行

## `String` 类型

### 模板字符串

```js
`${表达式}`
```

### 标签函数

```js
// 模板字符串前加上标签函数名
let ret = tagFun`${a} + ${b} = ${a + b}`
// 调用时会把间隔的字符串和变量值传入
function tagFun(strings, ...expressions) {
  // strings 为 ${} 分割的字符串数组
  // expressions 为 ${} 中的每个表达式的值
}
```

**用标签函数实现默认字符串拼接功能：**

```js
function noTag(strings, ...expressions) { 
  return strings[0] + expressions.map((e, i) => `${e}${strings[i + 1]}`).join(''); 
}
```

### 原始字符串

```js
console.log('\u00A9')
// 输出 ©

console.log(String.raw`\u00A9`)
// 输出 \u00A9
```

>   注意：调用时没用括号

## Symbol 类型