---
title: 268. Missing Number
date: 2019-09-01 16:30:07
tags:
---

Easy

https://leetcode.com/problems/missing-number/

Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example:**

```
Input: [3,0,1]
Output: 2
```

**Note**:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

-----

2019.9.1 没写出来时间复杂度 O(n) 且空间复杂度 O(1) 的解法，参考 https://blog.csdn.net/fuxuemingzhu/article/details/70332471

**方法：**

把数组求和，减去 0~n 的总和就是 missing number

```python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        sum_ = 0
        for n in nums:
            sum_ += n
        for i in range(len(nums)+1):
            sum_ -= i
        return abs(sum_)
```



**类似题目：**

First Missing Positive
Couples Holding Hands