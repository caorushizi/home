---
title: 谈谈对babel-polyfill的了解
pubDatetime: 2021-07-10T16:00:00.000Z
author: caorushizi
tags:
  - 工具
postSlug: 0e79d665ee5b7d7a6e85d0bd60f1ddee
description: >-
  babelpolyfill有三种：*babel-polyfill*babel-runtime*babel-plugin-transform-runtimebabel-polyfill---------
difficulty: 3
questionNumber: 19
source: >-
  https://fe.ecool.fun/topic-answer/ffbc34ea-c928-4f17-b469-322b3c8be7be?orderBy=updateTime&order=desc&tagId=29
---

babel polyfill 有三种：

- babel-polyfill
- babel-runtime
- babel-plugin-transform-runtime

## babel-polyfill

babel-polyfill 通过向全局对象和内置对象的 prototype 上添加方法来实现的。所以这会造成全局空间污染。

babel-polyfill 使用的两种方式：

- webpack.config.js 中：

配置 webpack.config.js 里的 entry 设置为 entry: \['babel-polyfill',path.join(\_\_dirname, 'index.js')\]

- 业务 js 中：

在 webpack.config.js 配置的主入口 index.js 文件的最顶层键入

```js
import "babel-polyfill";
```

两者打印出来的大小都是一样的，打包后大小是 280KB，如果没有使用 babel-polyfill，大小是 3.43kb。

两则相差大概 81.6 倍。原因是 webpack 把 babel-polyfill 整体全部都打包进去了。而 babel-polyfill 肯定也实现了所有 ES6 新 API 的垫片,文件一定不会小。

那么有没有一种办法,根据实际代码中用到的 ES6 新增 API ,来使用对应的垫片,而不是全部加载进去呢?

是的，有的。那就是 `babel-runtime & babel-plugin-transform-runtime`，他们可以实现按需加载。

## babel-runtime

简单说 babel-runtime 更像是一种按需加载的实现，比如你哪里需要使用 Promise，只要在这个文件头部

```js
import Promise from "babel-runtime/core-js/promise";
```

就行了。

不过如果你许多文件都要使用 Promise，难道每个文件都要 import 一下吗？当然不是，Babel 官方已考虑这种情况，只需要使用 babel-plugin-transform-runtime 就可以解决手动 import 的苦恼了。

## babel-plugin-transform-runtime

babel-plugin-transform-runtime 装了就不需要装 babel-runtime 了，因为前者依赖后者。 总的来说，babel-plugin-transform-runtime 就是可以在我们使用新 API 时 自动 import babel-runtime 里面的 polyfill，具体插件做了以下三件事情：

- 当我们使用 async/await 时，自动引入 babel-runtime/regenerator
- 当我们使用 ES6 的静态事件或内置对象时，自动引入 babel-runtime/core-js
- 移除内联 babel helpers 并替换使用 babel-runtime/helpers 来替换

babel-plugin-transform-runtime 优点：

- 不会污染全局变量
- 多次使用只会打包一次
- 依赖统一按需引入,无重复引入,无多余引入
- 避免 babel 编译的工具函数在每个模块里重复出现，减小库和工具包的体积

使用方式：

在 .babelrc 中配置：

    plugins: ["tranform-runtime"]

打包后大小为 17.4kb，比之前的 280kb 要小很多。
