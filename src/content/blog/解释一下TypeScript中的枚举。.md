---
title: 解释一下TypeScript中的枚举。
pubDatetime: 2021-07-10T16:00:00.000Z
author: caorushizi
tags:
  - typescript
postSlug: 704be92e16a7454215d05086d2307ba0
description: >-
  枚举是TypeScipt数据类型，它允许我们定义一组命名常量。使用枚举使记录意图或创建一组不同的案例变得更加容易。它是相关值的集合，可以是数字值或字符串值。```typescriptenumGende
difficulty: 1
questionNumber: 26
source: >-
  https://fe.ecool.fun/topic-answer/c585e9b3-1595-40cc-9132-b9dff1abd028?orderBy=updateTime&order=desc&tagId=19
---

枚举是 TypeScipt 数据类型，它允许我们定义一组命名常量。 使用枚举使记录意图或创建一组不同的案例变得更加容易。 它是相关值的集合，可以是数字值或字符串值。

```typescript
enum Gender {
    Male,
    Female
    Other
}
console.log(Gender.Male); // Output: 0

//We can also access an enum value by it's number value.
console.log(Gender[1]); // Output: Female
```
