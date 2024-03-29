---
title: 说说你对useMemo的理解
pubDatetime: 2022-05-29T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 6ec44f2c25c6ef254575c35093404201
description: >-
  Memo====在class的时代，我们一般是通过pureComponent来对数据进行一次浅比较，引入Hook特性后，我们可以使用Memo进行性能提升。在此之前，我们来做一个实验```jsimpor
difficulty: 1
questionNumber: 40
source: >-
  https://fe.ecool.fun/topic-answer/33a7cf04-f6d0-4b57-9a9b-60983f09b553?orderBy=updateTime&order=desc&tagId=13
---

# Memo

在 class 的时代，我们一般是通过 pureComponent 来对数据进行一次浅比较，引入 Hook 特性后，我们可以使用 Memo 进行性能提升。

在此之前，我们来做一个实验

```js
import React, { useState } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function App() {
  const [n, setN] = useState(0);
  const [m, setM] = useState(10);
  console.log("执行最外层盒子了");
  return (
    <>
      <div>
        最外层盒子
        <Child1 value={n} />
        <Child2 value={m} />
        <button
          onClick={() => {
            setN(n + 1);
          }}
        >
          n+1
        </button>
        <button
          onClick={() => {
            setM(m + 1);
          }}
        >
          m+1
        </button>
      </div>
    </>
  );
}
function Child1(props) {
  console.log("执行子组件1了");
  return <div>子组件1上的n：{props.value}</div>;
}
function Child2(props) {
  console.log("执行子组件2了");
  return <div>子组件2上的m：{props.value}</div>;
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

上面的代码我设置了两个子组件，分别读取父组件上的 n 跟 m，然后父组件上面设置两个点击按钮，当点击后分别让设置的 n、m 加 1。以下是第一次渲染时 log 控制台的结果

    执行最外层盒子了
    执行子组件1了
    执行子组件2了

跟想象中一样，render 时先进入 App 函数，执行，发现里面的两个 child 函数，执行，创建虚拟 dom，创建实体 dom，最后将画面渲染到页面上。

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ee29f9aa15c4ba7af3129028494d2cf~tplv-k3u1fbpfcp-watermark.image)

预览

# 使用 Memo 优化

当我点击 n+1 按钮时，此时 state 里面的 n 必然+1，也会重新引发 render 渲染，并把新的 n 更新到视图中。

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f55bac905da45b2bd56bde9836bcf22~tplv-k3u1fbpfcp-watermark.image)

预览

我们再看控制台

    执行最外层盒子了
    执行子组件1了
    执行子组件2了
    + 执行最外层盒子了
    + 执行子组件1了
    + 执行子组件2了 //为什么组件2也渲染了，里面的m没有变化

你会发现子组件 2 也渲染了，显然 react 重新把所有的函数都执行了一遍，把未曾有 n 数据的子组件 2 也重新执行了。

如何优化？我们可以使用`memo`把子组件改成以下代码

```js
const Child1 = React.memo(props => {
  console.log("执行子组件1了");
  return <div>子组件1上的n：{props.value}</div>;
});

const Child2 = React.memo(props => {
  console.log("执行子组件2了");
  return <div>子组件2上的m：{props.value}</div>;
});
```

再重新点击试试？

    执行最外层盒子了
    执行子组件1了
    执行子组件2了
    + 执行最外层盒子了
    + 执行子组件1了

会发现没有执行子组件 2 了

这样的话 react 就会只执行对应 state 变化的组件，而没有变化的组件，则复用上一次的函数，也许 memo 也有 memory 的意思，代表记忆上一次的函数，不重新执行（我瞎猜的- -！！）

# 出现 bug

上面的代码虽然已经优化好了性能，但是会有一个 bug

上面的代码是由父组件控制`<button>`的，如果我把控制 state 的函数传递给子组件，会怎样呢？

```html
<Child2 value="{m}" onClick="{addM}" /> //addM是修改M的函数
```

点击按钮让 n+1

    执行最外层盒子了
    执行子组件1了
    执行子组件2了
    + 执行最外层盒子了
    + 执行子组件1了
    + 执行子组件2了

又重新执行子组件 2。

为什么会这样？因为 App 重新执行了，它会修改 addM 函数的地址（函数是复杂数据类型），而 addM 又作为 props 传递给子组件 2，那么就会引发子组件 2 函数的重新执行。

# useMemo

这时候就要用 useMemo 解决问题。

`useMemo(()=>{},[])`

useMemo 接收两个参数，分别是函数和一个数组（实际上是依赖），函数里 return 函数,数组内存放依赖。

```js
const addM = useMemo(() => {
  return () => {
    setM({ m: m.m + 1 });
  };
}, [m]); //表示监控m变化
```

使用方式就跟 useEffect 似的。

# useCallback

上面的代码很奇怪有没有

```js
useMemo(() => {
  return () => {
    setM({ m: m.m + 1 });
  };
}, [m]);
```

react 就给我们准备了语法糖，useCallback。它是这样写的

```javascript
const addM = useCallback(() => {
  setM({ m: m.m + 1 });
}, [m]);
```

是不是看上去正常多了？

# 最终代码

```js
import React, { useCallback, useMemo, useState } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function App() {
  const [n, setN] = useState(0);
  const [m, setM] = useState({ m: 1 });
  console.log("执行最外层盒子了");
  const addN = useMemo(() => {
    return () => {
      setN(n + 1);
    };
  }, [n]);
  const addM = useCallback(() => {
    setM({ m: m.m + 1 });
  }, [m]);
  return (
    <>
      <div>
        最外层盒子
        <Child1 value={n} click={addN} />
        <Child2 value={m} click={addM} />
        <button onClick={addN}>n+1</button>
        <button onClick={addM}>m+1</button>
      </div>
    </>
  );
}
const Child1 = React.memo(props => {
  console.log("执行子组件1了");
  return <div>子组件1上的n：{props.value}</div>;
});

const Child2 = React.memo(props => {
  console.log("执行子组件2了");
  return <div>子组件2上的m：{props.value.m}</div>;
});

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

# 总结

- 使用`memo`可以帮助我们优化性能，让`react`没必要执行不必要的函数
- 由于复杂数据类型的地址可能发生改变，于是传递给子组件的`props`也会发生变化，这样还是会执行不必要的函数，所以就用到了`useMemo`这个 api
- `useCallback`是`useMemo`的语法糖
