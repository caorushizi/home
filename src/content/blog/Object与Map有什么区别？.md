---
title: Object与Map有什么区别？
pubDatetime: 2022-10-29T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 8e852d09e6118348f75edada8f4abbf5
description: >-
  ###概念*Object在ECMAScript中，`Object`是一个特殊的对象。它本身是一个顶级对象，同时还是一个构造函数，可以通过它（如：`newObject()`）来创建一个对象。我们可以认为
difficulty: 1
questionNumber: 62
source: >-
  https://fe.ecool.fun/topic-answer/7621c335-6645-4da0-bd71-cb81fe106f8f?orderBy=updateTime&order=desc&tagId=10
---

### 概念

- Object

在 ECMAScript 中，`Object`是一个特殊的对象。它本身是一个顶级对象，同时还是一个构造函数，可以通过它（如：`new Object()`）来创建一个对象。我们可以认为 JavaScript 中所有的对象都是`Object`的一个实例，对象可以用字面量的方法 const obj = {}即可声明。

- Map

`Object`本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键，这给它的使用带来了很大的限制。

为了解决这个问题，`ES6` 提供了 `Map` 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 `Hash` 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

通过 `const m = new Map();` 即可得到一个 map 实例。

### 访问

map: 通过 map.get(key)方法去属性, 不存在则返回 undefined

object: 通过 obj.a 或者 obj\['a'\]去访问一个属性, 不存在则返回 undefined

### 赋值

map: 通过 map.set 去设置一个值，key 可以是任意类型

object: 通过 object.a = 1 或者 object\['a'\] = 1，去赋值，key 只能是字符串，数字或 symbol

### 删除

map: 通过 map.delete 去删除一个值，试图删除一个不存在的属性会返回 false

object: 通过 delete 操作符才能删除对象的一个属性，诡异的是，即使对象不存在该属性，删除也返回 true，当然可以通过**Reflect.deleteProperty(target, prop)** 删除不存在的属性还是会返回 true。

    var obj = {}; // undefined
    delete obj.a // true

### 大小

map: 通过 map.size 即可快速获取到内部元素的总个数

object: 需要通过 Object.keys 的转换才能将其转换为数组，再通过数组的 length 方法去获得或者使用 Reflect.ownKeys(obj)也可以获取到 keys 的集合

### 迭代

map: 拥有迭代器，可以通过`for-of`、`forEach`去直接迭代元素，而且遍历顺序是确定的

object: 并没有实现迭代器，需要自行实现，不实现只能通过 for-in 循环去迭代，遍历顺序是不确定的

### 使用场景

1.  如果只需要简单的存储 key-value 的数据，并且 key 不需要存储复杂类型的，直接用对象
2.  如果该对象必须通过 JSON 转换的，则只能用对象，目前暂不支持 Map
3.  map 的阅读性更好，所有操作都是通过 api 形式去调用，更有编程体验
