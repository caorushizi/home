---
title: Node和Element是什么关系？
pubDatetime: 2022-11-13T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: 6ef5ac7b0c69cb6b8948d02051ddc689
description: >-
  Node与Element的关系---------------Node与Element的关系，从继承方面思考可能清晰很多。Element继承于Node，具有Node的方法，同时又拓展了很多自己的特有方法
difficulty: 1
questionNumber: 9
source: >-
  https://fe.ecool.fun/topic-answer/8bf5ed84-131a-405e-9385-0b3b75a42723?orderBy=updateTime&order=desc&tagId=12
---

## Node 与 Element 的关系

Node 与 Element 的关系，从继承方面思考可能清晰很多。

Element 继承于 Node，具有 Node 的方法，同时又拓展了很多自己的特有方法。

在 Element 的一些方法里，是明确区分了 Node 和 Element 的。比如说：childNodes 与 children, parentNode 与 parentElement 等方法。

Node 的一些方法，返回值为 Node，比如说文本节点，注释节点之类的，而 Element 的一些方法，返回值则一定是 Element。

区分清楚这点了，也能避免很多低级问题。

简单的说就是 Node 是一个基类，DOM 中的`Element`，`Text和Comment`都继承于它。换句话说，`Element`，`Text`和`Comment`是三种特殊的 Node，它们分别叫做`ELEMENT_NODE`,`TEXT_NODE`和`COMMENT_NODE`。

所以我们平时使用的 html 上的元素，即`Element`，是类型为`ELEMENT_NODE`的`Node`。
