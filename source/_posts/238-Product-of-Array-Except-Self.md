---
title: 238. Product of Array Except Self
date: 2019-08-28 23:57:57
tags:
---

Medium

https://leetcode.com/problems/product-of-array-except-self/

Given an array `nums` of *n* integers where *n* > 1,  return an array `output`such that `output[i]` is equal to the product of all the elements of `nums`except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Note:** Please solve it **without division** and in O(*n*).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)

**方法一：**

维护两个数组 left[] 和 right[]，分别表示从左往右扫、从右往左扫的时候，第 i 个元素左边的乘积和右边的乘积。

时间复杂度 O(n)，空间复杂度 O(n)

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums)<=1:
            return []
        left = [1]*len(nums)
        right = [1]*len(nums)
        for i in range(1, len(nums)):
            left[i] = left[i-1]*nums[i-1]
        for i in range(len(nums)-2, -1, -1):
            right[i] = right[i+1]*nums[i+1]
        return [left[i]*right[i] for i in range(len(nums))]
```

**方法二：**

在方法一的基础上把 left[] 和 right[] 直接合并为返回数组 ans[]，并用一个 temp 变量记录从右往左扫时的乘积。

时间复杂度 O(n)，空间复杂度 O(1)

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums)<=1:
            return []
        ans = [1]*len(nums)
        for i in range(1, len(nums)):
            ans[i] = ans[i-1]*nums[i-1]
        temp = 1
        for i in range(len(nums)-2, -1, -1):
            temp *= nums[i+1]
            ans[i] *= temp
        return ans
```

**类似题目：**
Paint House II