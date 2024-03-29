---
title: 为什么部分请求中，参数需要使用encodeURIComponent进行转码？
pubDatetime: 2021-07-24T16:00:00.000Z
author: caorushizi
tags:
  - 计算机基础
postSlug: 262d1f225c2617f3abd987f9c4a23f0d
description: >-
  一般来说，URL只能使用英文字母、阿拉伯数字和某些标点符号，不能使用其他文字和符号。这是因为网络标准RFC1738做了硬性规定：>"...Onlyalphanumerics\[0-9a-zA-Z\],
difficulty: 3
questionNumber: 11
source: >-
  https://fe.ecool.fun/topic-answer/ea7dbe32-726d-4d21-a9bc-3df77e1ec853?orderBy=updateTime&order=desc&tagId=30
---

一般来说，URL 只能使用英文字母、阿拉伯数字和某些标点符号，不能使用其他文字和符号。

这是因为网络标准 RFC 1738 做了硬性规定：

> "...Only alphanumerics \[0-9a-zA-Z\], the special characters "$-\_.+!\*'()," \[not including the quotes - ed\], and reserved characters used for their reserved purposes may be used unencoded within a URL."

这意味着，如果 URL 中有汉字，就必须编码后使用。但是麻烦的是，RFC 1738 没有规定具体的编码方法，而是交给应用程序（浏览器）自己决定。这导致"URL 编码"成为了一个混乱的领域。

不同的操作系统、不同的浏览器、不同的网页字符集，将导致完全不同的编码结果。如果程序员要把每一种结果都考虑进去，是不是太恐怖了？有没有办法，能够保证客户端只用一种编码方法向服务器发出请求？

就是使用 Javascript 先对 URL 编码，然后再向服务器提交，不要给浏览器插手的机会。因为 Javascript 的输出总是一致的，所以就保证了服务器得到的数据是格式统一的。

Javascript 语言用于编码的函数，一共有三个，最古老的一个就是 escape()。虽然这个函数现在已经不提倡使用了，但是由于历史原因，很多地方还在使用它，所以有必要先从它讲起。

它的具体规则是，除了 ASCII 字母、数字、标点符号"@ \* \_ + - . /"以外，对其他所有字符进行编码。

encodeURI()是 Javascript 中真正用来对 URL 编码的函数。

它着眼于对整个 URL 进行编码，因此除了常见的符号以外，对其他一些在网址中有特殊含义的符号"; / ? : @ & = + $ , #"，也不进行编码。编码后，它输出符号的 utf-8 形式，并且在每个字节前加上%。

最后一个 Javascript 编码函数是 encodeURIComponent()。与 encodeURI()的区别是，它用于对 URL 的组成部分进行个别编码，而不用于对整个 URL 进行编码。

因此，"; / ? : @ & = + $ , #"，这些在 encodeURI()中不被编码的符号，在 encodeURIComponent()中统统会被编码。至于具体的编码方法，两者是一样。

它对应的解码函数是 decodeURIComponent()。
