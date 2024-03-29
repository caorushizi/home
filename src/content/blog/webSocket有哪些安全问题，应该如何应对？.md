---
title: webSocket有哪些安全问题，应该如何应对？
pubDatetime: 2022-10-11T16:00:00.000Z
author: caorushizi
tags:
  - 前端安全
postSlug: 814d0660f747f3280cb334329a9e7a89
description: >-
  ###1\.WebSocket特性介绍WebSocket是HTML5开始提供的一种浏览器与服务器间进行全双工通讯的网络技术。WebSocket通信协议于2011年被IETF定为标准RFC6455，We
difficulty: 4
questionNumber: 5
source: >-
  https://fe.ecool.fun/topic-answer/6100dbed-3600-470f-90b1-b1c6ef213a52?orderBy=updateTime&order=desc&tagId=21
---

### 1\. WebSocket 特性介绍

WebSocket 是 HTML5 开始提供的一种浏览器与服务器间进行全双工通讯的网络技术。WebSocket 通信协议于 2011 年被 IETF 定为标准 RFC 6455，WebSocket API 也被 W3C 定为标准，主流的浏览器都已经支持 WebSocket 通信。

WebSocket 协议是基于 TCP 协议上的独立的通信协议，在建立 WebSocket 通信连接前，需要使用 HTTP 协议进行握手，从 HTTP 连接升级为 WebSocket 连接。浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。

WebSocket 定义了两种 URI 格式, “ws://“和“wss://”，类似于 HTTP 和 HTTPS, “ws://“使用明文传输，默认端口为 80，”wss://“使用 TLS 加密传输，默认端口为 443。

```ini
ws-URI : "ws://host[:port]path[?query]" wss-URI : "wss://host[:port]path[?query]"复制代码
```

WebSocket 握手阶段，需要用到一些 HTTP 头，升级 HTTP 连接为 WebSocket 连接如下表所示。

HTTP 头

是否必须

解释

Host

是

服务端主机名

Upgrade

是

固定值，”websocket”

Connection

是

固定值，”Upgrade”

Sec-WebSocket-Key

是

客户端临时生成的 16 字节随机值, base64 编码

Sec-WebSocket-Version

是

WebSocket 协议版本

Origin

否

可选, 发起连接请求的源

Sec-WebSocket-Accept

是(服务端)

服务端识别连接生成的随机值

Sec-WebSocket-Protocol

否

可选，客户端支持的协议

Sec-WebSocket-Extensions

否

可选， 扩展字段

一次完整的握手连接如下图:

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/11/5/166e31708ccb6601~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.image)

预览

一旦服务器端返回 101 响应，即可完成 WebSocket 协议切换。服务器端可以基于相同端口，将通信协议从 [http://或](http://%E6%88%96) https:// 切换到 ws://或 wss://。协议切换完成后，浏览器和服务器端可以使用 WebSocket API 互相发送和收取文本和二进制消息。

### 2\. WebSocket 应用安全问题

WebSocket 作为一种通信协议引入到 Web 应用中，并不会解决 Web 应用中存在的安全问题，因此 WebSocket 应用的安全实现是由开发者或服务端负责。这就要求开发者了解 WebSocket 应用潜在的安全风险，以及如何做到安全开发规避这些安全问题。

#### 2.1 认证

WebSocket 协议没有规定服务器在握手阶段应该如何认证客户端身份。服务器可以采用任何 HTTP 服务器的客户端身份认证机制，如 cookie 认证，HTTP 基础认证，TLS 身份认证等。在 WebSocket 应用认证实现上面临的安全问题和传统的 Web 应用认证是相同的，如：[CVE-2015-0201](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-0201), Spring 框架的 Java SockJS 客户端生成可预测的会话 ID，攻击者可利用该漏洞向其他会话发送消息; [CVE-2015-1482](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-1482), Ansible Tower 未对用户身份进行认证，远程攻击者通过 websocket 连接获取敏感信息。

#### 2.2 授权

同认证一样，WebSocket 协议没有指定任何授权方式，应用程序中用户资源访问等的授权策略由服务端或开发者实现。WebSocket 应用也会存在和传统 Web 应用相同的安全风险，如：垂直权限提升和水平权限提升。

#### 2.3 跨域请求

WebSocket 使用基于源的安全模型，在发起 WebSocket 握手请求时，浏览器会在请求中添加一个名为 Origin 的 HTTP 头，Oringin 字段表示发起请求的源，以此来防止未经授权的跨站点访问请求。WebSocket 的客户端不仅仅局限于浏览器，因此 WebSocket 规范没有强制规定握手阶段的 Origin 头是必需的，并且 WebSocket 不受浏览器同源策略的限制。如果服务端没有针对 Origin 头部进行验证可能会导致跨站点 WebSocket 劫持攻击。该漏洞最早在 2013 年被 Christian Schneider 发现并公开，Christian 将之命名为跨站点 WebSocket 劫持 (Cross Site WebSocket Hijacking)(CSWSH)。跨站点 WebSocket 劫持危害大，但容易被开发人员忽视。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/11/5/166e31708cdaca2e~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.image)

