---
title: 494. Target Sum
date: 2019-09-11 00:39:15
tags:
---

Medium

https://leetcode.com/problems/target-sum/

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols `+` and `-`. For each integer, you should choose one from `+` and `-` as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**

```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

**Note:**

1. The length of the given array is positive and will not exceed 20.
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.

---

2019.9.11 独立做出来了

虽然是独立写出来的，但是参考了之前留在页面上的注释：

“其实一般能用dfs解决的题目，如果题目只要求满足条件的数字而不是所有的结果且dfs超时时，解决方法其实基本只有一条路：动态规划”

于是用了 DP

**方法：**

用一个长度和 num[] 相同的 dp[]，dp[i] 为一个字典，key 为计算 nums[0]~nums[i] 的所有加减号的值，value 为相应的次数。

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        dp = [{} for _ in range(len(nums))]
        for i in range(len(nums)):
            if i==0:
                dp[i][nums[i]] = dp[i].get(nums[i], 0) + 1
                dp[i][-nums[i]] = dp[i].get(-nums[i], 0) + 1
            else:
                for key in dp[i-1]:
                    dp[i][key+nums[i]] = dp[i].get(key+nums[i], 0) + dp[i-1][key]
                    dp[i][key-nums[i]] = dp[i].get(key-nums[i], 0) + dp[i-1][key]
        return dp[-1].get(S,0)
```

**类似题目：**

Expression Add Operators