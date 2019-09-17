---
title: 215. Kth Largest Element in an Array
date: 2019-09-16 00:04:54
tags:
---

Medium

https://leetcode.com/problems/kth-largest-element-in-an-array/

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length

---

2019.9.16 没做出来，参考之前写的 TopKth.py 写的，还是没有完全掌握啊唉

**方法：**

快排

一开始正确写出了 search(arr, l, r) 函数（也就是通常的 partition() 函数），但是写错了主函数里的循环。

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if len(nums)==1:
            return nums[0]
        l,r = 0, len(nums)-1
        idx = search(nums, l, r)
        while idx!=len(nums)-k:
            if idx>len(nums)-k:
                r = idx-1
                idx = search(nums, l, r)
            else:
                l = idx+1
                idx = search(nums, l, r)
        return nums[len(nums)-k]
    
def search(arr, l, r):
    p = arr[l]
    while l<r:
        while l<r and arr[r]>=p:
            r -= 1
        arr[l] = arr[r]
        while l<r and arr[l]<=p:
            l += 1
        arr[r] = arr[l]
    arr[l] = p
    return l
```

**类似题目：**

Wiggle Sort II
Third Maximum Number
Kth Largest Element in a Stream
K Closest Points to Origin