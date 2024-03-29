---
title: 导致JavaScript中this指向混乱的原因是什么?
pubDatetime: 2023-06-03T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: f51405623dd50a45f39527a2a0399a61
description: >-
  在JavaScript中，this关键字的指向通常是动态的，而不是静态的。这意味着this可以根据上下文环境的变化而发生改变，导致它的指向变得混乱或难以预测。常见的导致this指向混乱的原因包括以下几
difficulty: 2
questionNumber: 6
source: >-
  https://fe.ecool.fun/topic-answer/dbf9172e-1193-44cb-a534-3c16ae07de2d?orderBy=updateTime&order=desc&tagId=10
---

在 JavaScript 中，this 关键字的指向通常是动态的，而不是静态的。这意味着 this 可以根据上下文环境的变化而发生改变，导致它的指向变得混乱或难以预测。常见的导致 this 指向混乱的原因包括以下几个方面：

1.  函数调用方式不同：当一个函数被调用时，它的 this 值取决于调用方式。如果使用普通函数调用方式（如 func()），则 this 会指向全局对象 window；如果使用方法调用方式（如 obj.func()），则 this 会指向调用该方法的对象。
2.  箭头函数的使用：箭头函数不具有自己的 this 值，它会捕获上下文中的 this 值。因此，如果在箭头函数中访问 this，它将引用外层作用域中的 this 值。
3.  使用 apply、call 和 bind 方法：apply、call 和 bind 方法可以改变函数执行时的 this 值。其中，apply 和 call 方法可以立即执行函数并传入参数，而 bind 方法可以返回一个新函数，该函数的 this 值被绑定到指定的对象上。
4.  DOM 事件处理程序的使用：在处理 DOM 事件时，浏览器会将事件处理程序内部的 this 指向触发事件的元素。但是，在使用 addEventListener 方法绑定事件处理程序时，this 会指向全局对象 window，而不是目标元素。
5.  对象的嵌套和继承：当一个对象被嵌套在另一个对象中或者使用继承时，this 的指向可能会变得混乱。这是因为 this 的指向取决于函数被调用时的上下文环境，而不是对象本身。因此，在嵌套对象或继承类中使用 this 时，需要特别注意它的指向。

> 面试题由“前端面试题宝典”（官网： [https://fe.cool.cun](https://fe.cool.cun) ）整理维护，如果您在其他小程序中使用，请向小助手（微信号：interview-fe）反馈。
