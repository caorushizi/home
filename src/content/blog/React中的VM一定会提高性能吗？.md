---
title: React中的VM一定会提高性能吗？
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 960a7d4200d4483da7bba50a0ed1e962
description: >-
  不一定，因为VM只是通过diff算法避免了一些不需要变更的DOM操作，最终还是要操作DOM的，并且diff的过程也是有成本的。对于某些场景，比如都是需要变更DOM的操作，因为VM还会有额外的diff算
difficulty: 2
questionNumber: 81
source: >-
  https://fe.ecool.fun/topic-answer/99fc6f13-b239-4697-8b20-5fdb03702be6?orderBy=updateTime&order=desc&tagId=13
---

不一定，因为 VM 只是通过 diff 算法避免了一些不需要变更的 DOM 操作，最终还是要操作 DOM 的，并且 diff 的过程也是有成本的。

对于某些场景，比如都是需要变更 DOM 的操作，因为 VM 还会有额外的 diff 算法的成本在里面，所以 VM 的方式并不会提高性能，甚至比原生 DOM 要慢。

但是正如尤大大说的，这是一个性能 vs 可维护性的取舍。

框架的意义在于为你掩盖底层的 DOM 操作，让你用更声明式的方式来描述你的目的，从而让你的代码更容易维护。

没有任何框架可以比纯手动的优化 DOM 操作更快，因为框架的 DOM 操作层需要应对任何上层 API 可能产生的操作，它的实现必须是普适的。

针对任何一个 benchmark，都可以写出比任何框架更快的手动优化，但是那有什么意义呢？在构建一个实际应用的时候，出于可维护性的考虑，不可能在每一个地方都去做手动优化。
