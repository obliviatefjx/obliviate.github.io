---
title: 416. Partition Equal Subset Sum
date: 2019-09-20 19:04:59
tags:
---

Medium

https://leetcode.com/problems/partition-equal-subset-sum/

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

---

2019.9.20 没做出来，参考 https://blog.csdn.net/fuxuemingzhu/article/details/79787425

这道题我真的...照着 0-1 背包的思路写，还是有的题总是过不了，看来我还需要加强背包系列的知识点。

**方法：**

0-1 背包问题

```python
class Solution(object):
    def canPartition(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums)==1:
            return False
        total = sum(nums)
        if total%2==1:
            return False
        target = total/2
        dp = [False]*(total+1)
        dp[0] = True
        for n in nums:
            for j in range(target, n-1, -1):
                dp[j] = dp[j] or dp[j-n]
        return dp[target]
```

**类似题目：**

[Partition to K Equal Sum Subsets](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

