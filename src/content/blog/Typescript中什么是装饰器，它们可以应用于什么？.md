---
title: Typescript中什么是装饰器，它们可以应用于什么？
pubDatetime: 2021-07-10T16:00:00.000Z
author: caorushizi
tags:
  - typescript
postSlug: 1d0a5bd0f4e4dee572093d1d10cb7171
description: >-
  装饰器是一种特殊的声明，它允许你通过使用@<name>注释标记来一次性修改类或类成员。每个装饰器都必须引用一个将在运行时评估的函数。例如，装饰器@sealed将对应于sealed函数。任何标有的@se
difficulty: 1
questionNumber: 42
source: >-
  https://fe.ecool.fun/topic-answer/58972e2f-584c-4073-af2a-f6b0c81f447d?orderBy=updateTime&order=desc&tagId=19
---

装饰器是一种特殊的声明，它允许你通过使用@<name>注释标记来一次性修改类或类成员。每个装饰器都必须引用一个将在运行时评估的函数。

例如，装饰器@sealed 将对应于 sealed 函数。任何标有 的@sealed 都将用于评估 sealed 函数。

    function sealed(target) {
      // do something with 'target' ...
    }

它们可以附加到：

- 类声明
- 方法
- 配件
- 特性
- 参数

注意：默认情况下不启用装饰器。要启用它们，你必须`experimentalDecorators从tsconfig.json`文件或命令行编辑编译器选项中的字段。
