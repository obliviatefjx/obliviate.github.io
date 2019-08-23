---
title: 312. Burst Balloons
date: 2019-08-24 00:41:28
tags:
---

**Hard**

https://leetcode.com/problems/burst-balloons/

Given `n` balloons, indexed from `0` to `n-1`. Each balloon is painted with a number on it represented by array `nums`. You are asked to burst all the balloons. If the you burst balloon `i` you will get `nums[left] * nums[i] * nums[right]` coins. Here `left` and `right` are adjacent indices of `i`. After the burst, the `left` and `right` then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

**Note:**

- You may imagine `nums[-1] = nums[n] = 1`. They are not real therefore you can not burst them.
- 0 ≤ `n` ≤ 500, 0 ≤ `nums[i]` ≤ 100

**Example:**

```
Input: [3,1,5,8]
Output: 167 
Explanation: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
             coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

**方法：**

边界条件好难写...

```python
class Solution(object):
    def maxCoins(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==0:
            return 0
        if len(nums)==1:
            return nums[0]
        # 在 nums 首尾增加 1 作为辅助
        arr = [0]*(len(nums)+2)
        for i in range(len(nums)):
            arr[i+1] = nums[i]
        arr[0], arr[-1] = 1, 1
        
        dp = [[0]*(len(nums)+2) for _ in range(len(nums)+2)]
        for len_ in range(1, len(nums)+1):
            for left in range(1, len(nums)+2-len_):
                right = left + len_ - 1
                for k in range(left, right+1):
                    dp[left][right] = max(dp[left][right], dp[left][k-1]+dp[k+1][right]+arr[k]*arr[left-1]*arr[right+1])
        return dp[1][len(nums)]
```