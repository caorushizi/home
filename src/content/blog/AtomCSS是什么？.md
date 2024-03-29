---
title: AtomCSS是什么？
pubDatetime: 2021-07-24T16:00:00.000Z
author: caorushizi
tags:
  - css
postSlug: d49dbd0944aadb8f4ffb42c9501f7112
description: >-
  AtomCSS：原子CSS，意思是一个类只干一件事。不同于大家常用的BEM这类规则，原子css就是拆分，所有CSS类都有一个唯一的CSS规则。例如如下```css.w-full{width:100%;
difficulty: 2
questionNumber: 55
source: >-
  https://fe.ecool.fun/topic-answer/b7956f38-87f5-4db6-958a-7ae47d60da9b?orderBy=updateTime&order=desc&tagId=11
---

Atom CSS：原子 CSS，意思是一个类只干一件事。

不同于大家常用的 BEM 这类规则，原子 css 就是拆分，所有 CSS 类都有一个唯一的 CSS 规则。例如如下

```css
.w-full {
  width: 100%;
}
.h-full {
  height: 100%;
}
```

而像这种就不是

    .w&h-full{
      width:100%;
      height:100%;
    }

当我们使用的时候，直接写 class 名就可以

```html
<html>
  <body>
    <div id="app" class="h-full w-full"></div>
  </body>
</html>
```

## 原子 CSS 的优缺点

- 优点
  - 减少了 css 体积，提高了 css 复用
  - 减少起名的复杂度
- 缺点
  - 增加了记忆成本。将 css 拆分为原子之后，你势必要记住一些 class 才能书写，哪怕 tailwindcss 提供了完善的工具链，你写 background，也要记住开头是 bg。
  - 增加了 html 结构的复杂性。当整个 dom 都是这样 class 名，势必会带来调试的麻烦，有的时候很难定位具体 css 问题
  - 你仍需要起 class 名。对于大部分属性而言，你可以只用到 center,auto，100%，这些值，但是有时候你仍需要设定不一样的参数值，例如 left，top，这时候你还需要起一个 class 名
