---
title: 浏览器是如何对HTML5的离线储存资源进行管理和加载？
pubDatetime: 2022-06-24T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: ec17714e1bbe8872979e4e8c1f4134ec
description: >-
  ***在线的情况下**，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问页面，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如
difficulty: 1.5
questionNumber: 26
source: >-
  https://fe.ecool.fun/topic-answer/93ffefee-3471-48a5-b60c-1b7adf8edf13?orderBy=updateTime&order=desc&tagId=12
---

- **在线的情况下**，浏览器发现 html 头部有 manifest 属性，它会请求 manifest 文件，如果是第一次访问页面 ，那么浏览器就会根据 manifest 文件的内容下载相应的资源并且进行离线存储。如果已经访问过页面并且资源已经进行离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的 manifest 文件与旧的 manifest 文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，就会重新下载文件中的资源并进行离线存储。
- **离线的情况下**，浏览器会直接使用离线存储的资源。
