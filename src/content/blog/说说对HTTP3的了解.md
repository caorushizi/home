---
title: 说说对HTTP3的了解
pubDatetime: 2022-05-15T16:00:00.000Z
author: caorushizi
tags:
  - 计算机网络
postSlug: 6d56bc6fc6a53dabbdac3e0ef7af37e7
description: >-
  HTTP/3的来源---------由于TCP和UDP两者在运输层存在一定差异，TCP的传递效率与UDP相比有天然劣势，于是Google基于UDP开发出了新的协议QUIC(QuickUDPIntern
difficulty: 3
questionNumber: 14
source: >-
  https://fe.ecool.fun/topic-answer/9eebcbe5-2c34-482e-9198-36f750aa3555?orderBy=updateTime&order=desc&tagId=16
---

## HTTP/3 的来源

由于 TCP 和 UDP 两者在运输层存在一定差异，TCP 的传递效率与 UDP 相比有天然劣势，于是 Google 基于 UDP 开发出了新的协议 QUIC(Quick UDP Internet Connections)，希望取代 TCP 提高传输效率，后经过协商将 QUIC 协议更名为 HTTP/3。

## QUIC 概述

TCP、UDP 是我们所熟悉的传输层协议，UDP 比 TCP 相比效率更高但并不具备传输可靠性。而 QUIC 便是看中 UDP 传输效率这一特性，并结合了 TCP、TLS、HTTP/2 的优势，加以优化。

于是在 QUIC 上层的应用层所运行的 HTTP 协议也就被称为 HTTP/3。

**HTTP over QUIC is HTTP/3**

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbbc1e2d3c36~tplv-t2oaga2asx-image.image)

预览

## HTTP/3 新特性

### 1\. **零 RTT 建立连接**

如下图，传统 HTTP/2(所有 HTTP/2 的浏览器均基于 HTTPS)传输数据前需要三次 RTT，即使将第一次 TLS 握手的对称秘钥缓存也需要两次 RTT 才能传递数据。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbbf66cd588c~tplv-t2oaga2asx-image.image)

预览

对于 HTTP/3 而言，仅仅需要一次 RTT 即可传递数据，如果将其缓存，就可将 RTT 减少至零。

其核心就是 DH 秘钥交换算法。

- 客户端向服务端请求数据。
- 服务端生成 g、p、a 三个随机数，用三个随机数生成 A。将 a 保留后，将 g、p、A(Server Config)传递到客户端。
- 客户端生成随机数 b，将 b 保留后，用 g、p、b 三个随机数生成 B。
- 客户端再使用 A、b、p 生成秘钥 K，用 K**加密 HTTP 数据**并与 B 一同发送到服务端。
- 服务端再使用 B、a、p 得到相同秘钥 K，并解密 HTTP 数据。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbc2229ed71a~tplv-t2oaga2asx-image.image)

预览

**至此即可完成一次 RTT 对连接的建立，当缓存 Server Config 后零 RTT 即可进行数据传递。**

### 2\. **连接迁移**

传统连接通过源 IP、源端口、目的 IP、目的端口进行连接，当网络发生更换后连接再次建立时延较长。

HTTP/3 使用 Connection ID 对连接保持，只要 Connection ID 不改变，连接仍可维持。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbd27b55aa2a~tplv-t2oaga2asx-image.image)

预览

### 3\. **队头阻塞/多路复用**

- TCP 作为面向连接的协议，对每次请求序等到 ACK 才可继续连接，一旦中间连接丢失将会产生队头阻塞。
- HTTP/1.1 中提出 Pipelining 的方式，单个 TCP 连接可多次发送请求，但依旧会有中间请求丢失产生阻塞的问题。

  ![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbd51e85a7aa~tplv-t2oaga2asx-image.image)

  预览

- HTTP/2 中将请求粒度减小，通过 Frame 的方式进行请求的发送。但在 TCP 层 Frame 组合得到 Stream 进行传输，一旦出现 Stream 中的 Frame 丢失，其后方的 Stream 都将会被阻塞。

  ![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbd9e7eafa91~tplv-t2oaga2asx-image.image)

  预览

- 对于 HTTP/2 而言，浏览器会默认采取 TLS 方式传输，TLS 基于 Record 组织数据，每个 Record 包含 16K，其中有 12 个 TCP 的包，一旦其中一个 TCP 包出现问题将会导致整个 Record 无法解密。这也是网络环境较差时 HTTP/2 的传输速度比 HTTP/1.1 更慢的原因。

  ![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbe4245b0e20~tplv-t2oaga2asx-image.image)

  预览

- HTTP/3 基于 UDP 的传输，不保证连接可靠性，也就没有对头阻塞的后果。同样传输单元与加密单元为 Packet，在 TLS 下也可避免对头阻塞的问题。

### 4\. **拥塞控制**

- 热拔插：TCP 对于拥塞控制在于传输层，QUIC 可在应用层操作改变拥塞控制方法。
- 前向纠错(FEC)：将数据切割成包后可对每个包进行异或运算，将运算结果随数据发送。一旦丢失数据可据此推算。(带宽换时间)
- 单调递增的 Packet Number：TCP 在超时重传后的两次 ACK 接受情况并不支持的很好。导致 RTT 和 RTO 的计算有所偏差。HTTP/3 对此进行改进，一旦重传后的 Packet N 会递增。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbde7e87843c~tplv-t2oaga2asx-image.image)

预览

- ACK Delay

  HTTP/3 在计算 RTT 时健壮的考虑了服务端的 ACK 处理时延。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/7/1728dbe831911ad6~tplv-t2oaga2asx-image.image)

预览

- 更多地 ACK 块

  一般每次请求都会对应一个 ACK，但这样也会浪费(下载场景只需返回数据即可)。

  于是可设计成每次返回 3 个 ACK block。在 HTTP/3 将其扩充成最多可携带 256 个 ACK block。

### 5\. **流量控制**

TCP 使用滑动窗口的方式对发送方的流量进行控制。而对接收方并无限制。在 QUIC 中便补齐了这一短板。

QUIC 中接收方从单挑 Stream 和整条连接两个角度动态调整接受的窗口大小。
