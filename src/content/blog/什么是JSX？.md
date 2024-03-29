---
title: 什么是JSX？
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 9f92d6ba9b3ce09a4edea935785eced8
description: >-
  JSX即JavaScriptXML。一种在React组件内部构建标签的类XML语法。JSX为react.js开发的一套语法糖，也是react.js的使用基础。React在不使用JSX的情况下一样可以工
difficulty: 1.5
questionNumber: 95
source: >-
  https://fe.ecool.fun/topic-answer/5bdf6ed5-2178-4bef-8690-c04dcdf46930?orderBy=updateTime&order=desc&tagId=13
---

JSX 即 JavaScript XML。一种在 React 组件内部构建标签的类 XML 语法。JSX 为 react.js 开发的一套语法糖，也是 react.js 的使用基础。React 在不使用 JSX 的情况下一样可以工作，然而使用 JSX 可以提高组件的可读性，因此推荐使用 JSX。

```jsx
class MyComponent extends React.Component {
  render() {
    let props = this.props;
    return (
      <div className="my-component">
        <a href={props.url}>{props.name}</a>
      </div>
    );
  }
}
```

**优点**：

- 允许使用熟悉的语法来定义 HTML 元素树；
- 提供更加语义化且移动的标签；
- 程序结构更容易被直观化；
- 抽象了 React Element 的创建过程；
- 可以随时掌控 HTML 标签以及生成这些标签的代码；
- 是原生的 JavaScript。
