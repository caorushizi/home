---
title: 什么是let的临时性死区？
pubDatetime: 2021-07-11T16:00:00.000Z
author: caorushizi
tags:
  - es6
postSlug: a38319b25c26b8fd2c54fe7819462ed0
description: >-
  let会产生临时性死区，在当前的执行上下文中，会进行变量提升，但是未被初始化，所以在执行上下文执行阶段，执行代码如果还没有执行到变量赋值，就引用此变量就会报错，此变量未初始化。
difficulty: 2
questionNumber: 21
source: >-
  https://fe.ecool.fun/topic-answer/769ab8fd-1070-42d3-817e-48d9b37374ff?orderBy=updateTime&order=desc&tagId=24
---

let 会产生临时性死区，在当前的执行上下文中，会进行变量提升，但是未被初始化，所以在执行上下文执行阶段，执行代码如果还没有执行到变量赋值，就引用此变量就会报错，此变量未初始化。
