---
title: 53. Maximum Subarray
date: 2019-08-24 01:40:37
tags:
---

Easy

https://leetcode.com/problems/maximum-subarray/

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

**方法：**

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==1:
            return nums[0]
        dp = [0]*len(nums)
        dp[0] = nums[0]
        max_ = dp[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i-1], 0) + nums[i]
            max_ = max(max_, dp[i])
        return max_
```

**类似题目：**

Degree of an Array
Longest Turbulent Subarray