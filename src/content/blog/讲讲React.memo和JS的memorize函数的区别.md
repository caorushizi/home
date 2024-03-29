---
title: 讲讲React.memo和JS的memorize函数的区别
pubDatetime: 2023-05-27T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 7853207430b5884e81d3b00a663d9afd
description: >-
  React.memo()和JS的memorize函数都是用来对函数进行结果缓存，提高函数的性能表现。不过，它们之间还是有一些区别的：1.**适用范围不同**：React.memo()主要适用于优化Re
difficulty: 3
questionNumber: 6
source: >-
  https://fe.ecool.fun/topic-answer/9491596e-4423-4426-b300-a31ded121bc1?orderBy=updateTime&order=desc&tagId=13
---

React.memo() 和 JS 的 memorize 函数都是用来对函数进行结果缓存，提高函数的性能表现。不过，它们之间还是有一些区别的：

1.  **适用范围不同**：React.memo() 主要适用于优化 React 组件的性能表现，而 memorize 函数可以用于任何 JavaScript 函数的结果缓存。
2.  **实现方式不同**：React.memo() 是一个 React 高阶组件（HOC），通过浅层比较 props 是否发生变化来决定是否重新渲染组件。而 memorize 函数则是通过将函数的输入参数及其计算结果保存到一个缓存对象中，以避免重复计算相同的结果。
3.  **缓存策略不同**：React.memo() 的缓存策略是浅比较（shallow compare），只比较 props 的第一层属性值是否相等，不会递归比较深层嵌套对象或数组的内容。而 memorize 函数的缓存策略是将输入参数转换成字符串后，作为缓存的键值。如果传入的参数不是基本类型时，则需要自己实现缓存键值的计算。
4.  **应用场景不同**：React.memo() 主要适用于对不经常变化的组件进行性能优化，而 memorize 函数则主要适用于对计算量大、执行时间长的函数进行结果缓存。例如，对于状态不变的组件或纯函数，可以使用 React.memo() 进行优化；对于递归计算、复杂数学运算等耗时操作，可以使用 memorize 函数进行结果缓存。

综上所述，React.memo() 和 JS 的 memorize 函数虽然都是用于提高函数的性能表现，但其适用范围、实现方式、缓存策略和应用场景等方面还是有一定的区别。开发者需要根据具体情况来选择合适的性能优化手段，以提高应用程序的性能和响应速度。
