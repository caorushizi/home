---
title: GET和POST的请求的区别
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - 计算机网络
postSlug: f4064d210154b61de396f19cc8820fc8
description: >-
  Post和Get是HTTP请求的两种方法。*应用场景：GET请求是一个**幂等**的请求，一般Get请求用于对服务器资源不会产生影响的场景，比如说请求一个网页。而Post不是一个幂等的请求，一般用于对
difficulty: 3
questionNumber: 66
source: >-
  https://fe.ecool.fun/topic-answer/706d3e5d-a02b-4925-84e2-3e2c81c7ef1b?orderBy=updateTime&order=desc&tagId=16
---

Post 和 Get 是 HTTP 请求的两种方法。

- 应用场景：GET 请求是一个**幂等**的请求，一般 Get 请求用于对服务器资源不会产生影响的场景，比如说请求一个网页。而 Post 不是一个幂等的请求，一般用于对服务器资源会产生影响的情景。比如注册用户这一类的操作。
- 是否缓存：因为不同的应用场景，所以浏览器一般会对 Get 请求缓存，但很少对 Post 请求缓存。
- 发送的报文格式：Get 请求的报文中实体部分为空，Post 请求的报文中实体部分一般为向服务器发送的数据。
- 安全性：Get 请求可以将请求的参数放入 url 中向服务器发送，这样的做法相对于 Post 请求来说，一个方面是不太安全，因为请求的 url 会被保留在历史记录中。
- 请求长度：浏览器由于对 url 有一个长度上的限制，所以会影响 get 请求发送数据时的长度。这个限制是浏览器规定的，并不是 RFC 规定的。
- 参数类型：post 的参数传递支持更多的数据类型。
