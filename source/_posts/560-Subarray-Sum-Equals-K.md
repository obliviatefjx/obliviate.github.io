---
title: 560. Subarray Sum Equals K
date: 2019-09-04 01:06:38
tags:
---

Medium

https://leetcode.com/problems/subarray-sum-equals-k/

Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

**Example 1:**

```
Input:nums = [1,1,1], k = 2
Output: 2
```

**Note:**

1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer **k** is [-1e7, 1e7].

---

2019.9.4 没做出来，参考 https://zhuanlan.zhihu.com/p/36439368 和 https://blog.csdn.net/fuxuemingzhu/article/details/82767119

**方法：**

由于数据量大，不能用暴力解法。采用 PrefixSum 方法，用一个字典 prefix{} 统计 nums[] 从 index=0 开始到各个位置截至时的前缀和的个数，例如 prefix[5] = 2 表示从 nums[0] 开始的连续数组中有 2 个连续数组的和为 5，这样遍历 nums[] 时计算到当前位置的前缀和 sum\_，只要 sum\_-k 在 prefix{} 中则表示有若干个从 nums[0] 开始的连续数组和为 sum\_-k，那么那些连续数组的后一个元素到当前元素的数组和就为 k。

时间复杂度 O(n)，空间复杂度 O(n)

```python
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if len(nums)==0:
            return 0
        cnt = 0
        sum_ = 0
        prefix = {}
        prefix[0] = 1
        for n in nums:
            sum_ += n
            if (sum_-k) in prefix:
                cnt += prefix[sum_-k]
            prefix[sum_] = prefix.get(sum_,0)+1
        return cnt
```

**类似题目：**

Continuous Subarray Sum
Subarray Product Less Than K
Find Pivot Index
Subarray Sums Divisible by K

