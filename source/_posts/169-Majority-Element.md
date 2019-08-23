---
title: 169. Majority Element
date: 2019-08-22 23:52:35
tags:
---

Easy

https://leetcode.com/problems/majority-element/

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**方法：**

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==1:
            return nums[0]
        cnt = 0
        ans = 0
        for i in range(len(nums)):
            if cnt==0:
                ans = nums[i]
                cnt += 1
            else:
                if nums[i]==ans:
                    cnt += 1
                else:
                    cnt -= 1
        return ans
```

**类似题目：**

[229. Majority Element II](https://leetcode.com/problems/majority-element-ii/)

