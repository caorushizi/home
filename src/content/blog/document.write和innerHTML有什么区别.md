---
title: document.write和innerHTML有什么区别
pubDatetime: 2021-09-25T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 3dcf6a21a462d6412c8037ff500b817f
description: >-
  *document.write是直接写入到页面的内容流，如果在写之前没有调用document.open,浏览器会自动调用open。每次写完关闭之后重新调用该函数，会导致页面被重写。*innerHTML
difficulty: 0.5
questionNumber: 212
source: >-
  https://fe.ecool.fun/topic-answer/1b0c8f90-9f1a-42bf-bd5a-d9efaf0d74eb?orderBy=updateTime&order=desc&tagId=10
---

- document.write 是直接写入到页面的内容流，如果在写之前没有调用 document.open, 浏览器会自动调用 open。每次写完关闭之后重新调用该函数，会导致页面被重写。
- innerHTML 则是 DOM 页面元素的一个属性，代表该元素的 html 内容。你可以精确到某一个具体的元素来进行更改。如果想修改 document 的内容，则需要修改 document.documentElement.innerElement。
- innerHTML 将内容写入某个 DOM 节点，不会导致页面全部重绘
- innerHTML 很多情况下都优于 document.write，其原因在于其允许更精确的控制要刷新页面的那一个部分。
