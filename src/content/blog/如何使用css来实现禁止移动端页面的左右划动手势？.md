---
title: 如何使用css来实现禁止移动端页面的左右划动手势？
pubDatetime: 2021-12-26T16:00:00.000Z
author: caorushizi
tags:
  - css
postSlug: 7b70fa5c0de9cc21ad3b03614741a584
description: >-
  CSS属性`touch-action`用于设置触摸屏用户如何操纵元素的区域(例如，浏览器内置的缩放功能)。最简单方法是：```csshtml{touch-action:none;touch-actio
difficulty: 1
questionNumber: 45
source: >-
  https://fe.ecool.fun/topic-answer/a792448f-bd4c-4320-b3dc-c1dbe395c090?orderBy=updateTime&order=desc&tagId=11
---

CSS 属性 `touch-action` 用于设置触摸屏用户如何操纵元素的区域(例如，浏览器内置的缩放功能)。

最简单方法是：

```css
html {
  touch-action: none;
  touch-action: pan-y;
}
```

还可以直接指定对应元素的宽度和 overflow：

```css
html {
  width: 100vw;
  overflow-x: hidden;
}
```
