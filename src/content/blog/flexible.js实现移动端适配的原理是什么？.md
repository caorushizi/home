---
title: flexible.js实现移动端适配的原理是什么？
pubDatetime: 2022-03-20T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: e91f1683237ea21681153876ee095cab
description: >-
  >flexible.js官方已不再维护，目前推行vw适配方案，本答案只是为了分析它的原理。flexible.js存在的目的，是为了让网页在各终端上的展示效果就像缩放设计稿图片一样，在不同屏幕上等比缩放
difficulty: 3
questionNumber: 128
source: >-
  https://fe.ecool.fun/topic-answer/3c003aad-68a0-4abf-8fbc-62e37b4f3b10?orderBy=updateTime&order=desc&tagId=10
---

> flexible.js 官方已不再维护，目前推行 vw 适配方案，本答案只是为了分析它的原理。

flexible.js 存在的目的，是为了让网页在各终端上的展示效果就像缩放设计稿图片一样，在不同屏幕上等比缩放，每一个元素与整体比例保持不变，真实还原设计稿。

# 基本原理

设页面宽度为 P（单位 px）

设计稿宽度为 750px

设 html 基准值为 X（单位 px）

---

首先将页面分为 100 份，份的单位为 F

设 1F 的像素值为 A（单位 px/F）

那么：

P = 100F \* A

A = P/100F

当 P 为 750 时，A=7.5px/F，即一份为 7.5px

有没有感觉这个 A 有点熟悉，没错它就是 X，上面份的单位 F 其实就是 rem。

（html font-size 的基准值单位虽然写为 px，但其实是 px/F，这点你知道就可以了）

现在懂了吧。

rem 的原理就是份，我们根据设计稿得到元素的份，写到代码中的也是份，现在只要动态改变 html 的基准值，就能够在不同屏幕下适配，从而还原设计稿尺寸了。

所以 flexible.js 的原理主要是：

window.onresize = function() { html.size = P/100 + 'px' }

当然针对高清屏，它还会设置“viewport scale”，以缩放页面，解决类似高清屏下无法实现 1px 边框等问题。

需要注意的是，基准值其实是个动态值，只是在写代码时，我们是按照设计稿宽度计算的基准值写的 rem，即以设计稿为标准进行屏幕适配的（将设计稿用代码还原成 UI 界面），但在实际运行时，页面宽度是动态的，所以基准值也是动态的哦。

# 源码解析

flexible.js 的源码并不多，总共不到 50 行：

```js
// 首先是一个立即执行函数，执行时传入的参数是window和document
(function flexible(window, document) {
  var docEl = document.documentElement; // 返回文档的root元素
  var dpr = window.devicePixelRatio || 1;
  // 获取设备的dpr，即当前设置下物理像素与虚拟像素的比值

  // 调整body标签的fontSize，fontSize = (12 * dpr) + 'px'
  // 设置默认字体大小，默认的字体大小继承自body
  function setBodyFontSize() {
    if (document.body) {
      document.body.style.fontSize = 12 * dpr + "px";
    } else {
      document.addEventListener("DOMContentLoaded", setBodyFontSize);
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  // 设置root元素的fontSize = 其clientWidth / 10 + ‘px’
  function setRemUnit() {
    var rem = docEl.clientWidth / 10;
    docEl.style.fontSize = rem + "px";
  }

  setRemUnit();

  // 当页面展示或重新设置大小的时候，触发重新
  window.addEventListener("resize", setRemUnit);
  window.addEventListener("pageshow", function (e) {
    if (e.persisted) {
      setRemUnit();
    }
  });

  // 检测0.5px的支持，支持则root元素的class中有hairlines
  if (dpr >= 2) {
    var fakeBody = document.createElement("body");
    var testElement = document.createElement("div");
    testElement.style.border = ".5px solid transparent";
    fakeBody.appendChild(testElement);
    docEl.appendChild(fakeBody);
    if (testElement.offsetHeight === 1) {
      docEl.classList.add("hairlines");
    }
    docEl.removeChild(fakeBody);
  }
})(window, document);
```
