---
title: 我现在有一个canvas，上面随机布着一些黑块，请实现方法，计算canvas上有多少个黑块。
pubDatetime: 2022-03-08T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 189e9b29d972dc9dba3709907a1911e2
description: >-
  这一题可以转化成图的联通分量问题。通过getImageData获得像素数组，从头到尾遍历一遍，就可以判断每个像素是否是黑色。同时，准备一个width\*height大小的二维数组，这个数组的每个元素是
difficulty: 3
questionNumber: 132
source: >-
  https://fe.ecool.fun/topic-answer/b866f9eb-e02a-4220-b35a-013db09ce0c2?orderBy=updateTime&order=desc&tagId=10
---

这一题可以转化成图的联通分量问题。通过 getImageData 获得像素数组，从头到尾遍历一遍，就可以判断每个像素是否是黑色。同时，准备一个 width \* height 大小的二维数组，这个数组的每个元素是 1/0。如果是黑色，二维数组对应元素就置 1；否则置 0。

然后问题就被转换成了图的连通分量问题。可以通过深度优先遍历或者并查集来实现。
