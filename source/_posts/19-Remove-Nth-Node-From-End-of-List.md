---
title: 19. Remove Nth Node From End of List
date: 2019-09-22 20:43:45
tags:
---

Medium

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

Given a linked list, remove the *n*-th node from the end of list and return its head.

**Example:**

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

**Note:**

Given *n* will always be valid.

**Follow up:**

Could you do this in one pass?

---

2019.9.22 做出来了

**方法：**

快慢指针。

P.S. 下面这坨代码写得太丑了，看到[有人写的挺简洁的](https://blog.csdn.net/fuxuemingzhu/article/details/80786149)

```python
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        if not head:
            return head
        fast = head
        i = 0
        while i<n and fast:
            fast = fast.next
            i += 1
        if i<n:
            return head
        if not fast:
            return head.next
        slow = head
        while fast and fast.next:
            fast = fast.next
            slow = slow.next
        temp = slow.next
        slow.next = temp.next
        return head
```

**类似题目：**

Partition List
Reverse String
Interval List Intersections