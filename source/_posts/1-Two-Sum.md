---
title: 1. Two Sum
date: 2019-08-24 01:30:12
tags:
---

Easy

https://leetcode.com/problems/two-sum/

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

**方法：**

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        d = {}
        for i in range(len(nums)):
            d[nums[i]] = i
        for i in range(len(nums)):
            if target-nums[i] in d and d[target-nums[i]]!=i:
                return [i, d[target-nums[i]]]
        return 
```

**类似题目：**

3Sum

4Sum

Two Sum II - Input array is sorted

Two Sum III - Data structure design

Two Sum IV - Input is a BST

Two Sum Less Than K

