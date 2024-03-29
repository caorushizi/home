---
title: for...in和for...of有什么区别？
pubDatetime: 2021-08-22T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: 35f7286fc66238f2058db585797eda73
description: >-
  for…of是ES6新增的遍历方式，允许遍历一个含有iterator接口的数据结构（数组、对象等）并且返回各项的值，和ES3中的for…in的区别如下：*for…of遍历获取的是对象的键值，for…i
difficulty: 2
questionNumber: 215
source: >-
  https://fe.ecool.fun/topic-answer/33d77817-96e1-4531-840c-26426223102c?orderBy=updateTime&order=desc&tagId=10
---

for…of 是 ES6 新增的遍历方式，允许遍历一个含有 iterator 接口的数据结构（数组、对象等）并且返回各项的值，和 ES3 中的 for…in 的区别如下：

- for…of 遍历获取的是对象的键值，for…in 获取的是对象的键名；
- for… in 会遍历对象的整个原型链，性能非常差不推荐使用，而 for … of 只遍历当前对象不会遍历原型链；
- 对于数组的遍历，for…in 会返回数组中所有可枚举的属性(包括原型链上可枚举的属性)，for…of 只返回数组的下标对应的属性值；

总结： for...in 循环主要是为了遍历对象而生，不适用于遍历数组；for...of 循环可以用来遍历数组、类数组对象，字符串、Set、Map 以及 Generator 对象。
