---
title: 16. 3Sum Closest
date: 2019-08-24 18:26:40
tags:
---

Medium

https://leetcode.com/problems/3sum-closest/

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

**方法：**

和 15. 3Sum 相同，只是多了一个保存最小差值的变量。

```python
class Solution(object):
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums)<3:
            return []
        nums.sort()
        res = float('inf')
        ans = []
        for t in range(len(nums)-2):
            i,j = t+1, len(nums)-1
            while i<j:
                sum_ = nums[t] + nums[i] + nums[j]
                if abs(sum_-target)<res:
                    res = abs(sum_ - target)
                    ans = [nums[t], nums[i], nums[j]]
                if sum_==target:
                    return target
                elif sum_<target:
                    i += 1
                else:
                    j -= 1
        return sum(ans)
```

**类似题目：**

3sum-smaller