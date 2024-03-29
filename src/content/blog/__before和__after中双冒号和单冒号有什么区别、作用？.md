---
title: "::before和::after中双冒号和单冒号有什么区别、作用？"
pubDatetime: 2023-04-02T16:00:00.000Z
author: caorushizi
tags:
  - css
postSlug: 640cc31e2eee0339013d2e1593f61139
description: >-
  在CSS中伪类一直用:表示，如:hover,:active等伪元素在CSS1中已存在，当时语法是用`:`表示，如`:before`和`:after`后来在CSS3中修订，伪元素用`::`表示，如`::
difficulty: 1
questionNumber: 8
source: >-
  https://fe.ecool.fun/topic-answer/77778585-d890-4a84-9d69-4a9042f571d7?orderBy=updateTime&order=desc&tagId=11
---

在 CSS 中伪类一直用 : 表示，如 :hover, :active 等

伪元素在 CSS1 中已存在，当时语法是用 `:` 表示，如 `:before` 和 `:after`

后来在 CSS3 中修订，伪元素用 `::` 表示，如 `::before` 和 `::after`，以此区分伪元素和伪类

由于低版本 IE 对双冒号不兼容，开发者为了兼容性各浏览器，可以继续使用 `:after` 这种老语法表示伪元素

- 单冒号（:）用于 css3 的伪类
- 双冒号（::）用于 css3 的伪元素

作用：`::before` 和 `::after` 的主要作用是在元素内容前后加上指定内容。

另外，伪类与伪元素的区别有：

- 伪类与伪元素都是用于向选择器加特殊效果
- 伪类与伪元素的本质区别就是是否抽象创造了新元素
- 伪类只要不是互斥可以叠加使用
- 伪元素在一个选择器中只能出现一次，并且只能出现在末尾
- 伪类与伪元素优先级分别与类、标签优先级相同
