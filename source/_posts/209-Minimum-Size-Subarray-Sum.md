---
title: 209. Minimum Size Subarray Sum
date: 2019-08-26 19:00:15
tags:
---

Medium

https://leetcode.com/problems/minimum-size-subarray-sum/

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**

If you have figured out the *O*(*n*) solution, try coding another solution of which the time complexity is *O*(*n* log *n*). 

**方法：**

滑动窗口方法，注意判断 min_len 的位置

```python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==0:
            return 0
        sum_ = 0
        for n in nums:
            sum_ += n
        if sum_<s:
            return 0
        sum_ = 0
        l,r = 0,0
        min_len = len(nums)
        while r<len(nums):
            sum_ += nums[r]
            while l<=r and sum_>=s:
                min_len = min(min_len, r-l+1)
                sum_ -= nums[l]
                l += 1
            r += 1
        return min_len
```

**类似题目：**

Maximum Size Subarray Sum Equals k
Maximum Length of Repeated Subarray