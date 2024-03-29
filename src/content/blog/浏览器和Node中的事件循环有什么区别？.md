---
title: 浏览器和Node中的事件循环有什么区别？
pubDatetime: 2021-08-08T16:00:00.000Z
author: caorushizi
tags:
  - nodejs
postSlug: d3584717d7bc4397b32b1edbf2c9cb7b
description: >-
  浏览器---关于微任务和宏任务在浏览器的执行顺序是这样的：*执行一只task（宏任务）*执行完micro-task队列（微任务）如此循环往复下去常见的task（宏任务）比如：setTimeout、se
difficulty: 3.5
questionNumber: 10
source: >-
  https://fe.ecool.fun/topic-answer/12240b0e-e285-422e-b6ac-b1e839af6cae?orderBy=updateTime&order=desc&tagId=18
---

## 浏览器

关于微任务和宏任务在浏览器的执行顺序是这样的：

- 执行一只 task（宏任务）
- 执行完 micro-task 队列 （微任务）

如此循环往复下去

常见的 task（宏任务） 比如：setTimeout、setInterval、script（整体代码）、 I/O 操作、UI 渲染等。 常见的 micro-task 比如: new Promise().then(回调)、MutationObserver(html5 新特性) 等。

## Node

Node 的事件循环是 libuv 实现的，引用一张官网的图：

![](https://i.loli.net/2021/08/07/g47eAhQN85sRBmS.png)

预览

大体的 task（宏任务）执行顺序是这样的：

- timers 定时器：本阶段执行已经安排的 setTimeout() 和 setInterval() 的回调函数。
- pending callbacks 待定回调：执行延迟到下一个循环迭代的 I/O 回调。
- idle, prepare：仅系统内部使用。
- poll 轮询：检索新的 I/O 事件;执行与 I/O 相关的回调（几乎所有情况下，除了关闭的回调函数，它们由计时器和
- setImmediate() 排定的之外），其余情况 node 将在此处阻塞。
- check 检测：setImmediate() 回调函数在这里执行。
- close callbacks 关闭的回调函数：一些准备关闭的回调函数，如：socket.on('close', ...)。

微任务和宏任务在 Node 的执行顺序

Node 10 以前：

- 执行完一个阶段的所有任务
- 执行完 nextTick 队列里面的内容
- 然后执行完微任务队列的内容

Node 11 以后： 和浏览器的行为统一了，都是每执行一个宏任务就执行完微任务队列。
