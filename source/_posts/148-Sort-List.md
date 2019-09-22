---
title: 148. Sort List
date: 2019-09-22 19:47:29
tags:
---

Medium

https://leetcode.com/problems/sort-list/

Sort a linked list in *O*(*n* log *n*) time using constant space complexity.

**Example 1:**

```
Input: 4->2->1->3
Output: 1->2->3->4
```

---

2019.9.22 做出来了

**方法：**

链表的归并排序

思路比较简单，但是找链表中点的代码那里还是要注意一点，一不小心就写 bug 了。

```python
class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        ans = mergeSort(head)
        return ans

def mergeSort(node):
    if not node or not node.next:
        return node
    slow,fast = node,node.next
    while fast and fast.next:
        fast = fast.next.next
        slow = slow.next
    left = node
    right = slow.next
    slow.next = None
    new_l = mergeSort(left)
    new_r = mergeSort(right)
    return merge(new_l,new_r)

def merge(l,r):
    head = ListNode(0)
    cur = head
    while l and r:
        if l.val<r.val:
            cur.next = l
            l = l.next
        else:
            cur.next = r
            r = r.next
        cur = cur.next
        cur.next = None
    if l:
        cur.next = l
    if r:
        cur.next = r
    return head.next
```

**类似题目：**

[Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/)

