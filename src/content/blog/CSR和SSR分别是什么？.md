---
title: CSR和SSR分别是什么？
pubDatetime: 2021-07-10T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 494668154faf96ee0ea9f7135e689916
description: >-
  对于html的加载，以React为例，我们习惯的做法是加载js文件中的React代码，去生成页面渲染，同时，js也完成页面交互事件的绑定，这样的一个过程就是CSR（客户端渲染）。但如果这个js文件比较
difficulty: 3
questionNumber: 264
source: >-
  https://fe.ecool.fun/topic-answer/c50852c5-6471-4bd3-8392-02ab58e4c726?orderBy=updateTime&order=desc&tagId=10
---

对于 html 的加载，以 React 为例，我们习惯的做法是加载 js 文件中的 React 代码，去生成页面渲染，同时，js 也完成页面交互事件的绑定，这样的一个过程就是 CSR（客户端渲染）。

但如果这个 js 文件比较大的话，加载起来就会比较慢，到达页面渲染的时间就会比较长，导致首屏白屏。这时候，SSR（服务端渲染）就出来了：由服务端直接生成 html 内容返回给浏览器渲染首屏内容。

但是服务端渲染的页面交互能力有限，如果要实现复杂交互，还是要通过引入 js 文件来辅助实现，我们把页面的展示内容和交互写在一起，让代码执行两次，这种方式就叫同构。

CSR 和 SSR 的区别在于，最终的 html 代码是从客户端添加的还是从服务端。
