---
title: 请实现下面的myAll方法
pubDatetime: 2023-03-12T16:00:00.000Z
author: caorushizi
tags:
  - typescript
postSlug: 5016d907f194e4db61253ce728e56f8f
description: >-
  ```ts/***@file实现PromiseAll方法*/import{sleep}from"./8.sleep";asyncfunctionmyAll<Textendsunknown[]|[]>(
difficulty: 1
questionNumber: 9
source: >-
  https://fe.ecool.fun/topic-answer/8694932e-df3f-492f-8ef9-b0e7aa486f2f?orderBy=updateTime&order=desc&tagId=19
---

```ts
/**
 * @file 实现 PromiseAll 方法
 */

import { sleep } from "./8.sleep";

async function myAll<T extends unknown[] | []>(
  values: T
): Promise<{ [P in keyof T]: Awaited<T[P]> }> {
  // 补全此处代码，使用 Promise.all 以外的语法完成
  throw new Error("功能待实现");
}

// 一秒钟后返回结果 value
async function request(value: string) {
  await sleep(1000);
  return value;
}
async function main() {
  console.log("start");
  const res = await myAll([request("a"), request("b"), request("c")]);
  console.log(res); // 预期输出 start 一秒后输出 ['a', 'b', 'c']
}
main();

export default {};
```
