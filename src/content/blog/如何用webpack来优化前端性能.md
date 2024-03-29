---
title: 如何用webpack来优化前端性能
pubDatetime: 2021-07-06T16:00:00.000Z
author: caorushizi
tags:
  - 工程化
postSlug: 2f350f22ae1496a66c8d7e04f6e60f00
description: >-
  用webpack优化前端性能是指优化webpack的输出结果，让打包的最终结果在浏览器运行快速高效。*压缩代码:删除多余的代码、注释、简化代码的写法等等方式。可以利用webpack的`UglifyJs
difficulty: 1.5
questionNumber: 25
source: >-
  https://fe.ecool.fun/topic-answer/9211a856-9131-4bb9-b7a3-e876bb528ee7?orderBy=updateTime&order=desc&tagId=28
---

用 webpack 优化前端性能是指优化 webpack 的输出结果，让打包的最终结果在浏览器运行快速高效。

- 压缩代码:删除多余的代码、注释、简化代码的写法等等方式。可以利用 webpack 的`UglifyJsPlugin`和`ParallelUglifyPlugin`来压缩 JS 文件， 利用`cssnano`（css-loader?minimize）来压缩 css

- 利用 CDN 加速: 在构建过程中，将引用的静态资源路径修改为 CDN 上对应的路径。可以利用 webpack 对于`output`参数和各 loader 的`publicPath`参数来修改资源路径
- Tree Shaking: 将代码中永远不会走到的片段删除掉。可以通过在启动 webpack 时追加参数`--optimize-minimize`来实现
- Code Splitting: 将代码按路由维度或者组件分块(chunk),这样做到按需加载,同时可以充分利用浏览器缓存
- 提取公共第三方库: SplitChunksPlugin 插件来进行公共模块抽取,利用浏览器缓存可以长期缓存这些无需频繁变动的公共代码
