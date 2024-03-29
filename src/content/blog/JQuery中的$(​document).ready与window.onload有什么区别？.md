---
title: JQuery中的$(​document).ready与window.onload有什么区别？
pubDatetime: 2022-09-26T16:00:00.000Z
author: caorushizi
tags:
  - javascript
postSlug: d6a78a3940bc1757656ebe35c99d5f99
description: >-
  定义--再说两者之前先简单说明一下window与document的区别：*window1.window对象表示浏览器中打开的窗口。2.window对象可以省略，如:`window.console.lo
difficulty: 1
questionNumber: 81
source: >-
  https://fe.ecool.fun/topic-answer/c4442ea9-cfe9-4ed5-a82c-8adc2e4e5d55?orderBy=updateTime&order=desc&tagId=10
---

## 定义

再说两者之前先简单说明一下 window 与 document 的区别：

- window
  1.  window 对象表示浏览器中打开的窗口。
  2.  window 对象可以省略，如:`window.console.log()`等价于`console.log()`
- document
  1.  document 对象是 window 对象的一部分,如：`document.body` 等价于 `window.document.body`
  2.  浏览器的 html 文档成为 document 对象

### $(document).ready()

从字面的意思上理解，就是文档准备好了，也就是浏览器已经加载并解析完整个 html 文档，DOM 树已经建立起来了,然后执行此函数。

原生的 JavaScript 写法如下：

    document.ready=function(){
     alert("ready");
    }

jQuery 中的写法如下：

    $(document).ready(function(){
     alert("ready");
    });
    //或者简写为
    $(function(){
     alert("ready");
    });

### $(window).load

在网页中所有元素(包括页面中图片、css 文件等所有关联文件)完全加载到浏览器后才执行。

原生 JavaScript 中的写法如下

    window.onload = function(){
     alert("onload");
    };

jQuery 中的写法如下：

    $(window).load(function(){
     alert("onload");
    });

## ready 与 load 执行顺序

先来看一下 DOM 文档加载的步骤：

        1.解析HTML结构
        2.加载外部脚本和样式表文件
        3.解析并执行脚本代码
        4.构造HTML DOM模型 //ready
        5.加载图片等外部文件
        6.页面加载完毕 //load

从上面的步骤中可以看出，ready 在第 4 步完成之后就执行了，但是 load 要在第 6 步完成之后才执行。

## 两者区别

### 1.执行时间

- `$(window).load()`必须等到页面内包括图片的所有元素加载完毕后才能执行（比如图片和媒体资源，它们的加载速度远慢于 DOM 的加载速度）加载完成之后才执行。
- `$(document).ready()`是 DOM 结构绘制完毕后就执行，不必等到加载完毕。但这并不代表页面的所有数据已经全部加载完成，一些大的图片有会在建立 DOM 树之后很长一段时间才行加载完成

以浏览器装载文档为例，在页面加载完毕后，浏览器会通过 Javascript 为 DOM 元素添加事件。在常规的 Javascript 代码中，通常使用 window.onload 方法，而在 Jquery 中，使用的是 `$(document).ready()` 方法。 `$(document).ready()`方法是事件模块中最重要一个函数，可以极大的提高 Web 应用程序的速度。

### 2.编写个数不同

- `$(window).load`不能同时编写多个，如果有多个`$(window).load()`，那么只有最后一个`$(window).load()`里面的函数或者代码才会执行，之前的`$(window).load()`都将被覆盖。
- `$(document).ready()`可以同时编写多个，并且都可以得到执行。

示例如下：

以下代码无法正确执行,结果只输出第二个,:

    $(window).load(function(){
        alert(“text1”);
    });
    $(window).load(function(){
        alert(“text2”);
    });

`$(document).ready()`能同时编写多个,以下代码正确执行，结果两次都输出：

    $(document).ready(function(){
        alert(“Hello World”);
    });
    $(document).ready(function(){
        alert(“Hello again”);
    });

### 3.简化写法

- `$(window).load`没有简化写法
- `$(document).ready(function(){})`可以简写成`$(function(){})`或者`$().ready(function(){})`

### 4.执行的效率不同

- 如要在 dom 的元素节点中添加 onclick 属性节点，这时用`$(document).ready()`就要比用`$(window).load()`的效率高
- 但是在某些时候还必须得用`$(window).load()`才行，比如按钮图片出现后添加事件
