---
title: 合并K个升序链表
pubDatetime: 2021-07-24T16:00:00.000Z
author: caorushizi
tags:
  - leetcode
postSlug: 61ba34f4848066170b510e4b1d56e269
description: >-
  给你一个链表数组，每个链表都已经按升序排列。请你将所有链表合并到一个升序链表中，返回合并后的链表。示例1：输入：lists=[[1,4,5],[1,3,4],[2,6]]输出：[1,1,2,3,4,4
difficulty: 4
questionNumber: 38
source: >-
  https://fe.ecool.fun/topic-answer/0e5e7b73-c27f-4e4f-a8ff-c39927175a55?orderBy=updateTime&order=desc&tagId=31
---

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

示例 1：

    输入：lists = [[1,4,5],[1,3,4],[2,6]]
    输出：[1,1,2,3,4,4,5,6]
    解释：链表数组如下：
    [
      1->4->5,
      1->3->4,
      2->6
    ]
    将它们合并到一个有序链表中得到。
    1->1->2->3->4->4->5->6

示例 2：

    输入：lists = []
    输出：[]

示例 3：

    输入：lists = [[]]
    输出：[]

提示：

- k == lists.length
- 0 <= k <= 10^4
- 0 <= lists\[i\].length <= 500
- \-10^4 <= lists\[i\]\[j\] <= 10^4
- lists\[i\] 按 升序 排列
- lists\[i\].length 的总和不超过 10^4

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function (lists) {};
```
