---
title: CSS预处理器/后处理器是什么？为什么要使用它们？
pubDatetime: 2022-06-24T16:00:00.000Z
author: caorushizi
tags:
  - css
postSlug: 814aa74327e9ade05f433e0bdf93b441
description: >-
  **预处理器，**如：`less`，`sass`，`stylus`，用来预编译`sass`或者`less`，增加了`css`代码的复用性。层级，`mixin`，变量，循环，函数等对编写以及开发UI组件
difficulty: 2
questionNumber: 21
source: >-
  https://fe.ecool.fun/topic-answer/ad2a65d2-9330-4f65-9be7-b61e11e10c02?orderBy=updateTime&order=desc&tagId=11
---

**预处理器，** 如：`less`，`sass`，`stylus`，用来预编译`sass`或者`less`，增加了`css`代码的复用性。层级，`mixin`， 变量，循环， 函数等对编写以及开发 UI 组件都极为方便。

**后处理器，** 如： `postCss`，通常是在完成的样式表中根据`css`规范处理`css`，让其更加有效。目前最常做的是给`css`属性添加浏览器私有前缀，实现跨浏览器兼容性的问题。

`css`预处理器为`css`增加一些编程特性，无需考虑浏览器的兼容问题，可以在`CSS`中使用变量，简单的逻辑程序，函数等在编程语言中的一些基本的性能，可以让`css`更加的简洁，增加适应性以及可读性，可维护性等。

其它`css`预处理器语言：`Sass（Scss）`, `Less`, `Stylus`, `Turbine`, `Swithch css`, `CSS Cacheer`, `DT Css`。

使用原因：

- 结构清晰， 便于扩展
- 可以很方便的屏蔽浏览器私有语法的差异
- 可以轻松实现多重继承
- 完美的兼容了`CSS`代码，可以应用到老项目中
