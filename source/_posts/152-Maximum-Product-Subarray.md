---
title: 152. Maximum Product Subarray
date: 2019-09-07 14:00:11
tags:
---

Medium

https://leetcode.com/problems/maximum-product-subarray/

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

---

2019.9.7 没做出来，参考 https://www.cnblogs.com/grandyang/p/4028713.html 和 https://blog.csdn.net/fuxuemingzhu/article/details/83211451

**方法：**

动态规划

用两个 dp 数组 max\_[] 和  min\_[]，其中 max\_[i] 表示子数组 [0, i] 范围内并且一定包含 nums[i] 的最大子数组乘积，min\_[i] 表示子数组 [0, i] 范围内并且一定包含 nums[i] 的最小子数组乘积。

初始化时 max\_[i]和 min\_[i] 都初始化为 nums[0]，其余都初始化为0。

从数组的第 2 个数字开始遍历，那么此时的最大值和最小值只会在这三个数字之间产生，即 **nums[i]、nums[i]\*max\_[i-1]、nums[i]\*min\_[i-1]**。所以我们用三者中的最大值来更新 max\_[i]，用最小值来更新 min\_[i]。

由于最终的结果不一定会包括 nums[-1] 这个数字，所以 max\_[i] 不一定是最终解，需要不断更新的结果 ans。

```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==0:
            return 0
        max_ = [0]*len(nums)
        min_ = [0]*len(nums)
        ans = nums[0]
        for i in range(len(nums)):
            if i==0:
                max_[i] = nums[i]
                min_[i] = nums[i]
            else:
                max_[i] = max(nums[i], nums[i]*max_[i-1], nums[i]*min_[i-1])
                min_[i] = min(nums[i], nums[i]*max_[i-1], nums[i]*min_[i-1])
            ans = max(ans, max_[i])
        return ans
```

**类似题目：**

Maximum Product of Three Numbers
Subarray Product Less Than K