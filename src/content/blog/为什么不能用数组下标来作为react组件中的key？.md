---
title: 为什么不能用数组下标来作为react组件中的key？
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 83ee4aa865823deb88c87a3dc87c0907
description: >-
  react使用diff算法，使用key来做同级比对。如果使用数组下标作为key，有以下情况：*在数组头部或中部插入或删除元素：所有key对应的节点的值发生更改，进行重新渲染。造成性能损耗*而如果使用数
difficulty: 2
questionNumber: 74
source: >-
  https://fe.ecool.fun/topic-answer/dfc9b600-74ec-4e03-8832-c3d69de4dcea?orderBy=updateTime&order=desc&tagId=13
---

react 使用 diff 算法，使用 key 来做同级比对。如果使用数组下标作为 key，有以下情况：

- 在数组头部或中部插入或删除元素： 所有 key 对应的节点的值发生更改，进行重新渲染。造成性能损耗
- 而如果使用数组中唯一值来作为 key：不管是在何处插入或删除节点，其他 key 对应的节点的值未发生更改，只需插入或删除操作的数组节点。
