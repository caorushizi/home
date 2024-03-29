---
title: 说说你对new.target的理解
pubDatetime: 2022-06-24T16:00:00.000Z
author: caorushizi
tags:
  - es6
postSlug: b97ca386d42ede6cedf4a73b623b606c
description: >-
  `new.target`属性允许你检测函数或构造方法是否是通过new运算符被调用的。在通过new运算符被初始化的函数或构造方法中，`new.target`返回一个指向构造方法或函数的引用。在普通的函数
difficulty: 1
questionNumber: 10
source: >-
  https://fe.ecool.fun/topic-answer/838b4eda-1f58-4215-9bb5-3e59db973286?orderBy=updateTime&order=desc&tagId=24
---

`new.target`属性允许你检测函数或构造方法是否是通过 new 运算符被调用的。

在通过 new 运算符被初始化的函数或构造方法中，`new.target`返回一个指向构造方法或函数的引用。在普通的函数调用中，`new.target` 的值是 undefined。

我们可以使用它来检测，一个函数是否是作为构造函数通过 new 被调用的。

```js
function Foo() {
  if (!new.target) throw "Foo() must be called with new";
  console.log("Foo instantiated with new");
}

Foo(); // throws "Foo() must be called with new"
new Foo(); // logs "Foo instantiated with new"
```
