---
title: JavaScript - 常用对象
date: 2021-02-25
category:
  - 前端
  - JavaScript
tag: JavaScript
---

# JavaScript - 常用对象

## 全局

### URI 编码

-   `encodeURI` 不对 URI 关键字符编码
-   `encodeURIComponent` 对所有字符编码

```js
et uri = "http://www.wrox.com/illegal value.js#start";
// "http://www.wrox.com/illegal%20value.js#start"
console.log(encodeURI(uri));
// "http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.js%23start"
console.log(encodeURIComponent(uri));
```

## 日期

## 正则

## 数组

## 定型数组

```js
const buf = new ArrayBuffer(16); // 初始化为0
const v = new DataView(buf);
const ints = new Int32Array(buf)
```

## Map