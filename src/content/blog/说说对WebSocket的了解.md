---
title: 说说对WebSocket的了解
pubDatetime: 2021-07-11T16:00:00.000Z
author: caorushizi
tags:
  - 计算机网络
postSlug: c6f7d41a30ddce3e29f8acb57fa0e6b6
description: >-
  什么是WebSocket------------HTML5开始提供的一种浏览器与服务器进行全双工通讯的网络技术，属于应用层协议。它基于TCP传输协议，并复用HTTP的握手通道。优点--说到优点，这里的
difficulty: 2.5
questionNumber: 47
source: >-
  https://fe.ecool.fun/topic-answer/4449a399-c20d-49e7-aac6-05236ee28662?orderBy=updateTime&order=desc&tagId=16
---

## 什么是 WebSocket

HTML5 开始提供的一种浏览器与服务器进行全双工通讯的网络技术，属于应用层协议。它基于 TCP 传输协议，并复用 HTTP 的握手通道。

## 优点

说到优点，这里的对比参照物是 HTTP 协议，概括地说就是：支持双向通信，更灵活，更高效，可扩展性更好。

- 支持双向通信，实时性更强。
- 更好的二进制支持。
- 较少的控制开销。连接创建后，ws 客户端、服务端进行数据交换时，协议控制的数据包头部较小。在不包含头部的情况下，服务端到客户端的包头只有 2~10 字节（取决于数据包长度），客户端到服务端的的话，需要加上额外的 4 字节的掩码。而 HTTP 协议每次通信都需要携带完整的头部。
- 支持扩展。ws 协议定义了扩展，用户可以扩展协议，或者实现自定义的子协议。（比如支持自定义压缩算法等）
