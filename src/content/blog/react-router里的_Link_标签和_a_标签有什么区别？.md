---
title: react-router里的<Link>标签和<a>标签有什么区别？
pubDatetime: 2023-03-25T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 4e38b14840ecafc8b74eb42c7f159246
description: >-
  对比<a>标签,Link避免了不必要的重新渲染。react-router是伴随着react框架出现的路由系统，它也是公认的一种优秀的路由解决方案。在使用react-router时候，我们常常会使用其自
difficulty: 3
questionNumber: 15
source: >-
  https://fe.ecool.fun/topic-answer/eb1b05fa-d58b-4d72-bf81-3cd8bab13f55?orderBy=updateTime&order=desc&tagId=13
---

对比 <a> 标签, Link 避免了不必要的重新渲染。

react-router 是伴随着 react 框架出现的路由系统，它也是公认的一种优秀的路由解决方案。在使用 react-router 时候，我们常常会使用其自带的路径跳转组件 Link,通过实现跳转；

react-router 接管了其默认的链接跳转行为，与传统的页面跳转有区别的是，Link 的 **“跳转”** 行为只会触发相匹配的对应的页面内容更新，而不会刷新整个页面。

Link 跳转做了三件事情：

- 有 onclick 那就执行 onclick
- click 的时候阻止 a 标签默认事件
- 根据跳转 href，用 history 跳转，此时只是链接变了，并没有刷新页面

而 a 标签就是普通的超链接了，用于从当前页面跳转到 href 指向的另一个页面（非锚点情况）。
