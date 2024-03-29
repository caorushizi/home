---
title: css加载会造成阻塞吗？
pubDatetime: 2021-07-10T16:00:00.000Z
author: caorushizi
tags:
  - 性能优化
postSlug: c5675e274d2abd980917ce3f8abd1892
description: >-
  先说下结论：*css加载不会阻塞DOM树的解析*css加载会阻塞DOM树的渲染*css加载会阻塞后面js语句的执行为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以
difficulty: 2.5
questionNumber: 13
source: >-
  https://fe.ecool.fun/topic-answer/fda596ab-16db-41ab-9e81-5a567a373d42?orderBy=updateTime&order=desc&tagId=20
---

先说下结论：

- css 加载不会阻塞 DOM 树的解析
- css 加载会阻塞 DOM 树的渲染
- css 加载会阻塞后面 js 语句的执行

为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高 css 加载速度，比如可以使用以下几种方法:

- 使用 CDN(因为 CDN 会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)
- 对 css 进行压缩(可以用很多打包工具，比如 webpack,gulp 等，也可以通过开启 gzip 压缩)
- 合理的使用缓存(设置 cache-control,expires,以及 E-tag 都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)
- 减少 http 请求数，将多个 css 文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

## 原理解析

浏览器渲染的流程如下：

- HTML 解析文件，生成 DOM Tree，解析 CSS 文件生成 CSSOM Tree
- 将 Dom Tree 和 CSSOM Tree 结合，生成 Render Tree(渲染树)
- 根据 Render Tree 渲染绘制，将像素渲染到屏幕上。

从流程我们可以看出来:

- DOM 解析和 CSS 解析是两个并行的进程，所以这也解释了为什么 CSS 加载不会阻塞 DOM 的解析。
- 然而，由于 Render Tree 是依赖于 DOM Tree 和 CSSOM Tree 的，所以他必须等待到 CSSOM Tree 构建完成，也就是 CSS 资源加载完成(或者 CSS 资源加载失败)后，才能开始渲染。因此，CSS 加载是会阻塞 Dom 的渲染的。
- 由于 js 可能会操作之前的 Dom 节点和 css 样式，因此浏览器会维持 html 中 css 和 js 的顺序。因此，样式表会在后面的 js 执行前先加载执行完毕。所以 css 会阻塞后面 js 的执行。
