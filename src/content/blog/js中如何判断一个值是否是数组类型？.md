---
title: js中如何判断一个值是否是数组类型？
pubDatetime: 2021-09-25T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 54bf20dc8e305dcd4bbd67169dfd7cbe
description: >-
  instanceof----------```jsconstarr=[];arrinstanceofArray;//true```Array.isArray-------------```jscons
difficulty: 1
questionNumber: 207
source: >-
  https://fe.ecool.fun/topic-answer/f53e39b7-9de1-4a49-b95d-6c73591d5512?orderBy=updateTime&order=desc&tagId=10
---

## instanceof

```js
const arr = [];
arr instanceof Array; // true
```

## Array.isArray

```js
const arr = [];
Array.isArray(arr); // true

const obj = {};
Array.isArray(obj); // false
```

## Object.prototype.isPrototypeOf

使用 Object 的原型方法 isPrototypeOf，判断两个对象的原型是否一样, isPrototypeOf() 方法用于测试一个对象是否存在于另一个对象的原型链上。

```js
const arr = [];
Object.prototype.isPrototypeOf(arr, Array.prototype); // true
```

## Object.getPrototypeOf

Object.getPrototypeOf() 方法返回指定对象的原型（内部\[\[Prototype\]\]属性的值）。

```js
const arr = [];
Object.getPrototypeOf(arr) === Array.prototype; // true
```

## Object.prototype.toString

借用 Object 原型的 call 或者 apply 方法，调用 toString()是否为\[object Array\]

```js
const arr = [];
Object.prototype.toString.call(arr) === "[object Array]"; // true

const obj = {};
Object.prototype.toString.call(obj); // "[object Object]"
```
