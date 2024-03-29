---
title: ts中any和unknown有什么区别？
pubDatetime: 2022-03-13T16:00:00.000Z
author: caorushizi
tags:
  - typescript
postSlug: ad0d23bec2dac8b538c2923b00cf5542
description: >-
  unknown和any的主要区别是unknown类型会更加严格：在对unknown类型的值执行大多数操作之前，我们必须进行某种形式的检查。而在对any类型的值执行操作之前，我们不必进行任何检查。举例说
difficulty: 2
questionNumber: 19
source: >-
  https://fe.ecool.fun/topic-answer/ae4d3995-6e26-443a-9f42-a07e594a9bff?orderBy=updateTime&order=desc&tagId=19
---

unknown 和 any 的主要区别是 unknown 类型会更加严格：在对 unknown 类型的值执行大多数操作之前，我们必须进行某种形式的检查。而在对 any 类型的值执行操作之前，我们不必进行任何检查。

举例说明：

```ts
let foo: any = 123;
console.log(foo.msg); // 符合TS的语法
let a_value1: unknown = foo; // OK
let a_value2: any = foo; // OK
let a_value3: string = foo; // OK

let bar: unknown = 222; // OK
console.log(bar.msg); // Error
let k_value1: unknown = bar; // OK
let K_value2: any = bar; // OK
let K_value3: string = bar; // Error
```

因为 bar 是一个未知类型(任何类型的数据都可以赋给 `unknown` 类型)，所以不能确定是否有 msg 属性。不能通过 TS 语法检测；而 unknown 类型的值也不能将值赋给 any 和 unknown 之外的类型变量

## 总结

any 和 unknown 都是顶级类型，但是 unknown 更加严格，不像 any 那样不做类型检查，反而 unknown 因为未知性质，不允许访问属性，不允许赋值给其他有明确类型的变量。
