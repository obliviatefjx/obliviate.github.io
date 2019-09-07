---
title: 645. Set Mismatch
date: 2019-09-01 16:18:22
tags:
---

Easy

https://leetcode.com/problems/set-mismatch/

The set `S` originally contains numbers from 1 to `n`. But unfortunately, due to the data error, one of the numbers in the set got duplicated to **another** number in the set, which results in repetition of one number and loss of another number.

Given an array `nums` representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

**Example 1:**

```
Input: nums = [1,2,2,4]
Output: [2,3]
```

**Note:**

1. The given array size will in the range [2, 10000].
2. The given array's numbers won't have any order.

--------

2019.9.1 没做出来，参考 https://blog.csdn.net/mebiuw/article/details/76277485

题目理解错了，“The given array's numbers won't have any order.” 我理解成了数组中的数字是乱序的，但是根据答案来看的话应该是有序的，这样就简单很多了。

**方法：**

注意 nums[] 中的数字是 1~n，而 index 是 0~n-1，需要减 1。

```python
class Solution(object):
    def findErrorNums(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        dup, mis = -1,-1
        for i in range(len(nums)):
            if nums[abs(nums[i])-1]<0:
                dup = abs(nums[i])
            else:
                nums[abs(nums[i])-1] *= -1
        for i in range(len(nums)):
            if nums[i]>0:
                mis = i + 1 
        return [dup, mis]
```



**类似题目：**

Integer to English Words
Complex Number Multiplication
Transform to Chessboard