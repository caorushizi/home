---
title: 说说你对自定义hook的理解
pubDatetime: 2022-05-29T16:00:00.000Z
author: caorushizi
tags:
  - react
postSlug: 5aee9b788b9183d97f36cfd6faa99562
description: >-
  自定义Hook=======通过自定义Hook，可以将组件逻辑提取到可重用的函数中。可以理解成Hook就是用来放一些重复代码的函数。下面我将做手动实现一个列表渲染、删除的组件，然后把它做成自定义Hoo
difficulty: 1
questionNumber: 39
source: >-
  https://fe.ecool.fun/topic-answer/e0fd403c-a34d-418e-8a92-18cfa6e00e1b?orderBy=updateTime&order=desc&tagId=13
---

# 自定义 Hook

通过自定义 Hook，可以将组件逻辑提取到可重用的函数中。

可以理解成 Hook 就是用来放一些重复代码的函数。

下面我将做手动实现一个列表渲染、删除的组件，然后把它做成自定义 Hook。

## 示例

定义数据列表

```js
const initialState = [
  { id: 1, name: "qiu" },
  { id: 2, name: "yan" },
  { id: 2, name: "xi" },
];
```

创建一个 App 组件并渲染它

```js
function App(props) {
  const [state, setState] = useState(initialState);
  const deleteLi = (index) => {
    setState((state) => {
      const newState = JSON.parse(JSON.stringify(state));//深拷贝数据
      newState.splice(index, 1);
      return newState;
    });
  };
  return (
    <>
      <ul>
        {state
          ? state.map((v, index) => {
              return (
                <li key={index}>
                  {index + "、"}
                  {v.name}
                  <button
                    onClick={() => {
                      deleteLi(index);
                    }}
                  >
                    X
                  </button>
                </li>
              );
            })
          : \"加载中\"}
      </ul>
    </>
  );
}
```

上面的代码，我对一个数组进行渲染+删除操作，当点击按钮时，就会删除数组的对应 index 的数据，从而执行页面更新

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4b99c901f2a4807934d78d74242207b~tplv-k3u1fbpfcp-watermark.image)

预览

## 封装成 Hook

```js
const useList = () => {
  const [state, setState] = useState(initialState);
  const deleteLi = index => {
    setState(state => {
      const newState = JSON.parse(JSON.stringify(state));
      newState.splice(index, 1);
      return newState;
    });
  };
  return { state, setState, deleteLi }; //返回查、改、删
};
```

我把上面的业务逻辑都放在`useList`这个函数中，并将查、改、删的 API 给放在一个对象中 return 出去。这样就形成了一个自定义 Hook

## 使用自定义 Hook

一般可以将自定义 Hook 给单独放在一个文件中，如果要使用，就引过来

```js
+ import useList from \"./useList\";
```

在需要使用的 App 组件中执行自定义 Hook 并接收 API

```js
function App(props) {
  const { state, deleteLi } = useList();//这里接收return出来的查、删API
  return (
 	... //这里跟最开始的App组件里是一样的，为了页面整洁，就不贴代码了
  );
}
```

# 总结

所谓的自定义 Hook，实际上就是把很多重复的逻辑都放在一个函数里面，通过闭包的方式给`return`出来，这是非常高级的方式，程序员崇尚代码简洁，如果说以后业务开发时需要大量的重复代码，我们就可以将它封装成自定义 Hook。
