---
title: 行内元素有哪些？块级元素有哪些？空(void)元素有那些？
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: 349586fc270902e161cae0940c77e16b
description: >-
  CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值
difficulty: 1
questionNumber: 57
source: >-
  https://fe.ecool.fun/topic-answer/d6a65597-0522-4127-bbe1-68eb9da818ee?orderBy=updateTime&order=desc&tagId=12
---

CSS 规范规定，每个元素都有 display 属性，确定该元素的类型，每个元素都有默认的 display 值，如 div 的 display 默认值为“block”，则为“块级”元素；span 默认 display 属性值为“inline”，是“行内”元素。

- 常用的块状元素有：

```html
<div>
  、
  <p>、</p>
  <h1>
    ...
    <h6>
      、
      <ol>
        、
        <ul>
          、
          <dl>
            、
            <table>
              、
              <address>
                、
                <blockquote>
                  、
                  <form></form>
                </blockquote>
              </address>
            </table>
          </dl>
        </ul>
      </ol>
    </h6>
  </h1>
</div>
```

- 常用的内联元素有：

```html
<a
  >、<span
    >、<br />、<i
      >、<em
        >、<strong
          >、<label
            >、<q
              >、<var
                >、<cite
                  >、<code
                  ></code></cite></var></q></label></strong></em></i></span
></a>
```

- 常用的内联块状元素有：

```html
<img />、<input />
```

- 知名的空元素：

```html
<br />
<hr />
<img /> <input /> <link /> <meta /> <br />
```
