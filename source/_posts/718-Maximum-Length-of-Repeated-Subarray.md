---
title: 718. Maximum Length of Repeated Subarray
date: 2019-08-26 19:16:15
tags:
---

Medium

https://leetcode.com/problems/maximum-length-of-repeated-subarray/

Given two integer arrays `A` and `B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**

```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

**Note:**

1. 1 <= len(A), len(B) <= 1000
2. 0 <= A[i], B[i] < 100

**方法：**

方法和 “求两个字符串的最长公共子串” 相同，都是二维 DP

```python
class Solution(object):
    def findLength(self, A, B):
        """
        :type A: List[int]
        :type B: List[int]
        :rtype: int
        """
        if len(A)==0 or len(B)==0:
            return 0
        dp = [[0]*len(B) for _ in range(len(A))]
        max_len = 0
        for i in range(len(A)):
            for j in range(len(B)):
                if A[i]==B[j]:
                    if i==0 or j==0:
                        dp[i][j] = 1
                    else:
                        dp[i][j] = dp[i-1][j-1] + 1
                max_len = max(max_len, dp[i][j])
        return max_len
```

**类似题目：**

Unique Binary Search Trees II
Analyze User Website Visit Pattern
Online Majority Element In Subarray