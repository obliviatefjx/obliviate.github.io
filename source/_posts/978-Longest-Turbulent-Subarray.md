---
title: 978. Longest Turbulent Subarray
date: 2019-08-24 22:52:43
tags:
---

Medium

https://leetcode.com/problems/longest-turbulent-subarray/

A subarray `A[i], A[i+1], ..., A[j]` of `A` is said to be *turbulent* if and only if:

- For `i <= k < j`, `A[k] > A[k+1]` when `k` is odd, and `A[k] < A[k+1]`when `k` is even;
- **OR**, for `i <= k < j`, `A[k] > A[k+1]` when `k` is even, and `A[k] < A[k+1]` when `k` is odd.

That is, the subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

Return the **length** of a maximum size turbulent subarray of A.

**方法：**

```python
class Solution(object):
    def maxTurbulenceSize(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        # 1 2 1 2 1 2 1 2 first_small
        # 3 2 3 2 3 2 3 2 first_big
        if len(A)<=1:
            return len(A)
        first_small = [1]*len(A)
        first_big = [1]*len(A)
        max_ = -1
        for i in range(1, len(A)):
            if i%2==0:
                first_small[i] = first_small[i-1]+1 if A[i]<A[i-1] else 1
                first_big[i] = first_big[i-1]+1 if A[i]>A[i-1] else 1
            else:
                first_small[i] = first_small[i-1]+1 if A[i]>A[i-1] else 1
                first_big[i] = first_big[i-1]+1 if A[i]<A[i-1] else 1
            max_ = max(max_, first_small[i], first_big[i])
        return max_
```

**类似题目：**

Freedom Trail
Array Partition I
Race Car