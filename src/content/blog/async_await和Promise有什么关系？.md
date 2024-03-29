---
title: async/await和Promise有什么关系？
pubDatetime: 2021-07-11T16:00:00.000Z
author: caorushizi
tags:
  - es6
postSlug: 8efea0d40fda6fdbdfbfcd0c34f4d38a
description: >-
  Promise------->Promise对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）
difficulty: 3
questionNumber: 25
source: >-
  https://fe.ecool.fun/topic-answer/fbcd6444-9c0f-492a-b138-bd205bb4bf1d?orderBy=updateTime&order=desc&tagId=24
---

## Promise

> Promise 对象是一个代理对象（代理一个值），被代理的值在 Promise 对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的 promise 对象

## async/await

es2017 的新语法，async/await 就是 generator + promise 的语法糖

async/await 和 Promise 的关系非常的巧妙，await 必须在 async 内使用，并装饰一个 Promise 对象，async 返回的也是一个 Promise 对象。

async/await 中的 return/throw 会代理自己返回的 Promise 的 resolve/reject，而一个 Promise 的 resolve/reject 会使得 await 得到返回值或抛出异常。

- 如果方法内无 await 节点

  - return 一个字面量则会得到一个{PromiseStatus: resolved}的 Promise。
  - throw 一个 Error 则会得到一个{PromiseStatus: rejected}的 Promise。

- 如果方法内有 await 节点

  - async 会返回一个{PromiseStatus: pending}的 Promise（发生切换，异步等待 Promise 的执行结果）。
  - Promise 的 resolve 会使得 await 的代码节点获得相应的返回结果，并继续向下执行。
  - Promise 的 reject 会使得 await 的代码节点自动抛出相应的异常，终止向下继续执行。
