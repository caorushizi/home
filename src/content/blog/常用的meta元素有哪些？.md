---
title: 常用的meta元素有哪些？
pubDatetime: 2021-07-04T16:00:00.000Z
author: caorushizi
tags:
  - html
postSlug: 9ad0ca2d3a29045c966a37961af80e4f
description: >-
  >作者：tonytony来源：掘金>The<meta>tagprovidesmetadataabouttheHTMLdocument.Metadatawillnotbedisplayedonthepa
difficulty: 1
questionNumber: 60
source: >-
  https://fe.ecool.fun/topic-answer/c849aa25-0dae-49aa-8148-b1c410a7aa1e?orderBy=updateTime&order=desc&tagId=12
---

> 作者：tonytony 来源：掘金

> The <meta> tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.

<meta> 元素标签是提供有关HTML文档的元数据，元数据不会显示在页面上，但是能够被机器识别。

总而言之, meta 标签是用来让机器识别的，同时它对 SEO 起着重要的作用。

## charset

指定了 html 文档的编码格式，常用的是 utf-8(Unicode 的字符编码)，还有 ISO-8859-1(拉丁字母的字符编码)。当然还有其他的，但是一般不常用也就不介绍了

```html
<meta charset="utf-8" />
```

## name & content

指定元数据的名称(这部分对 SEO 非常有用)

- author——定义了页面的作者

```html
<meta name="author" content="Tony" />
```

- keywords——为搜索引擎提供关键字

```html
<meta name="keywords" content="HTML, CSS, JavaScript" />
```

- description——对网页整体的描述

```html
<meta name="description" content="My tutorials on HTML, CSS and JavaScript" />
```

- viewport——对页面视图相关进行定义

  width=device-width——将页面宽度设置为跟随屏幕宽度变化而变化
  initial-scale=1.0——设置浏览器首次加载页面时的初始缩放比例(0.0-10.0 正数)
  maximum-scale=1.0——允许用户缩放的最大比例(0.0-10.0 正数)，必须大于等于 minimum-scale
  minimum-scale=1.0——允许用户缩放的最小比例(0.0-10.0 正数)，必须小于等于 maximum-scale
  user-scalable=no——是否允许用户手动缩放(yes 或者 no)

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minmum-scale=1.0"
/>
```

- generator——包含生成页面软件的标识符

> which contains the identifier of the software that generated the page.

```html
<meta name="generator" content="Hexo 3.8.0" />
```

- theme-color——定义主题颜色

```html
<meta name="theme-color" content="#222" />
```

- http-equiv & content

> Provides an HTTP header for the information/value of the content attribute

- refresh——每 30s 刷新一次文档

```html
<meta http-equiv="refresh" content="30" />
```

- X-UA-Compatible——告知浏览器以何种版本渲染界面。下面的例子有限使用 IE 最新版本

```html
<meta http-equiv="X-UA-Compatible" content="ie=edge" />
```

关于是否有必要使用这一条在 stack overflow 尚且有争议。个人认为如果不想兼容低版本的 IE，可以直接忽略这一条。

- Cache-Control——请求和响应遵循的缓存机制，可以声明缓存的内容，修改过期时间，可多次声明

> no-transform——不得对资源进行转换或转变。 no-siteapp——禁止百度进行转码

```html
<meta http-equiv="Cache-Control" content="no-transform" />
<meta http-equiv="Cache-Control" content="no-siteapp" />
```

- property & content

可以让网页成为一个富媒体对象，同意网页内容被其他网站引用，同时在应用的时候不会只是一个链接，会提取相应的信息展现给用户。

```html
<meta property="og:type" content="website" />
<meta property="og:url" content="https://zjgyb.github.io/index.html" />
<meta property="og:site_name" content="tony's blog" />
```
