---
title: 使用Promise实现红绿灯交替重复亮
pubDatetime: 2022-01-09T16:00:00.000Z
author: caorushizi
tags:
  - 编程题
postSlug: 11a8c1779775f6fab4293b6c04eceba0
description: >-
  红灯3秒亮一次，黄灯2秒亮一次，绿灯1秒亮一次；如何让三个灯不断交替重复亮灯？要求：用Promise实现三个亮灯函数已经存在：```jsfunctionred(){console.log('red')
difficulty: 4
questionNumber: 49
source: >-
  https://fe.ecool.fun/topic-answer/446d36f9-0845-432d-957a-7a9a2997a276?orderBy=updateTime&order=desc&tagId=26
---

红灯 3 秒亮一次，黄灯 2 秒亮一次，绿灯 1 秒亮一次；如何让三个灯不断交替重复亮灯？

要求：用 Promise 实现

三个亮灯函数已经存在：

```js
function red() {
  console.log("red");
}
function green() {
  console.log("green");
}
function yellow() {
  console.log("yellow");
}
```
