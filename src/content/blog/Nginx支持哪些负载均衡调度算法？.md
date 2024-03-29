---
title: Nginx支持哪些负载均衡调度算法？
pubDatetime: 2021-07-24T16:00:00.000Z
author: caorushizi
tags:
  - 计算机网络
postSlug: be7897b999ae9bdb322aaa4e981f831b
description: >-
  *weight轮询（默认，常用，具有HA功效！）：接收到的请求按照权重分配到不同的后端服务器，即使在使用过程中，某一台后端服务器宕机，Nginx会自动将该服务器剔除出队列，请求受理情况不会受到任何影响
difficulty: 3.5
questionNumber: 41
source: >-
  https://fe.ecool.fun/topic-answer/cfff7bf1-9ff0-4661-8e8e-2ddec4ed270a?orderBy=updateTime&order=desc&tagId=16
---

- weight 轮询（默认，常用，具有 HA 功效！）：接收到的请求按照权重分配到不同的后端服务器，即使在使用过程中，某一台后端服务器宕机，Nginx 会自动将该服务器剔除出队列，请求受理情况不会受到任何影响。 这种方式下，可以给不同的后端服务器设置一个权重值(weight)，用于调整不同的服务器上请求的分配率；权重数据越大，被分配到请求的几率越大；该权重值，主要是针对实际工作环境中不同的后端服务器硬件配置进行调整的。
- ip_hash（常用）：每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器，这也在一定程度上解决了集群部署环境下 session 共享的问题。
- fair：智能调整调度算法，动态的根据后端服务器的请求处理到响应的时间进行均衡分配，响应时间短处理效率高的服务器分配到请求的概率高，响应时间长处理效率低的服务器分配到的请求少；结合了前两者的优点的一种调度算法。但是需要注意的是 Nginx 默认不支持 fair 算法，如果要使用这种调度算法，请安装 upstream_fair 模块。
- url_hash：按照访问的 url 的 hash 结果分配请求，每个请求的 url 会指向后端固定的某个服务器，可以在 Nginx 作为静态服务器的情况下提高缓存效率。同样要注意 Nginx 默认不支持这种调度算法，要使用的话需要安装 Nginx 的 hash 软件包。
