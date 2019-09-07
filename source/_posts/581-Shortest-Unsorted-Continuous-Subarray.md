---
title: 581. Shortest Unsorted Continuous Subarray
date: 2019-08-25 01:23:51
tags:
---

Easy

https://leetcode.com/problems/shortest-unsorted-continuous-subarray/

Given an integer array, you need to find one **continuous subarray** that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the **shortest** such subarray and output its length.

**Example 1:**

```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

**Note:**

1. Then length of the input array is in range [1, 10,000].
2. The input array may contain duplicates, so ascending order here means **<=**

**方法：**

参考 https://blog.csdn.net/fuxuemingzhu/article/details/79254454

先排序，然后找排序前后第一个和最后一个不同的数字位置。

```python
class Solution(object):
    def findUnsortedSubarray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<=1:
            return 0
        new = sorted(nums)
        l,r = 0,len(nums)-1
        while l<len(nums)-1 and nums[l]==new[l]:
            l += 1
        if l==len(nums)-1:
            return 0
        while r>0 and nums[r]==new[r]:
            r -= 1  
        return r-l+1
```

**类似题目：**

Construct Binary Tree from Inorder and Postorder Traversal
Minimum Size Subarray Sum
Beautiful Arrangement II