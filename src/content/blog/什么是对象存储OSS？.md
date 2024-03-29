---
title: 什么是对象存储OSS？
pubDatetime: 2021-07-06T16:00:00.000Z
author: caorushizi
tags:
  - 计算机网络
postSlug: 2313b3e9e2f7636f9b90b8e46d374f69
description: >-
  对象存储OSS（ObjectStorageService）是一种海量、安全、低成本、高持久的云存储服务。OSS具有与平台无关的RESTfulAPI接口，您可以在任何应用、任何时间、任何地点存储和访问任
difficulty: 2
questionNumber: 52
source: >-
  https://fe.ecool.fun/topic-answer/5ee5ebe0-04c8-4852-a0fb-5c1178cb17dc?orderBy=updateTime&order=desc&tagId=16
---

对象存储 OSS（Object Storage Service）是一种海量、安全、低成本、高持久的云存储服务。

OSS 具有与平台无关的 RESTful API 接口，您可以在任何应用、任何时间、任何地点存储和访问任意类型的数据。

## OSS 相关概念

- 存储类型（Storage Class） OSS 提供标准、低频访问、归档、冷归档四种存储类型，全面覆盖从热到冷的各种数据存储场景。其中标准存储类型提供高持久、高可用、高性能的对象存储服务，能够支持频繁的数据访问；低频访问存储类型适合长期保存不经常访问的数据（平均每月访问频率 1 到 2 次），存储单价低于标准类型；归档存储类型适合需要长期保存（建议半年以上）的归档数据；冷归档存储适合需要超长时间存放的极冷数据。更多信息，请参见存储类型介绍。
- 存储空间（Bucket） 存储空间是您用于存储对象（Object）的容器，所有的对象都必须隶属于某个存储空间。存储空间具有各种配置属性，包括地域、访问权限、存储类型等。您可以根据实际需求，创建不同类型的存储空间来存储不同的数据。
- 对象（Object） 对象是 OSS 存储数据的基本单元，也被称为 OSS 的文件。对象由元信息（Object Meta）、用户数据（Data）和文件名（Key）组成。对象由存储空间内部唯一的 Key 来标识。对象元信息是一组键值对，表示了对象的一些属性，例如最后修改时间、大小等信息，同时可以在元信息中存储一些自定义的信息。
- 地域（Region） 地域表示 OSS 的数据中心所在物理位置。您可以根据费用、请求来源等选择合适的地域创建 Bucket。更多信息，请参见 OSS 已开通的地域。
- 访问域名（Endpoint） Endpoint 表示 OSS 对外服务的访问域名。OSS 以 HTTP RESTful API 的形式对外提供服务，当访问不同地域的时候，需要不同的域名。通过内网和外网访问同一个地域所需要的域名也是不同的。
- 访问密钥（AccessKey） AccessKey 简称 AK，指的是访问身份验证中用到的 AccessKey ID 和 AccessKey Secret。OSS 通过使用 AccessKey ID 和 AccessKey Secret 对称加密的方法来验证某个请求的发送者身份。AccessKey ID 用于标识用户；AccessKey Secret 是用户用于加密签名字符串和 OSS 用来验证签名字符串的密钥，必须保密。
