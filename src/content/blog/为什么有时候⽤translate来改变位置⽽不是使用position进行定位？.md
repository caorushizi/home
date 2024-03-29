---
title: 为什么有时候⽤translate来改变位置⽽不是使用position进行定位？
pubDatetime: 2022-06-24T16:00:00.000Z
author: caorushizi
tags:
  - css
postSlug: 05479225b80e6d004802a02a82eba39d
description: >-
  translate是transform属性的⼀个值。改变transform或opacity不会触发浏览器重新布局（reflow）或重绘（repaint），只会触发复合（compositions）。⽽改
difficulty: 1.5
questionNumber: 22
source: >-
  https://fe.ecool.fun/topic-answer/98cd24a6-d666-4ddd-a696-f74fbe1552a1?orderBy=updateTime&order=desc&tagId=11
---

translate 是 transform 属性的⼀个值。

改变 transform 或 opacity 不会触发浏览器重新布局（reflow）或重绘（repaint），只会触发复合（compositions）。

⽽改变绝对定位会触发重新布局，进⽽触发重绘和复合。

transform 使浏览器为元素创建⼀个 GPU 图层，但改变绝对定位会使⽤到 CPU。

因此 translate()更⾼效，可以缩短平滑动画的绘制时间。

⽽ translate 改变位置时，元素依然会占据其原始空间，绝对定位就不会发⽣这种情况。

具体的原理可查看 [【前端基础系列】CSS 篇-带你搞懂“硬件加速”](https://mp.weixin.qq.com/s?__biz=Mzk0NTI2NDgxNQ==&mid=2247484939&idx=1&sn=229467c549cec5e3980671f488a4d89e&chksm=c31947cbf46ecedd13f930b44e9bc2a25ce706a8d30fce56c54584598015640338a6e075b8ff#rd)