预览

上图展示了跨站 WebSocket 劫持的过程，某个用户已经登录了 WebSocket 应用程序，如果他被诱骗访问了某个恶意网页，而恶意网页中植入了一段 js 代码，自动发起 WebSocket 握手请求跟目标应用建立 WebSocket 连接。注意到，Origin 和 Sec-WebSocket-Key 都是由浏览器自动生成的，浏览器再次发起请求访问目标服务器会自动带上 Cookie 等身份认证参数。如果服务器端没有检查 Origin 头，则该请求会成功握手切换到 WebSocket 协议，恶意网页就可以成功绕过身份认证连接到 WebSocket 服务器，进而窃取到服务器端发来的信息，或者发送伪造信息到服务器端篡改服务器端数据。与传统跨站请求伪造(CSRF)攻击相比，CSRF 主要是通过恶意网页悄悄发起数据修改请求，而跨站 WebSocket 伪造攻击不仅可以修改服务器数据，还可以控制整个双向通信通道。也正是因为这个原因，Christian 将这个漏洞命名为劫持(Hijacking)，而不是请求伪造(Request Forgery)。

理解了跨站 WebSocket 劫持攻击的原理和过程，那么如何防范这种攻击呢？处理也比较简单，在服务器端的代码中增加 对 Origin 头的检查，如果客户端发来的 Origin 信息来自不同域，服务器端可以拒绝该请求。但是仅仅检查 Origin 仍然是不够安全的，恶意网页可以伪造 Origin 头信息，绕过服务端对 Origin 头的检查，更完善的解决方案可以借鉴 CSRF 的解决方案-令牌机制。

#### 2.4 拒绝服务

WebSocket 设计为面向连接的协议，可被利用引起客户端和服务器端拒绝服务攻击。

**(1). 客户端拒绝服务**

WebSocket 连接限制不同于 HTTP 连接限制，和 HTTP 相比，WebSocket 有一个更高的连接限制，不同的浏览器有自己特定的最大连接数,如：火狐浏览器默认最大连接数为 200。通过发送恶意内容，用尽允许的所有 Websocket 连接耗尽浏览器资源，引起拒绝服务。

**(2). 服务器端拒绝服务**

WebSocket 建立的是持久连接，只有客户端或服务端其中一发提出关闭连接的请求，WebSocket 连接才关闭，因此攻击者可以向服务器发起大量的申请建立 WebSocket 连接的请求，建立持久连接，耗尽服务器资源，引发拒绝服务。针对这种攻，可以通过设置单 IP 可建立连接的最大连接数的方式防范。攻击者还可以通过发送一个单一的庞大的数据帧(如, 2^16)，或者发送一个长流的分片消息的小帧，来耗尽服务器的内存，引发拒绝服务攻击, 针对这种攻击，通过限制帧大小和多个帧重组后的总消息大小的方式防范。

#### 2.5 中间人攻击

WebSocket 使用 HTTP 或 HTTPS 协议进行握手请求，在使用 HTTP 协议的情况下，若存在中间人可以嗅探 HTTP 流量，那么中间人可以获取并篡改 WebSocket 握手请求，通过伪造客户端信息与服务器建立 WebSocket 连接，如下图所示。防范这种攻击，需要在加密信道上建立 WebSocket 连接，使用 HTTPS 协议发起握手请求。

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/11/5/166e31708ced092b~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.image)

预览

#### 2.6 输入校验

WebSocket 应用和传统 Web 应用一样，都需要对输入进行校验，来防范来客户端的 XSS 攻击，服务端的 SQL 注入，代码注入等攻击。

### 3\. 总结

Websocket 是一个基于 TCP 的 HTML5 的新协议，可以实现浏览器和服务器之间的全双工通讯。在即时通讯等应用中，WebSocket 具有很大的性能优势, 并且非常适合全双工通信，但是，和任何其他技术一样，开发 WebSocket 应用也需要考虑潜在的安全风险。
