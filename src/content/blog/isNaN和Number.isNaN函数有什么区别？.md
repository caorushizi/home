---
title: isNaN和Number.isNaN函数有什么区别？
pubDatetime: 2021-08-22T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: bb9d4257f5dc8344f9acb5d677c0512e
description: >-
  NaN---全局属性NaN的值表示不是一个数字（Not-A-Number）。在JavaScript中，NaN最特殊的地方就是，我们不能使用相等运算符（==(en-US)和===(en-US)）来判断一
difficulty: 2
questionNumber: 224
source: >-
  https://fe.ecool.fun/topic-answer/8200a6ae-94f7-4056-bdb8-6bd84b383500?orderBy=updateTime&order=desc&tagId=10
---

## NaN

全局属性 NaN 的值表示不是一个数字（Not-A-Number）。

在 JavaScript 中，NaN 最特殊的地方就是，我们不能使用相等运算符（== (en-US) 和 === (en-US)）来判断一个值是否是 NaN，因为 NaN == NaN 和 NaN === NaN 都会返回 false。因此，必须要有一个判断值是否是 NaN 的方法。

## 方法简介

- 函数 isNaN 接收参数后，会尝试将这个参数转换为数值，任何不能被转换为数值的的值都会返回 true，因此非数字值传入也会返回 true ，会影响 NaN 的判断。
- 函数 Number.isNaN 会首先判断传入参数是否为数字，如果是数字再继续判断是否为 NaN ，不会进行数据类型的转换，这种方法对于 NaN 的判断更为准确。

## 总结

和全局函数 isNaN() 相比，Number.isNaN() 不会自行将参数转换成数字，只有在参数是值为 NaN 的数字时，才会返回 true。

Number.isNaN() 方法确定传递的值是否为 NaN，并且检查其类型是否为 Number。它是原来的全局 isNaN() 的更稳妥的版本。
