---
title: JS中怎么阻止事件冒泡和默认事件？
pubDatetime: 2021-09-25T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 5d685be8637f6c99803ead3aa49445c0
description: >-
  event.stopPropagation()方法-------------------------这是阻止事件的冒泡方法，不让事件向document上蔓延，但是默认事件任然会执行，当你掉用这个方法的
difficulty: 1
questionNumber: 205
source: >-
  https://fe.ecool.fun/topic-answer/1b65452c-ab0b-41a8-8621-fc25704afa33?orderBy=updateTime&order=desc&tagId=10
---

## event.stopPropagation()方法

这是阻止事件的冒泡方法，不让事件向 document 上蔓延，但是默认事件任然会执行，当你掉用这个方法的时候，如果点击一个连接，这个连接仍然会被打开，

## event.preventDefault()方法

这是阻止默认事件的方法，比如在 a 标签的绑定事件上调用此方法，链接则不会被打开，但是会发生冒泡，冒泡会传递到上一层的父元素；

## return false

这个方法比较暴力，他会同事阻止事件冒泡也会阻止默认事件；写上此代码，连接不会被打开，事件也不会传递到上一层的父元素；可以理解为 return false 就等于同时调用了 event.stopPropagation()和 event.preventDefault()
