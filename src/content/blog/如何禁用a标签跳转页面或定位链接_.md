---
title: 如何禁用a标签跳转页面或定位链接?
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: f4ceebaaa352106f20acf6ba4d951ac0
description: >-
  当页面中a标签不需要任何跳转时，从原理上来讲，可分如下两种方法：*标签属性href，使其指向空或不返回任何内容。如：```html<ahref="javascript:void(0);">点此无反应j
difficulty: 2
questionNumber: 56
source: >-
  https://fe.ecool.fun/topic-answer/65fa7d0f-fd68-4c2d-9c2b-4f98d7a4f9e3?orderBy=updateTime&order=desc&tagId=12
---

当页面中 a 标签不需要任何跳转时，从原理上来讲，可分如下两种方法：

- 标签属性 href，使其指向空或不返回任何内容。如：

```html
<a href="javascript:void(0);">点此无反应javascript:void(0)</a>

<a href="javascript:;">点此无反应javascript:</a>
```

- 从标签事件入手，阻止其默认行为。如：

html 方法：

```html
<a href="" onclick="return false;">return false;</a>
<a href="#" onclick="return false;">return false;</a>
```

或者在 js 文件中阻止默认点击事件：

```javascript
Event.preventDefault();
```

还可以在 css 文件中处理点击，不响应任何鼠标事件：

```css
pointer-events: none;
```
