---
title: 介绍一下treeshaking及其工作原理
pubDatetime: 2021-08-12T16:00:00.000Z
author: caorushizi
tags:
  - 工程化
postSlug: 362fed63dfb5ff99700ff89c06caddbc
description: >-
  >Treeshaking是一种通过清除多余代码方式来优化项目打包体积的技术，专业术语叫Deadcodeelimination。treeshaking如何工作的呢？-------------------
difficulty: 3
questionNumber: 10
source: >-
  https://fe.ecool.fun/topic-answer/c00fbf63-deef-433c-aa48-a10812107b0e?orderBy=updateTime&order=desc&tagId=28
---

> Tree shaking 是一种通过清除多余代码方式来优化项目打包体积的技术，专业术语叫 Dead code elimination。

## tree shaking 如何工作的呢？

虽然 tree shaking 的概念在 1990 就提出了，但直到 ES6 的 `ES6-style` 模块出现后才真正被利用起来。

在 ES6 以前，我们可以使用 CommonJS 引入模块：require()，这种引入是动态的，也意味着我们可以基于条件来导入需要的代码：

```javascript
let dynamicModule;
// 动态导入
if (condition) {
  myDynamicModule = require("foo");
} else {
  myDynamicModule = require("bar");
}
```

但是 CommonJS 规范无法确定在实际运行前需要或者不需要某些模块，所以 CommonJS 不适合 tree-shaking 机制。在 ES6 中，引入了完全静态的导入语法：import。这也意味着下面的导入是不可行的：

```javascript
// 不可行，ES6 的import是完全静态的
if (condition) {
  myDynamicModule = require("foo");
} else {
  myDynamicModule = require("bar");
}
```

我们只能通过导入所有的包后再进行条件获取。如下：

    import foo from "foo";
    import bar from "bar";

    if (condition) {
      // foo.xxxx
    } else {
      // bar.xxx
    }

ES6 的 import 语法可以完美使用 tree shaking，因为可以在代码不运行的情况下就能分析出不需要的代码。

看完上面的分析，你可能还是有点懵，这里我简单做下总结：因为 tree shaking 只能在静态 modules 下工作。ECMAScript 6 模块加载是静态的,因此整个依赖树可以被静态地推导出解析语法树。所以在 ES6 中使用 tree shaking 是非常容易的。

## tree shaking 的原理是什么?

看完上面的分析，相信这里你可以很容易的得出题目的答案了：

- ES6 Module 引入进行静态分析，故而编译的时候正确判断到底加载了那些模块
- 静态分析程序流，判断那些模块和变量未被使用或者引用，进而删除对应代码
