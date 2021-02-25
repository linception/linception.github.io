---
title: AJAX
date: 2021-02-17
category:
  - 前端
tag: AJAX
---



# AJAX

AJAX 是异步的 JavaScript 和 XML（**A**synchronous **J**avaScript **A**nd **X**ML）。简单点说，就是使用 `XMLHttpRequest` 对象与服务器通信。

## 快速开始

```js
// Old compatibility code, no longer needed.
if (window.XMLHttpRequest) { // Mozilla, Safari, IE7+ ...
    httpRequest = new XMLHttpRequest();
} else if (window.ActiveXObject) { // IE 6 and older
    httpRequest = new ActiveXObject("Microsoft.XMLHTTP");
}
```

## 参考

- [XMLHttpRequest](https://developer.mozilla.org/zh-cn/docs/web/api/xmlhttprequest)

- [什么是AJAX？](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started#什么是ajax？)