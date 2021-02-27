---
title: JavaScript - 运算符
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 运算符

## 移位

-   `>>` 有符号右移
-   `>>>` 无符号右移

## 没有整除

-   `Math.floor()`

## 指数

-   `**`

## 相等和全等

### 规则

-   如果任一操作数是布尔值，则将其转换为数值再比较是否相等。`false` 转换为 0，`true` 转换为 1
-   如果一个操作数是字符串，另一个操作数是数值，则尝试将字符串转换为数值，再比较是否相等

- 如果一个操作数是对象，另一个操作数不是，则调用对象的 `valueOf()` 方法取得其原始值，再根据前面的规则进行比较

>   `null == undefined`
>
>   `null !=== undefined`

## `for-in` 和 `for-of`

-   `for-in` 遍历键名
-   `for-of` 遍历键值

```js
for (const [idx, element] of array)
```

## `with`

```js
with (location) {
  // location加入到作用域上下文中
}
```

