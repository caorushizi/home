---
title: Promise.all和Promise.allSettled有什么区别？
pubDatetime: 2021-10-18T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: d3260fd8890b1e5075236041d62275b1
description: >-
  一句话概括`Promise.allSettled`和`Promise.all`的最大不同：`Promise.allSettled`永远不会被**reject**。Promise.all的痛点-----
difficulty: 3
questionNumber: 204
source: >-
  https://fe.ecool.fun/topic-answer/4d19c9e2-7a80-40fd-83ee-ae6d9b531a0a?orderBy=updateTime&order=desc&tagId=10
---

一句话概括`Promise.allSettled`和`Promise.all`的最大不同：`Promise.allSettled`永远不会被**reject**。

## Promise.all 的痛点

当需要处理多个 Promise 并行时，大多数情况下 Promise.all 用起来是非常顺手的，比如下面这样

```js
const delay = n => new Promise(resolve => setTimeout(resolve, n));

const promises = [delay(100).then(() => 1), delay(200).then(() => 2)];

Promise.all(promises).then(values => console.log(values));
// 最终输出： [1, 2]
```

可是，是一旦有一个 promise 出现了异常，被 reject 了，情况就会变的麻烦。

```js
const promises = [
  delay(100).then(() => 1),
  delay(200).then(() => 2),
  Promise.reject(3),
];

Promise.all(promises).then(values => console.log(values));
// 最终输出： Uncaught (in promise) 3

Promise.all(promises)
  .then(values => console.log(values))
  .catch(err => console.log(err));
// 加入catch语句后，最终输出：3
```

尽管能用 catch 捕获其中的异常，但你会发现其他执行成功的 Promise 的消息都丢失了，仿佛石沉大海一般。

要么全部成功，要么全部重来，这是 Promise.all 本身的强硬逻辑，也是痛点的来源，不能说它错，但这的确给 Promise.allSettled 留下了立足的空间。

## Promise.allSettled

假如使用 Promise.allSettled 来处理这段逻辑会怎样呢?

```js
const promises = [
  delay(100).then(() => 1),
  delay(200).then(() => 2),
  Promise.reject(3),
];

Promise.allSettled(promises).then(values => console.log(values));
// 最终输出：
//    [
//      {status: "fulfilled", value: 1},
//      {status: "fulfilled", value: 2},
//      {status: "rejected", value: 3},
//    ]
```

可以看到所有 promise 的数据都被包含在 then 语句中，且每个 promise 的返回值多了一个 status 字段，表示当前 promise 的状态，没有任何一个 promise 的信息被丢失。

因此，当用 Promise.allSettled 时，我们只需专注在 then 语句里，当有 promise 被异常打断时，我们依然能妥善处理那些已经成功了的 promise，不必全部重来。
