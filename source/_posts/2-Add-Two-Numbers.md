---
title: 2. Add Two Numbers
date: 2019-09-22 21:02:10
tags:
---

Medium

https://leetcode.com/problems/add-two-numbers/

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

---

2019.9.22 做出来了

**方法：**

依次从前往后遍历 l1 和 l2 的节点，同时用一个变量 flg 表示上一次的进位值。

```python
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1 or not l2:
            return l1 if not l2 else l2
        head = ListNode(0)
        p,q = l1,l2
        flg = 0
        cur = head
        while p and q:
            val = (flg+p.val+q.val)%10
            new = ListNode(val)
            cur.next = new
            flg = (flg+p.val+q.val)/10
            p = p.next
            q= q.next
            cur = cur.next
        while p:
            val = (flg+p.val)%10
            new = ListNode(val)
            cur.next = new
            flg = (flg+p.val)/10
            p = p.next
            cur = cur.next
        while q:
            val = (flg+q.val)%10
            new = ListNode(val)
            cur.next = new
            flg = (flg+q.val)/10
            q = q.next
            cur = cur.next
        if flg>0:
            new = ListNode(flg)
            cur.next = new
        return head.next
```

**类似题目：**

Multiply Strings
Add Binary
Sum of Two Integers
Add Strings
Add Two Numbers II
Add to Array-Form of Integer