---
title: 解释下如下代码的意图：Array.prototype.slice.apply(arguments)
pubDatetime: 2021-12-26T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: d89abb1d1b461d3bfbe8fff34feaec10
description: >-
  arguments为类数组对象，并不是真正的数组。slice可以实现数组的浅拷贝。由于arguments不是真正的数组，所以没有slice方法，通过apply可以调用数组对象的slice方法，从而将a
difficulty: 1
questionNumber: 183
source: >-
  https://fe.ecool.fun/topic-answer/d0625555-2b53-4edc-bf3f-2721eaf7af55?orderBy=updateTime&order=desc&tagId=10
---

arguments 为类数组对象，并不是真正的数组。

slice 可以实现数组的浅拷贝。

由于 arguments 不是真正的数组，所以没有 slice 方法，通过 apply 可以调用数组对象的 slice 方法，从而将 arguments 类数组转换为数组。
