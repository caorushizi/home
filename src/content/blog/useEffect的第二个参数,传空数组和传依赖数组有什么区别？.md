---
title: useEffect的第二个参数,传空数组和传依赖数组有什么区别？
pubDatetime: 2023-05-29T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 029419c74e972bb9d6d7665480b49f3a
description: >-
  在React中，useEffect是一个常用的Hook，它用于处理组件生命周期中的副作用。useEffect接收两个参数，第一个是要执行的函数，第二个是依赖数组（可选）。当传递空数组\[\]时，use
difficulty: 1
questionNumber: 4
source: >-
  https://fe.ecool.fun/topic-answer/c17d0549-bd85-4202-81d1-8f28db624e5f?orderBy=updateTime&order=desc&tagId=13
---

在 React 中，useEffect 是一个常用的 Hook，它用于处理组件生命周期中的副作用。

useEffect 接收两个参数，第一个是要执行的函数，第二个是依赖数组（可选）。

当传递空数组 \[\] 时，useEffect 只会在组件挂载和卸载时调用一次。这种情况下，useEffect 不会监听任何变量，并且不会对组件进行重新渲染。

```js
useEffect(() => {
  // 只在挂载和卸载时执行
}, []);
```

当传递依赖数组时，useEffect 会在组件挂载和依赖项更新时调用。当依赖项中的任何一个值发生变化时，useEffect 都将被重新调用。如果依赖数组为空，则每次组件重新渲染时都会调用 useEffect。

```js
useEffect(() => {
  // 在挂载、依赖列表变化及卸载时执行
}, [dep1, dep2]);
```

下面是这两种情况的总结：

- 当传递空数组 \[\] 时，useEffect 只会在组件挂载和卸载时调用一次，不会对组件进行重新渲染。
- 当传递依赖数组时，useEffect 会在组件挂载和依赖项更新时调用，每次更新时都会检查依赖项列表是否有变化，如果有变化则重新执行。

如果 useEffect 中使用了闭包函数，则应该确保所有引用的变量都在依赖项中被显示声明，否则可能会导致不必要的重新渲染或者无法获取最新的状态。
