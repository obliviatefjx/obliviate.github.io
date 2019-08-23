---
title: 229. Majority Element II
date: 2019-08-23 00:33:21
tags: 
---

Medium

https://leetcode.com/problems/majority-element-ii/

Given an integer array of size *n*, find all elements that appear more than `⌊ n/3 ⌋` times.

**Note:** The algorithm should run in linear time and in O(1) space.

**Example:**

```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

**方法：**

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums)==1:
            return nums
        ans = [0, 0]
        cnt = [0, 0]
        for i in range(len(nums)):
            match = False
            for j in range(2):
                if ans[j]==nums[i]:
                    match = True
                    cnt[j] += 1
                    break
            if match:
                continue
            full = True
            for j in range(2):
                if cnt[j]==0 :
                    ans[j] = nums[i]
                    cnt[j] += 1
                    full = False
                    break
            match = False
            if full:
                for j in range(2):
                    if nums[i]==ans[j]:
                        cnt[j] += 1
                        match = True
                if not match:
                    cnt[0] -= 1
                    cnt[1] -= 1
        res = [ans[i] for i in range(2) if cnt[i]>0]
        cnt = [0]*len(res)
        if len(res)>0:
            for n in nums:
                for j in range(len(res)):
                    if n==res[j]:
                        cnt[j] += 1
        return [res[i] for i in range(len(cnt)) if cnt[i]>len(nums)/3]
```

