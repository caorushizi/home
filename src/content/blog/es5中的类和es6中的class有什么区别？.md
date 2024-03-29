---
title: es5中的类和es6中的class有什么区别？
pubDatetime: 2023-03-03T16:00:00.000Z
author: caorushizi
tags:
  - es6
postSlug: 6dab99d3aba056f61ca5434574e38cfe
description: >-
  在es5中主要是通过构造函数方式和原型方式来定义一个类，在es6中我们可以通过class来定义类。一、class类必须new调用，不能直接执行。-----------------------![](h
difficulty: 3
questionNumber: 8
source: >-
  https://fe.ecool.fun/topic-answer/1036468a-13c7-49d5-af8f-31c31135ceea?orderBy=updateTime&order=desc&tagId=24
---

在 es5 中主要是通过构造函数方式和原型方式来定义一个类，在 es6 中我们可以通过 class 来定义类。

## 一、class 类必须 new 调用，不能直接执行。

![](https://pic.rmb.bdstatic.com/bjh/80a46bd84b6fec579111adb70ea88ad2.png)

预览

class 类执行的话会报错，而 es5 中的类和普通函数并没有本质区别，执行肯定是 ok 的。

## 二、class 类不存在变量提升

![](https://pic.rmb.bdstatic.com/bjh/3e34d40c8d36b35c3149660dc9a727b6.png)

预览

![](https://pic.rmb.bdstatic.com/bjh/1301f1c5a607efe29c7e407b951a50f2.png)

预览

图 2 报错，说明 class 方式没有把类的定义提升到顶部。

## 三、class 类无法遍历它实例原型链上的属性和方法

```js
function Foo(color) {
  this.color = color;
}
Foo.prototype.like = function () {
  console.log(`like${this.color}`);
};
let foo = new Foo();

for (let key in foo) {
  // 原型上的like也被打印出来了
  console.log(key); // color、like
}
```

```js
class Foo {
  constructor(color) {
    this.color = color;
  }
  like() {
    console.log(`like${this.color}`);
  }
}
let foo = new Foo("red");

for (let key in foo) {
  // 只打印一个color,没有打印原型链上的like
  console.log(key); // color
}
```

## 四、new.target 属性

es6 为 new 命令引入了一个 new.target 属性，它会返回 new 命令作用于的那个构造函数。如果不是通过 new 调用或 Reflect.construct()调用的，new.target 会返回 undefined

```js
function Person(name) {
  if (new.target === Person) {
    this.name = name;
  } else {
    throw new Error("必须使用 new 命令生成实例");
  }
}

let obj = {};
Person.call(obj, "red"); // 此时使用非new的调用方式就会报错
```

## 五、class 类有 static 静态方法

static 静态方法只能通过类调用，不会出现在实例上；另外如果静态方法包含 this 关键字，这个 this 指的是类，而不是实例。static 声明的静态属性和方法都不可以被子类继承。

```js
class Foo {
  static bar() {
    this.baz(); // 此处的this指向类
  }
  static baz() {
    console.log("hello"); // 不会出现在实例中
  }
  baz() {
    console.log("world");
  }
}

Foo.bar(); // hello
```
