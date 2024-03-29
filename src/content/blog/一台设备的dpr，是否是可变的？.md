---
title: 一台设备的dpr，是否是可变的？
pubDatetime: 2021-08-22T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: 3166c00f6fd8afc708322b4ee18ba5e7
description: >-
  `devicePixelRatio`，中文名称是设备像素比。这个概念在移动开发的时候会被特别关注，因为它关系到了整个画面的观感、布局甚至是清晰度。在JavaScriptBOM中，它是window全局对
difficulty: 3
questionNumber: 41
source: >-
  https://fe.ecool.fun/topic-answer/8dad4e08-b8b7-4593-bb5e-8df4d4b14499?orderBy=updateTime&order=desc&tagId=12
---

`devicePixelRatio`，中文名称是设备像素比。这个概念在移动开发的时候会被特别关注，因为它关系到了整个画面的观感、布局甚至是清晰度。在 JavaScript BOM 中，它是 window 全局对象下的一个属性，它的定义如下：

> dpr = 设备像素 / CSS 像素

也有文章把设备像素称为物理像素，把 CSS 像素称为独立像素（DIPs），但所指的都是同样概念：

(1) 首先说设备像素。举手机的例子来说，设备像素也就是在手机广告上经常会看到的 1920_1080 像素或 1280_720 像素，也就是常说的分辨率为 1080p 或 720p。它所指的是设备上有多少个能够显示一种特定颜色的最小区域，在任何设备中这个数值都是不会变的。

(2) 再说 CSS 像素，它的一种更广义的叫法是独立像素。CSS 像素是为 web 开发者所打造的，是在 CSS 和 JavaScript 中使用的一个抽象的层，我们在 CSS 中定义的 width: 100px;、font-size: 16px;等属性都是指 CSS 像素。而相对于 CSS 像素，设备像素这个概念在前端中几乎用不上（除了 screen.width/height）。

那么，从定义来看，dpr 的意义就是：在一个设备（的每个方向）上，每个 CSS 像素会被多少个实际的物理像素来显示。

![](https://i.loli.net/2021/08/15/nD9KeYyGqO6tk7b.png)

预览

上图中，一个蓝色方块代表一个设备像素，一个黄色方块代表一个 CSS 像素。我们可以通过这张图来理清 dpr 的概念：

- 如图左，一个设备像素覆盖了多个 CSS 像素，dpr < 1，对应用户的缩小操作；
- 如图右，一个 CSS 像素覆盖了多个设备像素，dpr > 1，对应用户的放大操作。

由于**用户的缩放操作会改变 dpr**，所以设备 dpr 是在默认缩放为 100%的情况下定义的。
