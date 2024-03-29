---
title: Canvas和SVG有什么区别？
pubDatetime: 2022-06-24T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: a11c3698310fab8dbd88b90d988a3a97
description: >-
  **（1）SVG：**SVG可缩放矢量图形（ScalableVectorGraphics）是基于可扩展标记语言XML描述的2D图形的语言，SVG基于XML就意味着SVGDOM中的每个元素都是可用的，可
difficulty: 2
questionNumber: 25
source: >-
  https://fe.ecool.fun/topic-answer/c8a51567-945f-461d-b632-0209dd1917f5?orderBy=updateTime&order=desc&tagId=12
---

**（1）SVG：** SVG 可缩放矢量图形（Scalable Vector Graphics）是基于可扩展标记语言 XML 描述的 2D 图形的语言，SVG 基于 XML 就意味着 SVG DOM 中的每个元素都是可用的，可以为某个元素附加 Javascript 事件处理器。在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

其特点如下：

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用

**（2）Canvas：** Canvas 是画布，通过 Javascript 来绘制 2D 图形，是逐像素进行渲染的。其位置发生改变，就会重新进行绘制。

其特点如下：

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

注：矢量图，也称为面向对象的图像或绘图图像，在数学上定义为一系列由线连接的点。矢量文件中的图形元素称为对象。每个对象都是一个自成一体的实体，它具有颜色、形状、轮廓、大小和屏幕位置等属性。
