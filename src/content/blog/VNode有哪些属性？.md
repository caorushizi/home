---
title: VNode有哪些属性？
pubDatetime: 2022-04-05T16:00:00.000Z
author: caorushizi
tags:
  - vue
postSlug: 87fbcbe80109264e45c9872d1f909050
description: >-
  Vue内部定义的Vnode对象包含了以下属性：*\_\_v\_isVNode:_true_，内部属性，有该属性表示为Vnode*\_\_v\_skip:true，内部属性，表示跳过响应式转换，reac
difficulty: 3
questionNumber: 22
source: >-
  https://fe.ecool.fun/topic-answer/20be1725-4902-4135-8b80-7be60507fc13?orderBy=updateTime&order=desc&tagId=14
---

Vue 内部定义的 Vnode 对象包含了以下属性：

- \_\_v*isVNode: \_true*，内部属性，有该属性表示为 Vnode
- \_\_v_skip: true，内部属性，表示跳过响应式转换，reactive 转换时会根据此属性进行判断
- isCompatRoot?: _true_，用于是否做了兼容处理的判断
- type: VNodeTypes，虚拟节点的类型
- props: (VNodeProps & ExtraProps) | _null_，虚拟节点的 props
- key: _string_ | _number_ | _null_，虚拟阶段的 key，可用于 diff
- ref: VNodeNormalizedRef | _null_，虚拟阶段的引用
- scopeId: _string_ | _null_，仅限于 SFC(单文件组件)，在设置 currentRenderingInstance 当前渲染实例时，一期设置
- slotScopeIds: _string_\[\] | _null_，仅限于单文件组件，与单文件组件的插槽有关
- children: VNodeNormalizedChildren，子节点
- component: ComponentInternalInstance | null，组件实例
- dirs: DirectiveBinding\[\] | null，当前 Vnode 绑定的指令
- transition: TransitionHooks<HostElement> | null，TransitionHooks
- DOM 相关属性
  - el: HostNode | _null_，宿主阶段
  - anchor: HostNode | _null_ // fragment anchor
  - target: HostElement | _null_ ，teleport target 传送的目标
  - targetAnchor: HostNode | _null_ // teleport target anchor
  - staticCount: _number_，包含的静态节点的数量
- suspense 悬挂有关的属性
  - suspense: SuspenseBoundary | _null_
  - ssContent: VNode | _null_
  - ssFallback: VNode | _null_
- optimization only 用于优化的属性
  - shapeFlag: _number_
  - patchFlag: _number_
  - dynamicProps: _string_\[\] | _null_
  - dynamicChildren: VNode\[\] | _null_
- 根节点会有的属性
  - appContext: AppContext | _null_，实例上下文

可以看到在 Vue 内部，对于一个 Vnode 描述对象的属性大概有二十多个。

Vue 为了给用于减轻一定的负担，但又不至于太封闭，就创建了渲染 h。可以在用户需要的时候，通过 h 函数创建对应的 Vnode 即可。

这样就给为一些高阶玩家保留了自由发挥的空间。
